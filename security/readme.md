# Security Guidelines

## Table of Contents

1. [Third-Party Code](#third-party-code)
 * [Plugins](#plugins)
 * [Composer](#composer)
 * [Other](#other)
2. [Data Handling](#data-handling)
3. [Theme](#theme)

## Third-Party Code

All third-party code and libraries should be reviewed before inclusion:

1. Is the project actively maintained?
2. Does the project require additional dependencies?
3. Is the code clean and well-documented?
4. Are there known vulnerabilities, active and/or closed?

### Plugins

WordPress plugins can provide useful functionality and save development time, however they are also the main attack vector for WordPress-driven web sites.

1. All plugins must support automatic, lifetime updates. Do not install plugins from outside the main WordPress repository unless they hook into the updates API.
2. If licensing is required, contact the project administrator for approval. If a license is domain-specific, it must be purchased for both the staging and production URLs.
3. If a plugin is in the main WordPress repository, evaluate the support history, reviews, and release frequency.

### Composer

[Composer](https://getcomposer.org/) is the preferred method for including third-party PHP libraries and managing your own class-based code.

1. Be aware of a project's dependencies, which can quickly spawn out of control;
2. Make sure you are including an "official" source and not an out-of-date fork;
3. Specify a version where applicable, e.g. `3.1.*`;
4. Place Composer libraries in a "dot" folder to prevent direct exection, e.g. `thetheme/.lib/vendor`;
5. Clean up the content prior to committing or uploading; refer to the skeleton [Gruntfile.js](https://github.com/brightbrightgreat/skeleton/blob/master/wordpress/Gruntfile.js) for a helper;

### Other

1. Serve local copies of static assets like Javascript files whenever possible; do not link to external locations like a CDN or Github.
2. Any necessarily external scripts like `Analytics` should connect over HTTPS;

## Data Handling

1. **NEVER** trust user data. :)
2. Familiarize yourself with WordPress' [sanitizing and validation functions](https://codex.wordpress.org/Validating_Sanitizing_and_Escaping_User_Data), as well as those provided by [Tutan Common](https://github.com/Blobfolio/blob-common/blob/master/blob-common/docs/SANITIZE.md).
3. For historical reasons, WordPress provides its own implementation of "Magic Quotes". All `$_REQUEST` data will be backslashed upon receipt. You can use [stripslashes_deep()](https://developer.wordpress.org/reference/functions/stripslashes_deep/) to access the raw data, however you should always assign the stripped values to a new variable; never override a SUPERGLOBAL unless your code is going the last thing that will be run (e.g. inside an AJAX callback).
4. If a project requires handling uploads from unauthenticated users, please contact [josh@brightbrightgreat.com](mailto:josh@brightbrightgreat.com).
5. Use built-in WordPress functions for retrieving and filtering data. Do not interact directly with the database. If a project requires complex MySQL functionality, contact [josh@brightbrightgreat.com](mailto:josh@brightbrightgreat.com).

## Theme

A theme's PHP code should only ever be accessible through WordPress. A front-facing site should never link directly to a PHP script (for e.g. form handling). Each PHP script should include a quick check before any other executable code:

```php
if(!defined('ABSPATH')){ exit; }
```

This will prevent path disclosure vulnerabilities on improperly configured servers and avoid cluttering error logs with 500 errors.
