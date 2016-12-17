# WordPress

## Enqueuing
Enqueue scripts and styles through [`wp_enqueue_script()`](https://developer.wordpress.org/reference/functions/wp_enqueue_script/) and [`wp_enqueue_style()`](https://developer.wordpress.org/reference/functions/wp_enqueue_style/) rather than putting them directly in your templates. 

## Hooks
Take advantage of WordPress hooks to abstract operations into your `functions.php` file rather than polluting your template files. 

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

## jQuery
If jQuery is being used, please, use the version of jQuery that comes with WordPress rather than dequeueing the script and enqueuing a different version


## Media
We use Tutan Common JIT Image generation. Please familiarize yourself with some of the code consequences by [reading the documentation](https://github.com/Blobfolio/blob-common/blob/master/blob-common/docs/JIT.md).

**Never display the original size for an image.** Use thoughtful image sizes added through the [`add_image_size()`](https://developer.wordpress.org/reference/functions/add_image_size/) function and call them appropriately. 

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

## Custom Post Types & Taxonomy
Do not use plugins for custom post types and custom taxonomies, instead code them manually using [`register_post_type()`](https://codex.wordpress.org/Function_Reference/register_post_type)  and [`register_taxonomy()`](https://codex.wordpress.org/Function_Reference/register_taxonomy) 

## Forms
Do not use Gravity Forms. We prefer Formidable Forms for security reasons. 

## Debugging
There will be a debug log on the staging site. Keep an eye on the debug log and address any notices and warnings you control. 

Plugins can also generate items in the log. We do not expect you to fix problems in plugin code. However, if a plugin is generating an excessive amount, its use should be reconsidered.


