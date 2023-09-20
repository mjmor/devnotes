---
layout: default
title: UX/UI Development
nav_order: 1
permalink: /web-dev/uxui
parent: Web Development
has_children: false
---

# UX/UI Development
{: .no_toc }

Foundational knowledge for all types of UX/UI development tasks ranging from visual design to client-side software.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Visual Design

### Typography

Typography is the style and appearance of (digitally or physically) printed text.

Additional resources:
  * [web typography basics in Figma](https://webdesign.tutsplus.com/web-typography-basics-in-figma--CRS-200982c)
  * [advanced typography design in Figma](https://webdesign.tutsplus.com/advanced-typography-design-in-figma--CRS-200991c/adjusting-font-sizes)

## Themes & Styles

### Cascading Style Sheets (CSS)

**TODO: Add overview and fundamentals.**

#### REM vs. EM

REM:
* Computes px relative to the parent HTML (i.e. what the browser or website has set at the root HTML element)
* **TODO: Add examples of when to use REM instead of EM and why.**

EM:
* Computes px relative to the element that the em value is used on
* **TODO: Add examples of when to use EM instead of REM and why.**

See a [comprehensive comparison guide](https://webdesign.tutsplus.com/comprehensive-guide-when-to-use-em-vs-rem--cms-23984t) or a [visual overview](https://webdesign.tutsplus.com/a-visual-guide-to-em-and-rem-units--CRS-200720c/overview-of-px-em-and-rem).

### Bootstrap

Bootstrap is a front-end styling framework focused on responsive, mobile first, and modern design. Bootstrap uses SASS to generate large libraries of CSS that is used to style HTML elements mostly through HTML classes.

Additional resources:
* [main docs](https://getbootstrap.com/docs/5.0/getting-started/introduction/)
* [using SASS to customize bootstrap](https://getbootstrap.com/docs/5.0/customize/sass/)
* [the utilities API & custom classes](https://getbootstrap.com/docs/5.0/utilities/api/)
* [Bootstrap approach](https://getbootstrap.com/docs/5.0/extend/approach/)

## Client-Side Software

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

See ![Drupal: Themes](./drupal.md#themes).
