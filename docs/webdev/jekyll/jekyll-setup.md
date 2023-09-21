---
layout: default
title: Setup
nav_order: 1
permalink: /webdev/jekyll/setup
parent: Jekyll
grand_parent: Web Development
---

# Jekyll Setup
{: .no_toc }

Jekyll is a static site generator framework built in Ruby. Below are notes on setting up a new website using Jekyll.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Creating a New Site

Jekyll has a self-titled command: `Jekyll`.

<script src="https://gist.github.com/mjmor/2781f916dafcd0edc883d011909fb8ce.js"></script>

## Serving the Site Locally

Jekyll has a built in server to generate and serve the site locally. Just like any Ruby executable,
it's best to execute the `jekyll` command by prepending `bundle exec` so that the gem versions
specified in the project's Gemfile are used instead of the global/local context.

<script src="https://gist.github.com/mjmor/e3f07538e8e49f80791a31530037ae4f.js"></script>