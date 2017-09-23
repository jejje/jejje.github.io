---
id: 249
title: 'Laravel 5 &#8211; Gravatar Package'
date: 2015-07-07T15:08:56+00:00
author: JejjE
layout: page
guid: http://jejje.net/?page_id=249
factory_shortcodes_assets:
  - 'a:0:{}'
image: /wp-content/uploads/2015/07/laravel_5_gravatar_package.png
---
As a part of an Tutorial series I wrote this basic Gravatar package for Laravel 5 just to show how one would go about making your own package from start to publishing it to Packagist. It only contains a few basic methods you can call, retrieving the URL to Gravatar with your e-mail hashed.

## Tutorial

  * [Create your own Laravel 5 package &#8211; Part 1]({{ site.baseurl }}/create-your-own-laravel-5-package-part-1/)
  * [Create your own Laravel 5 package &#8211; Part 2]({{ site.baseurl }}/create-your-own-laravel-5-package-part-2/)

##  Source and Packagist

  * <a href="https://github.com/jejje/gravatar" target="_blank" rel="nofollow">Jejje/Gravatar at GitHub</a>
  * <a href="https://packagist.org/packages/jejje/gravatar" target="_blank" rel="nofollow">Jejje/Gravatar at Packagist</a>

## Usage example

```php?start_inline=1
public function index() {
    $email = 'jejje@jejje.net';
    $size = 100; // Optional, you may set a default in the config file
    Gravatar::getImageWithLinkToProfile($email, $size);
}
```

