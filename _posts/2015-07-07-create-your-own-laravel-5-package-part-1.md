---
id: 229
title: 'Create your own Laravel 5 package &#8211; Part 1'
date: 2015-07-07T17:30:07+00:00
author: JejjE
layout: post
guid: http://jejje.net/?p=229
permalink: /create-your-own-laravel-5-package-part-1/
snap_isAutoPosted:
  - "1"
snap_MYURL:
  - ""
snapEdIT:
  - "1"
snapFB:
  - 's:365:"a:1:{i:0;a:12:{s:4:"doFB";s:1:"1";s:8:"postType";s:1:"A";s:10:"AttachPost";s:1:"2";s:10:"SNAPformat";s:23:"(%TITLE%) at %SITENAME%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:31:"376126219133781_868728323206899";s:5:"pDate";s:19:"2015-07-07 17:30:26";}}";'
dsq_thread_id:
  - "3912970463"
banner_image: /wp-content/uploads/2015/07/create_your_own_laravel_5_package_pt1.png
categories:
  - Coding
  - Laravel
  - PHP
tags:
  - code
  - development
  - laravel 5
  - php
---
Laravel is where it&#8217;s all at right now, there are many different PHP Frameworks out there that you can use to speed up your coding and not needing to reinvent the wheel for every project you make. If we&#8217;re following the **DRY** _(Don&#8217;t Repeat Yourself)_ principle we can create or use packages for common tasks we use a lot.
<!--more-->
## What are we making

We&#8217;re going to make a simple package that will return a user Gravatar or a link to the users profile, with the help of Facades we&#8217;ll be able to call it like _Gravatar::method()_. This is just a simple tutorial to get you started with your own package development.

