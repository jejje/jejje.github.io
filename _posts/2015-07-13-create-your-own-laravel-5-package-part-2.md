---
id: 244
title: 'Create your own Laravel 5 package &#8211; Part 2'
date: 2015-07-13T12:09:08+00:00
author: JejjE
layout: post
guid: http://jejje.net/?p=244
permalink: /create-your-own-laravel-5-package-part-2/
factory_shortcodes_assets:
  - 'a:0:{}'
snap_isAutoPosted:
  - "1"
snap_MYURL:
  - ""
snapEdIT:
  - "1"
snapFB:
  - 's:363:"a:1:{i:0;a:12:{s:4:"doFB";s:1:"1";s:8:"postType";s:1:"A";s:10:"AttachPost";s:1:"2";s:10:"SNAPformat";s:21:"%TITLE% at %SITENAME%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:31:"376126219133781_872240816188983";s:5:"pDate";s:19:"2015-07-13 12:09:32";}}";'
dsq_thread_id:
  - "5921593589"
banner_image: /wp-content/uploads/2015/07/create_your_own_laravel_5_package_pt2.png
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
In a previous article we begun to look into developing our own simple package for Laravel 5 and in this article we will continue where we left off and finish our little Gravatar package, to begin we&#8217;ll summarize what we&#8217;ve done so far in [Create your own Laravel 5 package Part 1](http://jejje.net/create-your-own-laravel-5-package-part-1/).
<!--more-->
  * [Created our Laravel 5 project](http://jejje.net/create-your-own-laravel-5-package-part-1/#create-new-laravel-5-project)
  * [Created our Gravatar package](http://jejje.net/create-your-own-laravel-5-package-part-1/#create-our-gravatar-package)
  * [Created our Facade and Configuration file](http://jejje.net/create-your-own-laravel-5-package-part-1/#add-facade-and-configuration-file)

Great, we&#8217;re now up to speed on our package development, and it&#8217;s finally time for the best part &#8211; the actual coding! Remember that this package is a simple tutorial and it could really need some improvement, and <a href="https://github.com/jejje/gravatar" target="_blank" rel="nofollow">feel free to fork my project</a> and update me on your improvements!

## Contents

  1. [Finishing up our Laravel package](#finishing-up-our-laravel-package)
  2. [Prepare to publish our package](#prepare-to-publish-our-package) 
      1. [Update the package composer.json](#update-the-package-composer-json)
      2. [Create a README file](#create-a-readme-file)
      3. [Upload to GitHub](#upload-to-github)
      4. [Register and Upload on Packagist](#register-and-upload-on-packagist)
  3. [Conclusion](#conclusion)

<a href="https://github.com/jejje/gravatar" target="_blank" rel="nofollow">Check out the Github Page if you&#8217;re impatient</a>

<a name="finishing-up-our-laravel-package"></a>

## Finishing up our Laravel package

As a refresher we made our Facade and linked it to a file that we have not yet created, the PHP class **Image** and we know we&#8217;re going to need the **Config** facade from Laravel 5. Keep in mind that I&#8217;m going to break up this file into sections, we&#8217;ll begin with the first method of the file.

<pre>
<?php namespace Jejje\Gravatar;

use Illuminate\Support\Facades\Config;

/**
 * Class Image
 *
 * @package Jejje\Gravatar
 */
class Image {

    /**
     * Get the global size if none is passed as argument
     *
     * Don't forget to vendor:publish
     * @return int
     */
    public function getGlobalSize()
    {
        $size = Config::get('jejje.gravatar.config.default_gravatar_size');

        return $size;
    }

 </pre>

Here we&#8217;re making use of our configuration file we made in the previous article, we only have one setting and it&#8217;s the _default\_gravatar\_size_ which we set to _100_ if we do not supply and override it as a second argument.

<pre>
/**
     * Method to reuse the Gravatar image url
     *
     * @param $id
     * @param $size
     * @return string
     */
    private function gravatarImage($id, $size)
    {
        return "http://www.gravatar.com/avatar/$id?s=$size";
    }

    /**
     * Method to reuse Gravatar profile url
     *
     * @param $id
     * @return string
     */
    private function gravatarProfile($id)
    {
        return "http://www.gravatar.com/$id";
    }
 </pre>   

These methods is only used as an part of easy access of the Gravatar url depending if we need the avatar or the profile. These methods are private and is not accessible via the Facade.

<pre>
/**
     * This method is used to retrive url to users Gravatar
     * Will use default size from config file unless size
     * argument is passed.
     *
     * @param $email
     * @param null $size
     * @return string
     */
    public function getImageUrl($email, $size = null)
    {
        if(is_null($size))
        {
            $size = $this->getGlobalSize();
        }

        $gravatar_hash = $this->getHash($email);

        return $this->gravatarImage($gravatar_hash, $size);
    }
 </pre>

This is one of the main methods that we would be using, it takes two parameters the email of the user which is required and the optional size argument. As you can see if the none is provided, we&#8217;ll fetch it from our **getGlobalSize()** which get it from the config file. But wait a minute, there&#8217;s one method used here that we don&#8217;t have &#8211; yes, we do not have it just yet, we&#8217;ll get there.

<pre>
/**
     * Will return url to requested user Gravatar.
     *
     * @param $email
     * @return string
     */
    public function getProfileUrl($email)
    {
        $gravatar_hash = $this->getHash($email);

        return $this->gravatarProfile($gravatar_hash);
    }
 </pre>

This just returns the URL of the users profile, no particular magic here, and we could expand this method to actually return a tiny hCard &#8211; but it&#8217;s out of the scope of this package and tutorial.

<pre>
    /**
     * Will return a Gravatar image with link
     * to profile of the requested user.
     *
     * @param $email
     * @param null $size
     * @return string
     */
    public function getImageWithLinkToProfile($email, $size = null)
    {
        if(is_null($size))
        {
            $size = $this->getGlobalSize();
        }

        $gravatar_hash = $this->getHash($email);

        $image = $this->gravatarImage($gravatar_hash, $size);
        $link = $this->gravatarProfile($gravatar_hash);

        $image_with_link = "<a href='$link'><img src='$image'></a>";

        return $image_with_link;
    }
 </pre>

This nifty method returns an image of the user with a link to their profile, this method could also get the second argument just as the **getImageUrl** can, but this actually returns the HTML for the image as well.

<pre>

    /**
     * Returns the hash of an e-mail trimmed
     * if there was any spaces in the submitted
     * e-mail.
     *
     * @param $email
     * @return string
     */
    public function getHash($email)
    {
        $gravatar_hash = md5(strtolower(trim($email)));

        return $gravatar_hash;
    }



 </pre>

This is the last part of our **Image** class, and as I mentioned before, it gets the Hashed version of the users e-mail. We&#8217;re not to far from the finish line, of course we could add lots of more features, tests and so much more but I won&#8217;t deprive you of that.

<a name="prepare-to-publish-our-package"></a>

## Prepare to publish our package

We&#8217;ve tried our package out, and it works _(hopefully)_ and we now plan to publish our Laravel 5 package for others to use and enjoy, or even for personal use in our next project! So what more do we need to do? Let&#8217;s make a list to make sure we don&#8217;t miss anything.

  1. Update our composer.json with information about our package
  2. Add a README.md file
  3. Upload it to GitHub
  4. Publish it to Packagist

<a name="update-the-package-composer-json"></a>

### Update the package composer.json

Workbench did all of the heavy lifting for us but we need to enter more information if we&#8217;re going to publish our Gravatar package.

<pre>
<pre><code>
{

    "name": "jejje/gravatar",
    "description": "A very simple package to get a Gravatar image or Profile. Made for education purposes for http://jejje.net",
    "license": "MIT",
    "homepage": "http://jejje.net/php/laravel-5-gravatar-package/",
    "authors": [
        {
            "name": "Jimmy JejjE Nelsing",
            "email": "jimmy.nelsing@gmail.com",
            "homepage": "http://jejje.net",
            "role": "developer"
        }
    ],
    "require": {
        "php": ">=5.4.0",
        "illuminate/support": "5.1.*"
    },
    "require-dev": {

    },
    "autoload": {
        "psr-4": {
            "Jejje\\Gravatar\\": "src/Jejje/Gravatar"
        }

    },
    "minimum-stability": "dev"

}
</code></pre>
</pre>

I&#8217;ve added a description of our little package, license and homepage for our package and not to forget &#8211; more information about me, what role and website I have.

<a name="create-a-readme-file"></a>

### Create a README file

The convention for readme files is to use Markdown, which is a simple way to add html to a readme with _markdown_ syntax. These files has a few requirements, you need to inform people on how to install it and how to use it, and we&#8217;ll add this to the root of our package.

<a name="upload-to-github"></a>

### Upload to Github

Create your repository at Github, I&#8217;ve created it and I called it like our package **Gravatar**.

[<img class="aligncenter size-full wp-image-251" src="https://i0.wp.com/jejje.net/wp-content/uploads/2015/07/upload_our_package_to_github.png?resize=722%2C475" alt="Create our Github repository to upload our package to" srcset="https://i2.wp.com/jejje.net/wp-content/uploads/2015/07/upload_our_package_to_github.png?w=722 722w, https://i1.wp.com/jejje.net/wp-content/uploads/2015/07/upload_our_package_to_github.png?resize=300%2C197 300w" sizes="(max-width: 722px) 100vw, 722px" data-recalc-dims="1" />](https://i0.wp.com/jejje.net/wp-content/uploads/2015/07/upload_our_package_to_github.png)

Time to do a git init, which we usually do at the beginning of our package but since this is such a small package I decided to do it at the same time as I&#8217;m writing this article.

<pre class="lang:default decode:true ">git init

git remote add origin https://github.com/jejje/gravatar.git

git add .

git commit -m "First commit"

git push -u origin master </pre>

If you didn&#8217;t encounter any errors, great! I did encounter a few, but a few Google searches fixed that just as usual.

<a name="register-on-packagist-and-upload"></a>

### Register on Packagist and upload

If you haven&#8217;t already, <a href="https://packagist.org/" target="_blank" rel="nofollow">register on Packagist</a> so that we may upload our fresh package for others to use. When and if you&#8217;ve registered it&#8217;s simple to add the package, just add the github url for your package.

<img class="aligncenter size-full wp-image-252" src="https://i2.wp.com/jejje.net/wp-content/uploads/2015/07/package_at_packagist.png?resize=879%2C389" alt="Our package is now up at packagist for others to use, congratulations!" srcset="https://i1.wp.com/jejje.net/wp-content/uploads/2015/07/package_at_packagist.png?w=879 879w, https://i0.wp.com/jejje.net/wp-content/uploads/2015/07/package_at_packagist.png?resize=300%2C133 300w" sizes="(max-width: 879px) 100vw, 879px" data-recalc-dims="1" />

As you can see on this image, Packagist also suggest that we enable auto update &#8211; which is really nice. All you have to do is get the key when clicking the link GitHub Service hook, go into your GitHub settings panel and enter Packagist under the _Webhooks & Services_ tab.

<a name="conclusion"></a>

## Conclusion

Congratulations, you&#8217;ve now made your very own package for Laravel 5 from start to publish. I hope that you&#8217;ve learned something new, and will keep on learning and contribute to the PHP community &#8211; and if you do, feel free to leave a comment and show me!

&nbsp;

<div style="font-size:0px;height:0px;line-height:0px;margin:0;padding:0;clear:both">
</div>