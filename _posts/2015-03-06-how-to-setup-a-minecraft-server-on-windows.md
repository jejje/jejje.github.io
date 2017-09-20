---
id: 13
title: How to setup a Minecraft server on Windows
date: 2015-03-06T09:24:36+00:00
author: JejjE
layout: post
guid: http://jejje.net/?p=13
permalink: /how-to-setup-a-minecraft-server-on-windows/
dsq_thread_id:
  - "3839616663"
banner_image: /wp-content/uploads/2015/03/setup_a_minecraft_server_on_windows.png
categories:
  - Gaming
  - Minecraft
tags:
  - bukkit
  - minecraft
  - spigotmc
  - windows
---
The sandbox game Minecraft is quite a popular game and there are many servers that you can join and play on, but what if you and your friends just wanna play together and build something amazing? Then one of these big servers might not be the place for you and your friends, luckily it&#8217;s really easy to setup your own server at home <a title="Bukkit Official homepage" href="http://bukkit.org" target="_blank" rel="nofollow">using something called Bukkit</a> &#8211; this is a snippet from their website.
<!--more-->
> Bukkit is an up-and-coming Minecraft Server mod that will completely change how running and modifying a Minecraft server is done &#8211; making managing and creating servers easier and providing more flexibility.

Bukkit is easy to get started with, and has amazingly **13,249** plugins as of  2015-03-01, you can even easily make your own plugins if you have some basic Java knowledge, but that&#8217;s out of this tutorials scope and we&#8217;re going to focus on setting up the server. In this article I will walk you through all the steps to setup a Minecraft server on Windows, all the way from getting the files needed to logging in to the server.

## What you&#8217;ll need to get started

Minecraft is as you might know written in Java and you&#8217;ll need it to play Minecraft and also to run the server.** ** You&#8217;ll also need to setup a path to your Java if you&#8217;ve not done it, don&#8217;t worry it&#8217;s easy and you can read my tutorial on how to set system path variables. You&#8217;ll also need Git for windows, this is only needed to build the necessary files you&#8217;ll need. To sum up you&#8217;ll need to complete these following things before we can really get started.

### Download Java

Go to <a title="Download Java" href="https://java.com/en/download/" target="_blank" rel="nofollow">Java&#8217;s official homepage and download</a> and install it by following the easy instructions.

### Setup System Path variables

This step is not required, but it will make it a lot easier to get started, just <a title="Set system path variable in Windows" href="http://jejje.net/set-system-path-variable-in-windows/" target="_blank">follow my tutorial on how to setup System Path Variables in Windows</a>, it only takes about a minute to complete.

### Install Git for Windows

You will need to have git on Windows for using the Bukkits build tool, you do not need after you&#8217;ve initialized the tool for building the structure, I will explain further down this article &#8211; and everything will make sense. <a title="Download Git for Windows" href="http://msysgit.github.io/" target="_blank" rel="nofollow">Download Git for Windows here</a>, and just follow the instructions.

## Download Bukkit/SpigotMC build tool

In the autumn of 2014 there was a lot of confusion going around <a title="Bukkit DCMA - what's going on" href="https://bukkit.org/threads/bukkit-dmca-whats-going-on.309372/" target="_blank" rel="nofollow">because of rights disputes</a> and currently you will have to download Bukkit via SpigotMC which is the same as Bukkit with some custom hooks for developers, but don&#8217;t worry! Plugins will work on both Bukkit and SpigotMC &#8211; and you actually get both **craftbukkit** and **spigotmc** when you download the build tools I mentioned above. This tool will when run download the the latest files and build the structure you need using git, and that is why you need to have Git for Windows installed. Everything I&#8217;m talking about now you can <a title="Read more about Spigots Build Tool" href="http://www.spigotmc.org/wiki/buildtools/" target="_blank" rel="nofollow">read more about on Spigot&#8217;s Wiki about Build Tools here</a>.

Now begin by <a title="Download the latest BuildTool for Bukkit/Spigot" href="https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar" target="_blank" rel="nofollow">downloading the build tool</a> and place it in a folder where you wish to download and build &#8211; you will need to move the craftbukkit file into your desired Minecraft server folder later on, right click in the folder and select **Git Bash** as the image below shows.

[<img class="aligncenter size-full wp-image-69" src="https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/open_git_bash_to_begin_the_installation.png?resize=763%2C692" alt="open_git_bash_to_begin_the_installation" srcset="https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/open_git_bash_to_begin_the_installation.png?w=763 763w, https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/open_git_bash_to_begin_the_installation.png?resize=300%2C272 300w" sizes="(max-width: 763px) 100vw, 763px" data-recalc-dims="1" />](https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/open_git_bash_to_begin_the_installation.png)

This will open the Git Bash command prompt with the location of the build tool, so it&#8217;s as easy as it can be. Well then, now it&#8217;s time to start building with this tool and you start by entering this in the command prompt, **java -jar BuildTools.jar** just as the image below shows.

