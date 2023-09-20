# Drupal

Drupal is a CMS built in PHP and Javascript. Unlike other CMS, Drupal enforces
structured data for content.

Here's in-depth documentation on Drupal for admins and content editors: https://www.drupal.org/docs/user_guide/en/index.html

## Major Drupal Concepts
1. Entity - Anything that can have fields (e.g. content types, blocks, taxonomy, media, etc.)
2. Blocks - An area of the view.
3. Nodes - Any content item (i.e. any content type).
4. Views - A frame on the page. Contains business logic for selecting content to display.
5. Modules - An add-on feature built in PHP to augment or add on to Drupal core (e.g. layouts/themes, field types, migration helpers, etc.)

## Planning a Drupal Site
![Drupal Planning Diagram](./assets/drupal-planning.png)

## Content Types

A content type is a type of content with a collection of fields (values or references). A new content type may be needed when:
1. Information needed differs from existing content types (i.e. different set of fields)
2. The new content needs to be displayed differently from other content types (i.e. a custom template to render the content)

## Taxonomy

A taxonomy is a set of categories. There is no tree hierarchy to a taxonomy, however a taxonomy is an entity so it can have fields.

In taxonomies, Drupal calls category title/keys "vocabulary" and category entries/values "terms".

A taxonomy can be included as an entity reference field on another entity.

## Media

Media module was added in Drupal 9. The media module treats media as an entity. There is also the option to add an image as a normal (not an entity reference) field that is historic. There's not many good reasons to use the latter unless the value won't change often or be reused elsewhere.

## Modules

Modules are custom PHP software packages that augment how core drupal runs. They cover a wide variety of use cases.

Useful modules:
* BAT
* Simple google maps
* Linkit
* External links
* Pathauto
* Ctools
* Token
* Devel - development tools including content generation

## Users and Roles

The general workflow is: Create Roles -> Assign Permissions -> Add Users -> Test.

Note that the website creator is always a superuser (which is not an actual role).

Users are entities, meaning we can add fields to users (e.g. profile fields).

## Themes

Themes are exactly what they sound like: visual wrappers on the site. Themes are made up of .css, .js, and .twig html templates. Themes can define how content type are rendered in a view.

