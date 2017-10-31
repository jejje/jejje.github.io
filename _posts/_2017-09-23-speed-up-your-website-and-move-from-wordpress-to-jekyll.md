---
title: Speed up your website and move from Wordpress to Jekyll 
date: 2017-09-16T09:42:15+00:00
author: JejjE
layout: post

permalink: /speed-up-your-website-and-move-from-wordpress-to-jekyll/


banner_image: /wp-content/uploads/2017/09/speed-up-your-website.jpg
categories:
  - Online
tags:
  - website
  - how-to
---
Why not go back in time and use static simple HTML files again, speed up your website and move away from dynamically generated content such as how Wordpress functions. It might not be for everyone, but Jekyll is easy - and what loads faster than plain HTML?
<!--more-->

I’ve been using Wordpress for most of my projects since Wordpress emerged as a blogging platform. It has been great, it’s easy interface made management so simple. But Wordpress has now begun to be kind of bloated, and a high risk platform. Let’s go back to plain HTML instead!

## Why I made the switch from Wordpress to Jekyll
I’ve been hosting my Wordpress installs myself on a few VPS, because it gave me the freedom I needed - and sometimes it gave a nice speed boost. But recently I made the switch to a webhost because I got tired of all the extra work. And I was hoping that their extra servers would have better chaching and optimization than my servers I had spun up in the cloud.
But whatever I did, I could not trim off those extra seconds.

### The Loading Times
Wordpress has in some cases some insane loading times. This is due to the fact of all the plugins that inject code and make Wordpress by some design kind of messy. A lot of my long loading times was not because of my server, but because there was external JavaScript files that was loaded before all content was rendered.

This had been bothering me for quite some time. Two to five seconds of loading time, because of some injected JavaScript is unacceptable! 
I searched high and low to find which plugins added those extra annoying seconds, without much luck. 

### The Security
Being such a popular Content Management System have made Wordpress a big target for hackers and botnets. There are some great Security Plugins you can use that will block out some IP addresses and obscure the /wp-admin/ for extra security. But it’s still not enough.

### The Updates
Everything needs updating. The theme, the plugins and Wordpress itself needs it. With every update there is a slim chance something breaks - sigh. And if I we don’t update, we become vulnerable to attacks.

This is why I decided to give Jekyll a chance, a static HTML generator that is aware of complicated systems such as tags and categories, posts and pages. It is quite easy to get started if you’re familiar with some basics like the command line and git.

## How to export Wordpress and import it into Jekyll
The flow of Jekyll is to have files that it can read in either Markdown or HTML in a special file structure. And then you run jekylls serve command that starts the conversion process and launches a web server you can visit to see your website.

### Wordpress2Jekyll
If you already have a Wordpress site and you’d like to migrate to Jekyll. It is quite simple. Wordpress has a plugin that you install called Wordpress2Jekyll and then you find it and export it by simply clicking Tools -> Export to Jekyll and you will get a zip-file containing all of your posts, pages and images in Jekyll’s format.

You will probably take an extra look and clean up some posts and pages, depending on how many plugins you use. I had to go cleanup a few shortcodes to display YouTube videos and Contact forms for example.

### Get started with Jekyll
To get started you will need a few handy tools, and you’ll need to find the approrpiate version depending on your operation system. These programs are Git and Ruby Gem.

For Windows users you can try Git Bash if you have troubles getting it to work with Powershell or Cmd.

### Install Jekyll
Now that we have the tools needed, we can install Jekyll using these commands

https://jekyllrb.com/docs/windows/

```tcl
gem install jekyll bundler 
jekyll new my-awesome-site 
cd my-awesome-site 
bundle exec jekyll serve
```

Now browse to *http://localhost:4000* 

Now you can see the starter template for Jekyll, there are a few free templates you can use or you can buy one pretty cheap from http://themeforest.net. 

Now take all your files you got from the [Jekyll Exporter](https://sv.wordpress.org/plugins/jekyll-exporter/ "Wordpress plugin to export your blog to Jekyll format") export and place it into your newly created Jekyll site. There might be a few adjustments you need to make to get everything to work properly but it should be quite simple.

Now that we have jekyll installed we can also just enter a directory using the command line and use following command to serve and update on file changes.

```tcl
jekyll serve
```

Themes and tempaltes

### Get familiar with Github Pages
Using the free hosting service that Github has to offer is quite awesome! Github pages are easy to use and get started with, especially so with Jekyll. In my case I use the primary github pages that you create using yourname.github.io instead of branching off to a gh-pages which makes it even simpler for beginners.


Upload Project
When everything is as it should be, it’s time to upload it to github.
Custom Domain


## End Result
I couldn't be any happier about the end result. For sure I will miss the easy usablilty of Wordpress but I will not miss those **3 seconds loading times** which now has been reduced to as low as **0.73 seconds!**
JavScript redirect: https://stackoverflow.com/questions/8824141/how-to-redirect-from-one-url-to-another-url