### Contents

  1. [Create Laravel Project](#create-new-laravel-5-project)
  2. [Create our Gravatar package](#create-our-gravatar-package)
  3. [Add facade and configuration file](#add-facade-and-configuration-file) 
      1. [Create our Facade](#create-our-facade)
      2. [Setup a Configuration file](#setup-a-configuration-file)

<a href="https://github.com/jejje/gravatar" target="_blank" rel="nofollow">Check out the finished package on GitHub</a>

<a name="create-new-laravel-5-project"></a>

## Create new Laravel 5 project

Let&#8217;s begin with a fresh copy of Laravel, I assume you have everything setup like composer and laravel global.

<pre class="lang:default decode:true " title="Create a new laravel project">laravel new package-tutorial</pre>

When it has finished the installation we need to add our project into our homestead, open it up using **homestead edit**. And add the new project.

<pre class="lang:default decode:true " title="Add the site to Homestead.yml">- map: package-tutorial.dev
  to: /home/vagrant/Code/package-tutorial/public</pre>

When you&#8217;ve updated the homestead file you need to re-provision it with **homestead** **provision**, and add the new site into your **hosts** file. Great, now we have a clean install to work with! We will need a package called **workbench**, as I&#8217;m writing this you&#8217;ll need the _dev-master_ version since it&#8217;s the only one updated for Laravel 5.

<pre class="lang:default decode:true " title="Require workbench with composer">composer require xtwoend/workbench:dev-master --require-dev</pre>

You&#8217;ll also need to add it to your Service Providers in _app/config/app.php_.

<pre class="lang:default decode:true" title="Add Service Provider">Xtwoend\Workbench\WorkbenchServiceProvider::class,</pre>

Now we can see a new command if we run _php artisan_ called **workbench**, we can using this create a new package. We&#8217;ll need to publish the config file for workbench so that we may setup our author credentials.

<pre class="lang:default decode:true" title="Publish Workbench's config">php artisan vendor:publish</pre>

We can find the config file at _app/config/workbench.php_ and here you&#8217;ll enter your name and e-mail.

<a name="create-our-gravatar-package"></a>

## Create our Gravatar package

First off we&#8217;ll need to figure out what we&#8217;re going to name it, and the convention is to name the _vendor_ as your lastname or site-name. I use _jejje_ as my vendor name and we&#8217;re going to call the package _gravatar_, let&#8217;s generate the package with the **workbench** command.

<pre class="lang:default decode:true " title="Create our gravatar package">php artisan workbench jejje/gravatar</pre>

Now we just need to wait for the dependencies to be pulled in, it  won&#8217;t take long. When it&#8217;s finished you may find your newely generated package in _/workbench/jejje/gravatar_. You&#8217;ll find your package under the _src_ folder, and a Service Provider has been generated called **GravatarServiceProvider.php**. We can now add this to our Service Provider list.

**Oh, no!** We&#8217;re getting an error message that the class is not found! I had to Google around to figure out why I was getting this error message, and the solution was to add this to the _/bootstrap/autoload.php_.

<pre class="lang:default decode:true " title="Add to /bootstrap/autoload.php">/*
|--------------------------------------------------------------------------
| Register The Workbench Loaders
|--------------------------------------------------------------------------
|
| The Laravel workbench provides a convenient place to develop packages
| when working locally. However we will need to load in the Composer
| auto-load files for the packages so that these can be used here.
|
*/

if (is_dir($workbench = __DIR__.'/../workbench'))
{
    Xtwoend\Workbench\Starter::start($workbench);
}</pre>

<a name="add-facade-and-configuration-file"></a>

## Add facade and configuration file

We&#8217;ve now come so far that it is time to start coding and I think we should start with our Facade for easy access to our package methods like this **Gravatar::method()**.

<a name="create-our-facade"></a>

### Create our Facade

In our package folder _/workbench/jejje/gravatar/src/Jejje/Gravatar/_ we will add a PHP class that extends the Laravel Facade, we&#8217;ll name it Gravatar.

<pre class="lang:php decode:true" title="/workbench/jejje/gravatar/src/Jejje/Gravatar/Gravatar.php"><?php namespace Jejje\Gravatar;

use Illuminate\Support\Facades\Facade;

class Gravatar extends Facade {

    /**
     * Facade for our Gravatar Package
     * so that we may use it like
     * Gravatar::method();
     *
     * @return string
     */
    protected static function getFacadeAccessor() {
        return 'Jejje\Gravatar\Image';
    }

}</pre>

The _getFacadeAccessor_ binds the Facade to the PHP Class where all our logic will be stored and we&#8217;re going to name it **Image**, and we&#8217;ll do this in the next part of this tutorial since it&#8217;s going to be a long file with some nice methods. But just before we finish up I&#8217;d like to setup a configuration file that we&#8217;ll need in the main class.

<a name="setup-a-configuration-file"></a>

### Setup a Configuration file

It&#8217;s quite simple to make a configuration file where users can edit settings for our package, we&#8217;re not going to have many settings &#8211; we&#8217;re just doing it to get a light grasp on the concept. In our Gravatar folder create a folder called _config_ and a file within it called _config.php_.

<pre class="lang:default decode:true " title="/workbench/jejje/gravatar/src/Jejje/Gravatar/config/config.php"><?php

return [
    'default_gravatar_size' => 100
];</pre>

It&#8217;s a simple file that just returns an array as you can see, you can go as nuts as you like with settings and arrays within arrays if you need to. We need to register this in our **GravatarServiceProvider**.

<pre class="lang:default mark:22-27 decode:true"><?php namespace Jejje\Gravatar;

use Illuminate\Support\ServiceProvider;

class GravatarServiceProvider extends ServiceProvider {

	/**
	 * Indicates if loading of the provider is deferred.
	 *
	 * @var bool
	 */
	protected $defer = false;

	/**
	 * Register the service provider.
	 *
	 * @return void
	 */
	public function register()
	{
		//
        /**
         * This will publish the config file when you do vendor:publish
         */
        $this->publishes([
            __DIR__.'/config/config.php' => config_path('jejje/gravatar/config.php'),
        ]);
	}

	/**
	 * Get the services provided by the provider.
	 *
	 * @return array
	 */
	public function provides()
	{
		return [];
	}

}
</pre>

When you have updated your Service Provider you should run _vendor:publish_ so that the configuration file gets saved to your project config folder like this _/config/jejje/gravatar/config.php_. To finish up run;

<pre class="lang:default decode:true">php artisan vendor:publish</pre>

We&#8217;ve made great progress so far and I&#8217;ll see you in the next part of this series to add all our logic to make it work, and we&#8217;ll also look into how to publish our work.

&nbsp;

<div style="font-size:0px;height:0px;line-height:0px;margin:0;padding:0;clear:both">
</div>