[<img class="aligncenter size-full wp-image-70" src="https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/time_to_build_the_structure_with_this_command.png?resize=677%2C343" alt="time_to_build_the_structure_with_this_command" srcset="https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/time_to_build_the_structure_with_this_command.png?w=677 677w, https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/time_to_build_the_structure_with_this_command.png?resize=300%2C152 300w" sizes="(max-width: 677px) 100vw, 677px" data-recalc-dims="1" />](https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/time_to_build_the_structure_with_this_command.png)This will start the process of downloading the files that you need, at this point I would suggest you to go grab a cup of coffee or tea since this will take about 15 minutes of downloading, unpacking and setting up everything it needs &#8211; just enjoy the magic!  When everything is done you can see all the magic that the build tool has setup for you.

## Setting up our Bukkit or SpigotMC server

To start of with a clean folder structure for our server, you will need to choose if you want Bukkit or SpigotMC as your server &#8211; if you&#8217;re unsure just pick the Bukkit jar-file. Copy the **jar file** and the **eula.txt** file into the new folder you&#8217;ve chosen to be the Minecraft server location.

[<img class="aligncenter size-full wp-image-76" src="https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/clean_server_folder.png?resize=767%2C428" alt="clean_server_folder" srcset="https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/clean_server_folder.png?w=767 767w, https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/clean_server_folder.png?resize=300%2C167 300w" sizes="(max-width: 767px) 100vw, 767px" data-recalc-dims="1" />](https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/clean_server_folder.png)

Now is a good time to [make a batch file that will run the Java command to start your server]({{ site.baseurl }}/how-to-make-a-batch-file-to-start-your-minecraft-bukkit-server/ "How to make a batch file to start your Minecraft Bukkit server"). Before we can actually setup the basic server settings we need to run our **RUNME.bat** we created, and Bukkit will install the rest of the files needed for our server. The code snippet below is what you need to save into your **RUNME.bat** using notepad.

<pre>java -Xmx2G -jar craftbukkit-1.8.jar -o true
PAUSE
</pre>

But right before we can actually run this batch file, we need to <a title="Read the Minecraft EULA" href="https://account.mojang.com/documents/minecraft_eula" target="_blank" rel="nofollow">read the EULA (End User License Agreement)</a> before accepting it, when you&#8217;ve read the EULA and you agree to it&#8217;s terms you just open up the EULA.txt in our server folder and change the boolean value from **false** to **true**. Now when you&#8217;ve saved the file you can run our **RUNME.bat **and as you can see a lot new files have been put into your folder _(Sidenote: When I did this during the tutorial, I got a stacktrace error &#8211; but everything still works, if you also get an stacktrace, ignore it and it will disapear the next time you start)_. When it&#8217;s finished just enter **stop** into the console to give it a graceful shutdown.

[<img class="aligncenter size-full wp-image-78" src="https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/clean_server_folder_first_bukkit_run.png?resize=767%2C563" alt="clean_server_folder_first_bukkit_run" srcset="https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/clean_server_folder_first_bukkit_run.png?w=767 767w, https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/clean_server_folder_first_bukkit_run.png?resize=300%2C220 300w" sizes="(max-width: 767px) 100vw, 767px" data-recalc-dims="1" />](https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/clean_server_folder_first_bukkit_run.png)

We&#8217;re actually already done and your friends can join as long as the server is up, but I always do a few settings before I give my IP to my friends. These are not required but it&#8217;s always good to look through a settings file before you open it up to others so that you don&#8217;t need to restart because you in hindsight remembered that you should have done.

<pre>level-seed=<some cool seed>
difficulty=3
enable-command-block=true
max-players=10
motd=JejjE's network
</pre>

Usually I find a cool seed unless I actually like the random generated one, <a title="Google Minecraft seeds" href="https://www.google.se/?q=minecraft+seed" target="_blank" rel="nofollow">a quick Google search</a> will help you find some cool ones. I personally also find that **Easy** in Minecraft is too easy and I always change it to **Hard** by setting _difficulty=3_ but you can always change this later if you find it too hard or easy. Lastly I set the MOTD to the name of my server so that my friends can easily see that it&#8217;s the right server.

## Time to play some Minecraft

Now when everything in the **server.properties** file it&#8217;s time to login to it and test so that everything works. If you like the vanilla Minecraft as it is, nothing more is needed at this point. But I would recommend you to [read my article about the plugins every server needs]({{ site.baseurl }}/6-minecraft-bukkit-plugins-your-server-cannot-be-without/ "6 Minecraft Bukkit plugins your server cannot be without") and see if any of them seems like something you want on your server. If your friends is not in your local lan, don&#8217;t forget to open up the port **25565** and forward it to your computer. In the image below you can see that everything seems to work, and I even found a pretty nice spot to start out with, wood, sand and a cow &#8211; a cow that will become food pretty soon.

[<img class="aligncenter size-full wp-image-81" src="https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/2015-03-02_18.31.45.png?resize=854%2C480" alt="2015-03-02_18.31.45" srcset="https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/2015-03-02_18.31.45.png?w=854 854w, https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/2015-03-02_18.31.45.png?resize=300%2C169 300w" sizes="(max-width: 854px) 100vw, 854px" data-recalc-dims="1" />](https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/2015-03-02_18.31.45.png)

<div style="font-size:0px;height:0px;line-height:0px;margin:0;padding:0;clear:both">
</div>