---
title: PHP on Pantheon
subtitle: Debug Intermittent PHP 7 Notices
description: Debug and fix Deprecated Constructor notices in your Pantheon site.
contenttype: [guide]
innav: [false]
categories: [php]
cms: [--]
audience: [development]
product: [--]
integration: [--]
tags: [code]
contributors: [greg-1-anderson]
layout: guide
showtoc: true
permalink: docs/guides/php/deprecated-constructor-notices
anchorid: deprecated-constructor-notices
---

This section provides information on how to debug intermittent PHP 7 notices.

PHP notices are usually handled automatically by the Pantheon platform as described in [PHP Errors and Exceptions](/guides/php/php-errors). However, a PHP notice might occasionally be emitted directly into the web page content.

An example notice might look like this:

```none
Deprecated: Methods with the same name as their class will not be constructors in a future version of PHP; views_display has a deprecated constructor in /srv/bindings/46027a30ca4c4980a7188036eb2fcea5/code/sites/all/modules/views/includes/view.inc on line 2553
Deprecated: Methods with the same name as their class will not be constructors in a future version of PHP; views_many_to_one_helper has a deprecated constructor in /srv/bindings/46027a30ca4c4980a7188036eb2fcea5/code/sites/all/modules/views/includes/handlers.inc on line 753
```

An error like will usually only appear intermittently. Most page loads will come up correctly until, after a period of inactivity on the site, the same message will appear again.

## Cause and Remediation

This error is caused by a combination of two factors:

- PHP notices generated during source code parsing
- [PHP OPcache](https://www.php.net/manual/en/book.opcache.php) is in use

Convert your class constructor to `__construct()` to fix these errors. Refer to [deprecation notice for PHP-4-style constructors](https://secure.php.net/manual/en/migration70.deprecated.php#migration70.deprecated.php4-constructors) for more information.

## Finding PHP Files Containing Parse-Time Notices

**Temporarily** disable the OPcache in your `settings.php` file to make it easier to find and debug intermittent notices:

```php
if (!isset($_ENV['PANTHEON_ENVIRONMENT']) || ($_ENV['PANTHEON_ENVIRONMENT'] != 'live'))
{
    ini_set("opcache.enable", 0);
}
```

<Alert title="Warning" type="danger">

Disabling OPcache has a sever impact on performance, so care should be taken not to do this on a production system. Note that `display_errors` is set to `off` on Pantheon Live environments, so there is no need to disable OPcache in production. Make sure to re-enable OPcache after you are done debugging if you disable it in Dev and Multidev environments.

</Alert>

You can also search for deprecated constructors using the PHP linter on the command line. You must have PHP 7.0 to be installed locally to follow the steps below.

1. Create a local copy of your site as described in [Local Development](/guides/local-development).

1. Run the command below:

    ```bash{outputLines: 2-7}
    php -l sites/all/modules/views/includes/handlers.inc
    PHP Deprecated:  Methods with the same name as their class will not be constructors in a future version of PHP; views_many_to_one_helper has a deprecated constructor in sites/all/modules/views/includes/handlers.inc on line 753

    Deprecated: Methods with the same name as their class will not be constructors in a future version of PHP; views_many_to_one_helper has a deprecated constructor in sites/all/modules/views/includes/handlers.inc on line 753

    No syntax errors detected in sites/all/modules/views/includes/handlers.inc
    ```

1. Replace the path to the file you would like to check. Run the command below to check every .php, .inc and .module file in a Drupal site:

    ```bash{promptUser: user}
    find -E . -iregex ".*\.(inc|php|module)$" -exec php -l {} \; | grep -v 'No syntax errors'
    ```

1. Adjust the regular expression as needed to scan other file extensions that may contain php code.

## Explanation

[Deprecation notices for deprecated constructors](https://secure.php.net/manual/en/migration70.deprecated.php#migration70.deprecated.php4-constructors) are emitted if a class contains a method with the same name as the class name. This was the recommended way to declare class constructors in PHP 4, but it was not until PHP 7 that this form actually started producing a notice. At this time, the PHP-4-style constructor is the only deprecation notice that is reported during source code parsing. In theory, this structure should only be encountered in very old code; in practice, though, some projects may have continued using the deprecated form, so it may be encountered from time to time.

OPcache is always enabled on Pantheon. When OPcache is in use, PHP will print any notice emitted during source code processing directly to the standard output, ignoring any error handler that may be set. These notices may still be disabled by setting `error_reporting` to ignore E_DEPRECATED; however, Drupal always enables E_DEPRECATED in `error_reporting` early in its bootstrap process, so these notices will be printed if `display_errors` is set to `on`.

OPcache also influences when this error is displayed. Since OPcache caches the compiled form (opcodes) of the PHP that is being executed, the deprecation notices will not be printed when the PHP opcodes are fetched from the OPcache. This is what leads to the intermittent nature of this problem.

<Alert title="Note" type="info">

The deprecation notices used in the examples on this page appeared in an old version of the Drupal [views](https://www.drupal.org/project/views) module for Drupal 7.x. This was fixed in issue [#2579819](https://www.drupal.org/node/2579819), and included in the [7.x-3.12](https://www.drupal.org/project/views/releases/7.x-3.12) release.

</Alert>

## More Resources

- [PHP Errors and Exceptions](/guides/php/php-errors)

- [PHP Slow Log](/guides/php/php-slow-log)

- [Enable OPcache](/guides/frontend-performance/caching#enable-opcache)
