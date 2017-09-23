---
id: 55
title: How to make a batch file to start your Minecraft Bukkit server
date: 2015-03-02T13:00:49+00:00
author: JejjE
layout: post
guid: http://jejje.net/?p=55
permalink: /how-to-make-a-batch-file-to-start-your-minecraft-bukkit-server/
dsq_thread_id:
  - "3844613885"
banner_image: /wp-content/uploads/2015/03/make_a_batch_file_for_bukkit_server.png
categories:
  - Windows
tags:
  - batch
  - bukkit
  - minecraft
  - windows
---
When you&#8217;re going to start your local Bukkit server you will need to open up the command prompt, change directory to where your Minecraft server is located and then run a Java command with a few arguments. This is a really tedious process to do every time you need to start it. That&#8217;s why we should make a batch file named in the lines of **RUNME.bat** so that we with only one click can launch or server, but how do you make such a batch file? In this short article I&#8217;ll show you two great examples on how to make this easy file, it does not require more than two lines of code. To make a new batch file you simply open up notepad and save the file as **name.bat** and it will be a batch executable.
<!--more-->
## Making a batch file using a predefined Java path

If you&#8217;ve [set Java into your System path variables]({{ site.baseurl }}/set-system-path-variable-in-windows/ "Set system path variable in Windows"), which I give a walk through of, this will be the easiest batch file since it will not need the path to the Java, and it looks something like this:

```posh
java -Xmx1G -jar craftbukkit.jar -o true
PAUSE
```

The second flag **-Xmx1G** tells the system to give the Bukkit server 1Gb of RAM but you could also set it like **-Xmx1024M**, I usually give my server 2Gb of my 8Gb I have &#8211; but depending on how many plugins and how many players you have it can be a lot lower than that. Try it out and see what fits your needs!

## Making a batch file without defined Java path

If you&#8217;re unsure about how to set your System path variables, or you&#8217;ve had troubles doing it this few lines will make your life easier since this batch file will check for what system you are on x32- or x64-bit. And it will then run Java from the appropriate path, I would recommend you to read my guide on [how to setting System Variables]({{ site.baseurl }}/set-system-path-variable-in-windows/ "Set system path variable in Windows") to make it easier in the future.

```posh
@ECHO OFF
IF /I "%PROCESSOR_ARCHITECTURE:~-2%"=="64" "%ProgramFiles(x86)%\Java\jre7\bin\java.exe" -Xmx1024M -jar "craftbukkit.jar"
IF /I "%PROCESSOR_ARCHITECTURE:~-2%"=="86" "%ProgramFiles%\Java\jre7\bin\java.exe" -Xmx1024M -jar "craftbukkit.jar"
PAUSE
```

Hopefully this will help, but as I mentioned two times above &#8211; it&#8217;s always easier to define the path to Java in your System Variables, because then you may run any type of Java from the command line with ease.

