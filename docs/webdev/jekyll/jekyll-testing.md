---
layout: default
title: Testing
nav_order: 2
permalink: /webdev/jekyll/testing
parent: Jekyll
grand_parent: Web Development
---

# Jekyll Testing
{: .no_toc }

Jekyll is a static site generator framework built in Ruby. Below are notes on testing Jekyll sites.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Manual Testing

Jekyll doesn't come with any nifty testing capabilities out of the box. The only thing you get out of the box is the ability to deploy your site locally and manually test the site.

Naturally, this isn't sufficient for complex web apps, so this guide will go in depth on how to setup automated tests for a Jekyll site.

## Automated Testing

In order to build automated tests for our Jekyll site, we'll need to assemble an ensemble of Ruby web testing frameworks. Hat tip to [@deanmarano](https://github.com/deanmarano) for the [setup guide](https://gist.github.com/deanmarano/aeae5cd2d357fec1b06e30ead397d4e3).

### Setup

Writing automated tests for our Jekyll site involves string together a few common types of tech:
  1. [RSpec](http://rspec.info/) - A test framework to define and execute test suites in Ruby
  1. [Capybara](https://github.com/teamcapybara/capybara) - A web test middleware that defines a web interaction DSL and integration point for a web driver
  1. [Selenium](https://www.selenium.dev/) - A web driver to automate a browser a report back to Capybara
  1. [Puma]()
  1. [rack-jekyll](https://github.com/adaoraul/rack-jekyll) - A Ruby Gem that will serve our static site during testing using Ruby
  1. [Puma](https://puma.io/) - A web server to serve requests made by Capybara and pass the request to Rack.

Let's setup our Gemfile to add those dependencies:

<script src="https://gist.github.com/mjmor/bdb8a4c5770e0e4e3b3beb2d55b59c04.js"></script>

Run `bundle install && rbenv rehash` to install the new Gems and add any new executables to your executable path.

Next, we're going to configure RSpec to use Capybara, Selenium, and Rack to orchestrate web tests in our RSpec tests.

Initialize RSpec:

<script src="https://gist.github.com/mjmor/59d14cf925913c5a831351af30851532.js"></script>

Two files are produced: `.rspec` and `spec/spec_helper.rb`. `.rspec` configures the output for rspec and `spec/spec_helper.rb` loads tests and configures the testing environment. Let's configure rspec to use Capybara, Selenium, and Rack.

<script src="https://gist.github.com/mjmor/15815a212d30e5667070e2052580562e.js"></script>

### Writing Tests

Now that we have RSpec configured to run our web testing frameworks, we can write RSpec tests with Capybara DSL to verify our website behavior.

Here's an example test for a new Jekyll site:

<script src="https://gist.github.com/mjmor/e578faf37c97a8d445ba07e38060dab8.js"></script>

### Running Tests

To run the tests using RSpec, execute `bundle exec rspec`.