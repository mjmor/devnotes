---
layout: default
title: UX/UI Development
nav_order: 1
permalink: /webdev/uxui
parent: Web Development
has_children: false
---

# UX/UI Development
{: .no_toc }

Foundational knowledge for all types of UX/UI development tasks ranging from theming to client-side software.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Themes & Styles

### HyperText Markup Language (HTML)

Additional resources:
* [HTML Standard](https://html.spec.whatwg.org/)

### Cascading Style Sheets (CSS)

**TODO: Add overview and fundamentals.**

Additional resources:
* [Mozilla Learn CSS](https://developer.mozilla.org/en-US/docs/Learn/CSS)
* [Scalable and Modern Architecture for CSS](https://smacss.com/)

**Aggregation and Minimization / Compression**

**TODO: Add notes on tech like webpack.**

**PX vs. REM vs. EM**

PX stands for pixel.

_When to use PXs_
* When you need a fixed layout size to prevent scaling from breaking functionality (e.g. overlapping buttons or not being able to fit a control panel in the viewport).

REM is a relative unit of measurement REM stands for root EM.

_When to use REMs_
* When you want elements to be scalable based on the HTML element font size which is typically based on user browser settings. So it's good to generally use REMs to respect user browser settings.

_REM Details_
* REM computes px relative to the parent HTML (i.e. what the browser or website has set at the root HTML element)
* The computed value is HTML_parent_font_px * element_rem. E.g. HTML element font size is set to 16px font-size and current element width is set to 10rem then the current element width will be computed as 160px.
* Note: The HTML element font size is often set by the browser (default or user settings) and not directly in stylesheets. This is different from window zoom which scales up the size of a pixel to take up more device pixels (see [more details on StackOverflow](https://stackoverflow.com/questions/29390155/what-exactly-changes-in-the-css-rendering-when-desktop-browsers-zoom-in-or-out)).

EM is a relative unit of measurement.

_When to use EMs_
* When an element size must scale with the font size of that element. A good example is the padding of a button since you would want the padding to scale with the font size of the button (regardless of the HTML element font size).

_EM Details_
* EM computes px relative to the element that the em value is used on
* The computed value is element_font_px * element_rem. E.g. Current element font size is set to 16px font-size and current element width is set to 10em then the current element width will be computed as 160px.
* Using ems can be tricky because font-size of the current element is inerited from parent elements by default. Therefore, if we have nested elements setting font size with ems then there could be an exponential increase in font-size through inheritance. A fast fix in this case would be to set the current element (or its parent) font-size to 1rem so that it resets the font-size inheritance chain to the HTML element.

_When to use neither EMs nor REMs nor PXs_
* When setting line height, do not use any units. Unitless line height will compute the line height based on the children font settings.

See a [comprehensive comparison guide](https://webdesign.tutsplus.com/comprehensive-guide-when-to-use-em-vs-rem--cms-23984t) or a [visual overview](https://webdesign.tutsplus.com/a-visual-guide-to-em-and-rem-units--CRS-200720c/overview-of-px-em-and-rem).

### Bootstrap

Bootstrap is a front-end styling framework focused on responsive, mobile first, and modern design. Bootstrap uses SASS to generate large libraries of CSS that is used to style HTML elements mostly through HTML classes.

Additional resources:
* [main docs](https://getbootstrap.com/docs/5.0/getting-started/introduction/)
* [using SASS to customize bootstrap](https://getbootstrap.com/docs/5.0/customize/sass/)
* [the utilities API & custom classes](https://getbootstrap.com/docs/5.0/utilities/api/)
* [Bootstrap approach](https://getbootstrap.com/docs/5.0/extend/approach/)

## Client-Side Software

### Javascript Linters, Formatters, and Codemods

* [ESlint](https://eslint.org/)
* [Prettier](https://prettier.io/)
* [JS Codemod](https://github.com/facebook/jscodeshift)
* [Suppress ESLint Codemod](https://github.com/amanda-mitchell/suppress-eslint-errors)

### Web Components

**TODO: Add overview and fundamentals.**

Additional resources:
  * [main docs](https://developer.mozilla.org/en-US/docs/Web/API/Web_components)
  * [slots, state, & the web component lifecycle](https://stackoverflow.com/questions/48663678/how-to-have-a-connectedcallback-for-when-all-child-custom-elements-have-been-c)
  * [CSS isolation & the shadow dom](https://css-tricks.com/styling-a-web-component/)

### Storybook

Storybook is a small, development-only, framework agnostic workshop to isolate, render, and test web components (Web Components, React, Vue.js) in various states.

Additional resources:
* [main docs](https://storybook.js.org/docs/react/get-started/why-storybook)

### Drupal Theming

See [Drupal: Themes](/webdev/drupal#themes) and [Drupal: Front-End Development](/webdev/drupal#front-end-development).
