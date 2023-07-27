---
layout: default
title: Themes
nav_order: 2
permalink: /web-dev/jekyll/themes
parent: Jekyll
grand_parent: Web Development
---

# Jekyll Themes
{: .no_toc }

Jekyll is a static site generator framework built in Ruby. Below are notes on building and modifying Jekyll themes. For more in-depth
docs on Jekyll themes see [the main docs](https://jekyllrb.com/docs/themes/).

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Overview of Jekyll Themes

Jekyll themes are Ruby Gems containing assets, stylesheets, and layout configurations for your site. The sites `Gemfile` and `_config.yaml` tell Jekyll
which theme to use.

As an example, consider a new Jekyll site that comes with [Minima](https://github.com/jekyll/minima) as the default theme. You'll notice your Gemfile has the following line:

<script src="https://gist.github.com/mjmor/d341071cda3a3a6ecdacb3145eb86031.js"></script>

You'll also notice the sites _config.yaml has the following theme and plugin lines:

<script src="https://gist.github.com/mjmor/528820201b42a2da918e7a7066206649.js"></script>

## Changing the Theme

You can find many open source themes on [Github](https://github.com/topics/jekyll-theme). Once you find one, you can update the config files referenced above then run `bundle install` and `bundle exec jekyll build`.

## Modifying an Existing Theme

The theme is a directory containing assets, stylesheets, and layout configurations for your site. To modify the theme, simply add the theme's
file you want to modify to your site director in the exact same directory location. Jekyll will use the file in your site directory instead of
the theme's file.

For example, to override the site footer in the Minima theme:
1. Locate the Minima theme and observe its structure
<script src="https://gist.github.com/mjmor/7e61e1350b68ce377b36d083d12327fd.js"></script>

2. Create an `_includes` directory with a file called `footer.html` in your site repository.
It might also be easier to copy the theme file and edit it instead.
3. Update `footer.html` to include the HTML template code you want.

## Creating a New Theme

A theme can be created using Jekyll's `new-theme` subcommand or by simply copying an existing themes structure. I prefer the latter because it's a nice starting point, and I'll usually use it on a single site as a ["regular theme"](https://jekyllrb.com/docs/themes/#converting-gem-based-themes-to-regular-themes) before creating a Ruby Gem later on.

To copy the theme:

<script src="https://gist.github.com/mjmor/bac8eca608cba33201512550c2eeb15c.js"></script>

After the theme is copied, you can modify the theme to your heart's content. Later, you might consider copying that theme back to its own
directory so you can [create a Gem-based theme](https://jekyllrb.com/docs/themes/#creating-a-gem-based-theme).