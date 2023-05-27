---
layout: default
title: Elastic Beanstalk
nav_order: 1
permalink: /dev-ops/aws/eb
parent: AWS
grand_parent: DevOps
---

# AWS Elastic Beanstalk
{: .no_toc }

Elastic Beanstalk is a platform-as-a-service (PaaS) for hosting web apps. Below are notes on
configuring an Elastic Beanstalk environment with a new web app.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Configure App to Run on Elastic Beanstalk

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

## Where To Look For Logs

<!-- Add notes on eb-engine.log, puma.log, etc. -->