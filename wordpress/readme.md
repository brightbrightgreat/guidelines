# WordPress

## Table of Contents

1. [Enqueuing](#enqueuing)
2. [Hooks](#hooks-actions-and-filters)
3. [Media](#media)
4. [Plugins](#plugins)
5. [Custom Fields](#custom-fields)
6. [Custom Post Types & Taxonomy](#custom-post-types--taxonomy)
7. [Forms](#forms)
8. [Classes and PHP Dependencies](#classes-and-php-dependencies)
9. [Debugging](#debugging)
10. [Miscellaneous](#miscellaneous)
11. [Help](#help)

## Enqueuing
Enqueue scripts and styles through [`wp_enqueue_script()`](https://developer.wordpress.org/reference/functions/wp_enqueue_script/) and [`wp_enqueue_style()`](https://developer.wordpress.org/reference/functions/wp_enqueue_style/) rather than putting them directly in your templates.

WordPress has its own embedded versions of several third-party libraries like `jQuery`, which can be enqueued using the appropriate [handle](https://developer.wordpress.org/reference/functions/wp_enqueue_script/#defaults). If a WP version of a script exists, that version should be used instead of linking to a separate copy. Do **not** override or replace a native WP script as it can cause compatibility problems with plugins or future releases.

It is best practice to enqueue scripts at the end of the document, but if this is not possible due to to the nature of the code (e.g. `Analytics`, `AngularJS`, etc.), it is all right to place them inside the `<head>`.

See also [wp_add_inline_script()](https://developer.wordpress.org/reference/functions/wp_add_inline_script/) for enqueing blocks of code rather than external files.

## Hooks, Actions, and Filters
Take advantage of WordPress [hooks](https://codex.wordpress.org/Plugin_API#Hooks.2C_Actions_and_Filters) to abstract operations into your `functions.php` file rather than polluting your template files. 

A basic example (see below) is to use the [`wp_head`](https://codex.wordpress.org/Plugin_API/Action_Reference/wp_head) hook to add things like Google Analytics code. 

###### E X A M P L E
```php
function custom_google_analytics(){ ?>
  <script>
    (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)})(window,document,'script','//www.google-analytics.com/analytics.js','ga');
    ga('create', 'UA-XXXXXXX-1', 'auto');
    ga('send', 'pageview');
  </script>
<?php }
add_action('wp_head', 'custom_google_analytics');
```


## Media
We use Tutan Common JIT Image generation. Please familiarize yourself with some of the code consequences by [reading the documentation](https://github.com/Blobfolio/blob-common/blob/master/blob-common/docs/JIT.md).

**Never display the original size for an image.** Use thoughtful image sizes added through the [`add_image_size()`](https://developer.wordpress.org/reference/functions/add_image_size/) function and call them appropriately.

The new CSS property `object-fit` is a good responsive alternative to `background-image` for sections like page heroes. [blobject-fit](https://github.com/Blobfolio/blobject-fit) can be enqueued to provide a lightweight fallback for older browsers.

We use Tutan Common WebP functionality to generate WebP versions for browsers that support them. Use [`common_get_webp_srcset()`](https://github.com/Blobfolio/blob-common/blob/master/blob-common/docs/WEBP.md#common_get_webp_srcset) and [`common_get_webp_src()`](https://github.com/Blobfolio/blob-common/blob/master/blob-common/docs/WEBP.md#common_get_webp_src) to get your images.


## Plugins
Do not delete any of the plugins we have installed on staging. You can add others, but the ones we've added before giving you access must remain there. Please be judicious in your use of plugins.

You can refer to our list of recommended WordPress Plugins here: https://brightbrightgreat.com/2016/03/10/recommended-wordpress-plugins/

The security plugins will already be on staging. You do not have to use any or all of the others, but they’re a good place to start if you’re looking for something in particular. 

Tutan Common is used on all our sites, you can familiarize yourself with the variety of functions it includes [here](https://github.com/Blobfolio/blob-common)

## Custom Fields
Use ACF Pro for custom fields. We have a license and will set up the plugin for you.

When using ACF Pro to retrieve an image, please configure the field to return only the ID rather than the entire image object. This is less resource-intensive. 

Make use of the [ACF Clone](https://www.advancedcustomfields.com/resources/clone/) field functionality to make reusable components.

ACF Pro automatically generates a cache of its group and field structure located in `thetheme/acf-json`. Please download and commit these files with the rest of your project.

## Custom Post Types & Taxonomy
Do not use plugins for custom post types and custom taxonomies, instead code them manually using [`register_post_type()`](https://codex.wordpress.org/Function_Reference/register_post_type)  and [`register_taxonomy()`](https://codex.wordpress.org/Function_Reference/register_taxonomy) 

## Forms
Do not use Gravity Forms. We prefer [Formidable Forms](https://wordpress.org/plugins/formidable/) for security reasons.

### Contact Forms
1. Copies of submissions should be saved to the database and traversable via `wp-admin`. This provides a fallback in the event of email delivery issues.
2. The visitor's email address should not be used as the "From" address on the generated email. Certain mailserver configurations prohibit "email spoofing", which could cause such messages to fail. Note: this does not apply to the "Reply-To" mail header.
3. If functionality requires a custom form handler, all data must be properly sanitized and passed to [wp_mail()](https://developer.wordpress.org/reference/functions/wp_mail/) or [common_mail()](https://github.com/Blobfolio/blob-common/blob/master/blob-common/docs/EMAIL.md#common_mail) for sending plain text or HTML mail respectively. Do not use native PHP `mail()` or third-party libraries like `PHPMailer`.

## Classes and PHP Dependencies
All custom classes should be within the `bbg` namespace and conform to PSR-4 coding standards.

Use [Composer](https://getcomposer.org/) to manage both your class code and any third-party library dependencies. The vendor path should be `thetheme/.classes/vendor` and your custom classes `thetheme/.classes/bbg`.

Base configurations are included in the [skeleton](https://github.com/brightbrightgreat/skeleton/blob/master/wordpress/).

## Debugging
There will be a debug log on the staging site. Keep an eye on the debug log and address any notices and warnings generated by your code. 

Plugins can also generate items in the log. We do not expect you to fix problems in third-party code. However, if a plugin is generating an excessive amount, its use should be reconsidered.

## Miscellaneous
WordPress functions and features should be leveraged wherever possible:

1. Link URLs should never be hardcoded; use [get_permalink()](https://developer.wordpress.org/reference/functions/get_permalink/) (or a similar function specific to the page type) to fetch the correct URL;
2. The front-facing site should never link directly to a PHP script; use the [Rewrite API](https://codex.wordpress.org/Rewrite_API/add_rewrite_rule), [AJAX hooks](https://codex.wordpress.org/AJAX_in_Plugins), or bind the functionality to a specific page or post template.
3. Use [WP_Query](https://codex.wordpress.org/Class_Reference/WP_Query) and similar functions for retrieving content; if functionality is so specific as to require direct interaction with the database, please contact [josh@brightbrightgreat.com](mailto:josh@brightbrightgreat.com).

## Help

If you have any questions, please contact Tiffany Stoik ([tiffany@brightbrightgreat.com](mailto:tiffany@brightbrightgreat.com)).