Themes may also contain ![layouts](./drupal.md#layouts) that are used for content types.

Specifically, Drupal operates in the follow fashion when receiving a web request:

<img src="./assets/drupal-request-processing-flow.png"  height="500">

## Layouts

Layout dictates how components are displayed, structured, and layed out across the page. This encompasses:
* Display manager (drupal core admin page for each component type)
* Blocks (special areas of the page like header, footer, nav, and sidebars/gutters)
* Layout Builder (drupal core admin page allowing you to manage layout for a content type)
* Views (each page on the site is a view)

### Display Manager

Allows you to manage simple settings regarding how content types are displayed. Settings include: (1) rearranging the order fields are displayed in the view, (2) whether the field is pulled from the database and rendered at all, and (3) whether and how the field label is rendered in the view alongside the field value.

That's all you can do here.

### Blocks

Blocks are not content. They are containers for functionality - nav, search bar - and content - header footer - around the website. Theme defines and provides block regions. Blocks are developed by modules or by drupal admin/content creators. Blocks are assigned to specific block regions. There is a specific content block designated in the block region. Blocks also can be configured to only be rendered based on some filters (page_path, etc.).

Custom block types can be created from drupal admin. Custom block types are an entity (they can have fields). This makes blocks useful for things like banners, alerts, and nav bars. This also makes blocks able to have references to other nodes (content, taxonomies, media) and change it's content based on those references.

### Layout Builder

Layout building is the general notion of having the ability to manage how a content type is rendered onscreen. There are many modules that allow different ways to manage content layout.

#### Generally How Layout Builders Work

A specific module will ad some functionality to the 'Manage display' admin panel for content types. The functionality can be toggled on and off for a content type but typically enables a layout builder / design suite / etc. allowing you to graphically configure how the content will be arranged onscreen.

#### Core: Layout Builder

Overview: https://www.drupal.org/docs/8/core/modules/layout-builder/layout-builder-overview

Drag and drop layout builder that let's you arrange blocks and fields of content. [Additional modules](https://www.drupal.org/docs/8/core/modules/layout-builder/additional-modules) allow you to do things like set admin permissions on who may edit a layout and add css directly from layout builder.

Layout defaults: https://www.drupal.org/docs/8/core/modules/layout-builder/creating-layout-defaults

### Views

Views are frames on the site. Views can be pages or blocks. Views manage:
* business logic (static or dynamic) used to select which entities to display onto the page and how to sort them
* general format with which to display the elements returned from the query

Entity filters in the view can also be exposed to visitors making a convenient filter tool.

## Other Tools & Features

### Multilingual Setup

Drupal comes with modules and workflows for content translation right out of the box.

See the [docs](https://www.drupal.org/docs/user_guide/en/multilingual-chapter.html).

## Developing on Drupal

As a drupal developer you're writing either a theme (JS, HTML, CSS) or a module (PHP code). Modules are typically considered back-end because they run server side and can be written to handle sysadmin type work (e.g. DB migrations). Themes are tpyically considered front-end because they control how the site looks and feels. Client side applications may also be developed but they'd typically be housed in a content type instead of included in the theme.

References:
  * [Development Docs](https://www.drupal.org/docs/develop)
  * [API Docs w/ Examples](https://www.drupal.org/docs/develop/drupal-apis)
  * [API Docs from Source Code](https://api.drupal.org/api/drupal)
  * [Coding Standards](https://www.drupal.org/docs/develop/standards)

### Understanding A Drupal Site

Drupal provides a plethora of abstraction on top of the database layer, application / business layer, and presentation layer. To better understand how different Drupal entities are related to one another, you can use the [Entity Relationship Diagrams module](https://www.drupal.org/project/erd).

### Front-End Development

**Read this [full overview](https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Render%21theme.api.php/group/themeable/10) for how Drupal handles rendering of data from server-side (modules and preprocessors) to client-side (HTML templates, CSS, and JS).**

#### HTML Templating

The most common template engine used in Drupal is [Twig PHP templates](https://twig.symfony.com/doc/3.x/templates.html#twig-for-template-designers). Twig templates are
associated with all sorts of objects in Drupal (Regions, Blocks, Nodes, Fields, Taxonomy Terms, Fields, etc.) and define how to render an object in HTML. These
objects have defaults (defined via Drupal admin UI) that may be overridden. See
file [pattern for overriding defaults](https://www.drupal.org/docs/theming-drupal/twig-in-drupal/twig-template-naming-conventions). Twig also provides [a debug utility](https://www.drupal.org/docs/theming-drupal/twig-in-drupal/locating-template-files-with-debugging) that shows which template file is generating the HTML for a given HTML section.

[Twig Tweak](https://www.drupal.org/project/twig_tweak) is a module that provides many helper functions for template development. Check out the [Twig Tweak cheatsheet](https://git.drupalcode.org/project/twig_tweak/-/blob/3.x/docs/cheat-sheet.md).

Debugging Twig:
  * [VSCode, XDebug, and Lando](https://docs.lando.dev/guides/lando-with-vscode.html)
  * [XDebug PHP.ini Settings](https://gist.github.com/MatthieuScarset/0c3860def9ff1f0b84e32f618c740655)
  * [Debug configuration](https://www.drupal.org/docs/develop/theming-drupal/twig-in-drupal/debugging-twig-templates)
  * [Inspecting variables](https://www.drupal.org/docs/develop/theming-drupal/twig-in-drupal/discovering-and-inspecting-variables-in-twig-templates)
  * Note: Twig Tweak provides a breakpoint Twig function method [`drupal_breakpoint()`](https://git.drupalcode.org/project/twig_tweak/-/blob/3.x/docs/cheat-sheet.md#drupal-breakpoint). Also, [`xdebug_break()`]() may be used in PHP code.
  * [Debugging Twig with XDebug](https://www.drupal.org/project/twig_xdebug)

#### Theme Rendering

### Back-End Development

You can enable verbose error logs displayed to the browser through [Drupal configuration](https://www.drupal.org/docs/develop/development-tools/enable-verbose-error-logging-for-better-backtracing-and-debugging).

__TODO__

### Multisite Architecture

Simply put a multisite architecture allows a single drupal installation to run multiple websites. How resources are shared (or not) depend on the setup. For example, you could have a single database server (i.e. appserver) for all the multisites. Drupal will also use codepaths specific to the a multisite instance in case it is running different modules.

## Additional Resources
* [Drupalize.me](https://drupalize.me/) – paid content with roles from core developer up to content editor and admins.