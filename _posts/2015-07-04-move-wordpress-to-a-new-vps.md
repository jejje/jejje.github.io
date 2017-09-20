---
id: 217
title: Move WordPress to a new VPS
date: 2015-07-04T17:31:41+00:00
author: JejjE
layout: post
guid: http://jejje.net/?p=217
permalink: /move-wordpress-to-a-new-vps/
snap_isAutoPosted:
  - "1"
snap_MYURL:
  - ""
snapEdIT:
  - "1"
snapFB:
  - 's:386:"a:1:{i:0;a:12:{s:4:"doFB";s:1:"1";s:8:"postType";s:1:"A";s:10:"AttachPost";s:1:"2";s:10:"SNAPformat";s:44:"%TITLE% at %SITENAME% using the Command Line";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:31:"376126219133781_866370253442706";s:5:"pDate";s:19:"2015-07-04 17:36:58";}}";'
dsq_thread_id:
  - "3904622035"
banner_image: /wp-content/uploads/2015/07/move_your_wordpress_to_a_new_vps_using_command_tools.png
categories:
  - Linux
tags:
  - command line
  - ubuntu
  - vps
  - wordpress
---
Sometimes a change of scenery is really good for you, sometimes it&#8217;s even true for your WordPress site. For example you want to move your website from a server located in Germany to one of your servers in the US for better connectivity for the American users. [I&#8217;m using DigitalOcean as my VPS provider]({{ site.baseurl }}/vps-self-hosted-at-digital-ocean/) and you have the option to take a snapshot and move the whole server, but in my case this was not what I wished to do, I wanted to move WordPress to a new server setup I just made, so in this tutorial I will walk you through how to backup your file contents and your database and migrate it to the new server, both servers being of the flavor <a href="http://releases.ubuntu.com/14.04/" target="_blank" rel="nofollow">Ubuntu 14.04 LTS</a>.
<!--more-->
## Move WordPress using SCP

We&#8217;re going to use a really neat tool called safe copy which you can use to securely copy files from one server to another. But before we begin we will make sure that everything is setup properly.

We have two servers named **test1.jejje.net** and **test2.jejje.net** and we need SSH access to both of them, let&#8217;s say we have a user with the username **jejje** on both servers for convince, and our files are located within our home directory _/home/jejje/public_html_. Great! Let&#8217;s begin by _gzipping_ our folder.

<pre class="lang:default decode:true " title="Pack the public_html to public_html.tar.gz">tar -zcvf public_html.tar.gz /public_html</pre>

Now when we&#8217;ve zipped our folder we can securely copy it onto **test2.jejje.net** from our server **test1.jejje.net**. Let&#8217;s assume we wish to move the files to the same folder but on the new server using the **SCP** tool that I mentioned.

<pre class="lang:default decode:true" title="Securely copy file from test1.jejje.net to test2.jejje.net">scp public_html.tar.gz jejje@test2.jejje.net:/home/jejje/</pre>

A password prompt will pop up and all you need to do is enter it and wait for the files to transfer, it won&#8217;t take long at all depending on the size of your website.

## Backup your WordPress database

For this step we need our MySQL credentials, let&#8217;s say they are as following; **jejje** and **password** &#8211; and the database we are going to use is named **wordpress**. We will want to save our database into a _.sql_ file and the name doesn&#8217;t matter so let&#8217;s just call it **dump.sql**, with all of these credentials we can now finally make a backup dump of our wordpress database with all it&#8217;s tables.

<pre class="lang:default decode:true ">mysqldump -ujejje -ppassword wordpress > dump.sql</pre>

This command will login to your MySQL account and dump the **wordpress** database into the textbased **dump.sql** file, great! With this file and the WordPress files we&#8217;ve already sent over, we&#8217;ll soon be up and running on our new server, but first we&#8217;ll need to use the _SCP_ command to send it to the new server. It&#8217;s pretty much the same as before.

<pre class="lang:default decode:true" title="Transfer the SQL-file to the new server">scp dump.sql jejje@test2.jejje.net:/home/jejje/</pre>

When the magic is done, you can now login into your second server, in our case the _test2.jejje.net_ server.

##  Restore WordPress on the new server

We now have two files in our _/home/jejje/_ on _test2.jejje.net_, we have the gzipped file with our WordPress files in it, we need to unpack it to the correct folder.

<pre class="lang:default decode:true" title="Unpack the files">tar -zxvf public_html.tar.gz</pre>

This will now unpack and there are only a few steps left to finish our restore of our WordPress migration, we&#8217;re still missing the database and we&#8217;ll get to that right now. I am assuming that you already have a database setup on your new server named **wordpress** just as the old one, alongside with a matching MySQL account for convenience_._

<pre class="lang:default decode:true " title="Populate your database from the dump.sql">mysql -ujejje -ppassword wordpress < dump.sql</pre>

If everything has gone as it is supposed to, which it _mostly_ does. You could now change your DNS settings to point to the new server and everything should work just as nothing has happened, we just have to wait for the DNS to propegate _(which I do hate, I know I shouldn&#8217;t but I do). _

## Rounding up

This way we&#8217;ve done it today is by far the simplest road to travel when we&#8217;re working with our own servers. This way prevents the issues that may occur if we had used an FTP and PhpMyAdmin as an example, I myself encountered that the files took ages to transfer on my slow Internet, and the PhpMyAdmin aspect of it often failed because of file upload limits. This was the case when I transfered a clients WordPress blog that had been posting on a dailiy/weekly basis with a ton of plugin data in the database. His _dump.sql_ file was actually more than **one gigabyte**, instead of the regular two to ten megabytes, and that&#8217;s when I figured this would be the most painless way to do it &#8211; and I highly recommend it.

One thing to mention though is that errors might occur if you decide to change your database name from **wordpress** to **wordpress_blog**, but it&#8217;s easier to change the name afterwards. I wish to the best of luck on your future WordPress setups!

<div style="font-size:0px;height:0px;line-height:0px;margin:0;padding:0;clear:both">
</div>