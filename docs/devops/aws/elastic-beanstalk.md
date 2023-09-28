---
layout: default
title: Elastic Beanstalk
nav_order: 1
permalink: /dev-ops/aws/eb
parent: AWS
grand_parent: Developer Operations
---

# AWS Elastic Beanstalk
{: .no_toc }

Elastic Beanstalk is a platform-as-a-service (PaaS) for hosting web apps. Below are notes on
configuring an Elastic Beanstalk environment with a new web app.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Configure Your App to Run on Elastic Beanstalk

### Aligning Environment Software Versions

Elastic Beanstalk only supports a [few specific versions](https://docs.aws.amazon.com/elasticbeanstalk/latest/platforms/platforms-supported.html#platforms-supported.ruby) for the software used in our web
app (e.g. Ruby, Puma Server), so we'll need to make sure our web app is configured to
use those versions as well. Otherwise, we'll run into app install errors.

First, take a look at our Gemfile to check the version of Ruby being used. If the Gemfile isn't using the correct version (3.0.6 at the time of writing), then install the correct version using `rbenv`.

<script src="https://gist.github.com/mjmor/bcffe5fafcfaee26513316c3e34ad553.js"></script>

Next, update your Gemfile to use that version of Ruby. The easiest way to do this is to let the
Gemfile read `.ruby-version` file created by `rbenv`.

<script src="https://gist.github.com/mjmor/3721d53bd4be69a75fceb921dfca24aa.js"></script>

Next, check the version of Puma being used. Look for `puma ...` in your Gemfile. If the Gemfile isn't using the correct version (6.2.2 at the time of writing), then update uninstall the old version and reinstall the new version.

<script src="https://gist.github.com/mjmor/4562cba67aa2c610d84c3085087522c1.js"></script>

<!-- Add notes on install sql-devel. -->

### Installing Dependencies on Elastic Beanstalk

Elastic Beanstalk uses CentOS on the EC2 instances it spins up, and the default CentOS image is missing
some common package dependencies. For example, a default Rails app will need the `sqlite` Gem which requires
a sqlite development package to create the headers.

Elastic Beanstalk allows various [script hooks and configuration files](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/platforms-linux-extend.html) to be included in your app that will customize the
CentOS environment during deployment. We can write a [YAML configuration file](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/ebextensions.html) to install the `sqlite-devel` dependency from `yum`
package manager.

<script src="https://gist.github.com/mjmor/95360eb32e965df5661787bed908608e.js"></script>

## Deploying Your App

If you don't already have an EB environment configured, follow the
[guide AWS provides](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.environments.html)
for setting up an EB environment. However, instead of using the sample application option, you can jump right to deploying your app from the environment setup.

To deploy your app, create an app source bundle. In the root of your project directory, run the following
commands.

<script src="https://gist.github.com/mjmor/5023189262d993869382a911b686176c.js"></script>

This will generate a app source bundle named `<my-app-source-bundle>.zip` in the directory about your app root
directory. Use this file as the app source bundle, then use the AWS EB console to 'Upload and Deploy'
the source bundle.

If your Elastic Beanstalk environment goes to into a 'Warning' or 'Critical' state, see [Where to Look For Logs](#where-to-look-for-logs) to debug.

## Configuring DNS for Your App

By default, the EB environment will serve your app over HTTP (port 80) using a public domain that looks like `<env-name>.<env-prefix>.<region>.elasticbeanstalk.com`. If you have a custom domain purchased through a
non-AWS provider, this section will walk through routing traffic from your custom domain to your EB
environment.

First, we'll use AWS Route 53 to configure our DNS records. Go to [Route 53 console](https://us-east-1.console.aws.amazon.com/route53/v2/home#Dashboard). Create a 'Hosted Zone' using your root domain for the 'Domain Name'.

Next, we'll create alias records to route traffic from our root domain and subdomains to go to our EB environment domain. Go to 'Hosted Zones' in Route 53 console and select the hosted zone we just created.

1. Select 'Create Record'
2. Leave subdomain blank for the first record we create so we can create a root record
3. Select record type 'A'
4. Enable 'Alias' toggle
5. From the 'Route traffic to' dropdown, select 'Alias to Elastic Beanstalk environment', the region where your EB environment resides, and finally the public domain of your EB environment.
6. Leave 'Simple routing' as the routing policy and 'Evaluate target health' enabled.

Finally, we'll your configure your domain registrar to use Amazons name servers instead of any default
name servers they may be using. For example, in Google Domains under DNS select 'Custom name servers'. Add the four name servers from the AWS Route 53 NS record.

Give the records a few minutes to propagate, then [use `dig` and `whois`](https://blog.dnsimple.com/2017/08/debugging-dns/)
to check that your DNS setup is correct. For example, you can check that your custom domain and
EB environment domain point to the same public IP.

<script src="https://gist.github.com/mjmor/65ab10cf2afc08cbd70ba1de788575f4.js"></script>

If you go to your custom domain in a browser and receive a timeout, it's probably because browsers are forcing connection to HTTPS (port 443) but EB environments serve only on HTTP (port 80) by default. Read on to [Setup SSL](#setup-ssl-on-eb-environment) to install an SSL certificate and serve traffic on port 443.

## Setup SSL on EB Environment

We'll use [`certbot`](https://certbot.eff.org/) to automatically install and renew our certs in our EB environment. The general process is as follows:
1. Install Certbot on our EC2 instances
2. Open 443 port on EC2 instances
3. Download and configure the certificate in Nginx
4. Automatically renew the certificate

### Install Certbot

We'll use our EB configuration files [described earlier](#installing-dependencies-on-elastic-beanstalk) to install certbot while bringing up EC2 instances.

<script src="https://gist.github.com/mjmor/08ac847f2103d9fd74be29f29be56f0a.js"></script>

### Allow Traffic on Port 443

We'll create another EB configuration file to allow traffic from any IP on port 443.

<script src="https://gist.github.com/mjmor/da97ab75320f6b9ce584a669f93d9dc9.js"></script>

### Donwload and Configure Certificate

We'll create a script hook to run certbot after Nginx has been installed and configured on the new EC2 instance. The following file is a script hook as opposed to a configuration file, so it should be placed in `.platform/hooks/postdeploy` in our app root directory.

<script src="https://gist.github.com/mjmor/ab027388778c177d1669822cc37129c2.js"></script>

We also have to have an EB configuration file to grant execute permissions to that script hook.

<script src="https://gist.github.com/mjmor/3e75f7516798ab38909a8ee1a3b0d551.js"></script>

### Automatically Renew the Certificate

Finally, we'll use EB configuration to create a crontab entry to renew the cert every 12 hours.

<script src="https://gist.github.com/mjmor/8d08ac780786b408698e4592b7b77f78.js"></script>

That's it! Go ahead and redeploy your app and try connecting to the site. You should see the site being served over port 443
(i.e. a lock icon in the browser).

## CI/CD on Elastic Beanstalk

Additional resources:
* [Guide on setting up CI/CD for web app and Elastic Beanstalk](https://www.buildon.aws/tutorials/deploy-webapp-eb-cdk#add-the-elastic-beanstalk-cdk-dependencies)
* [AWS SDK for Ruby (e.g. to setup CI/CD in the Ruby app)](https://docs.aws.amazon.com/sdk-for-ruby/v3/api/index.html)

## Where To Look For Logs

Here's a list of EB log file locations and what they contain:
* `/var/log/eb-engine.log` - All deployment steps. If EB configuration or app install fails, the logs will be here.
* `/var/log/cfn-init.log` - EB extension configuration logs only.
* `/var/log/eb-hooks.log` - EB script hooks.
* `/var/log/puma/` - Logs for Puma server.

For a full list of log file locations as well as how to customize locations, see the [AWS guide](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.logging.html).