---
id: 22
title: Set system path variable in Windows
date: 2015-03-01T17:55:49+00:00
author: JejjE
layout: post
guid: http://jejje.net/?p=22
permalink: /set-system-path-variable-in-windows/
dsq_thread_id:
  - "3839612529"
banner_image: /wp-content/uploads/2015/03/setting_system_variables_in_windows.png
categories:
  - Windows
tags:
  - command prompt
  - how-to
  - tutorial
  - windows
---
When you need to run some application from the Windows terminal, it&#8217;s not very often you need to do this but if you&#8217;re for example going to run a Java **.jar** file to start your Minecraft server, it can be convenient to tell Windows where your Java JRE is located and you do not need to reference it by path every time. Setting these system path variables is pretty much the same on all Windows machines and it&#8217;s easy if you know where to look. In this tutorial you will learn how to set a system path variable in Windows.
<!--more-->
## The quick way

Using shortcut key&#8217;s are a very convenient way of finding the right stuff quickly, and I&#8217;m a big fan of ease of access. We need to go to the **System** window, use these shortcuts to get there quickly.

**[Windows button] + [Pause]**

## The long way

Sometimes it can be a good idea to also know how to find it the hard way, especially if you forget the shortcut buttons &#8211; which is quite normal, since there are so many to keep track of, anyhow. Go to **Control Panel** -> **System and Security** -> **System**

[<img class="aligncenter size-full wp-image-31" src="https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/control_panel_system_and_security.png?resize=850%2C640" alt="control_panel_system_and_security" srcset="https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/control_panel_system_and_security.png?w=850 850w, https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/control_panel_system_and_security.png?resize=300%2C226 300w" sizes="(max-width: 850px) 100vw, 850px" data-recalc-dims="1" />](https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/control_panel_system_and_security.png)

When you&#8217;ve reached the **System** window either by using the shortcut or clicking the long way, you&#8217;ll see a screen looking something like this image below. As an administrator find and click on the **Advanced system settings**.

[<img class="aligncenter size-full wp-image-32" src="https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/system_window_screen.png?resize=850%2C640" alt="system_window_screen" srcset="https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/system_window_screen.png?w=850 850w, https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/system_window_screen.png?resize=300%2C226 300w" sizes="(max-width: 850px) 100vw, 850px" data-recalc-dims="1" />](https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/system_window_screen.png)

From the **System Properties** you&#8217;ll need to find and click the **Environment Variables** button.

[<img class="aligncenter size-full wp-image-27" src="https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/system_properties.png?resize=426%2C475" alt="system_properties" srcset="https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/system_properties.png?w=426 426w, https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/system_properties.png?resize=269%2C300 269w" sizes="(max-width: 426px) 100vw, 426px" data-recalc-dims="1" />](https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/system_properties.png)

If you do not have a **Path** variable as the image shows below, you just need to click the **New&#8230;** and name it **Path**, and if you do have one just select it and instead click the **Edit&#8230;** button.

[<img class="aligncenter size-full wp-image-26" src="https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/environment_variables.png?resize=426%2C475" alt="environment_variables" srcset="https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/environment_variables.png?w=426 426w, https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/environment_variables.png?resize=269%2C300 269w" sizes="(max-width: 426px) 100vw, 426px" data-recalc-dims="1" />](https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/environment_variables.png)

Most likely you will already have a path variable and it probably already have a lot of values. As you can see I have a few values in the path variable, these values are separated by a semi-colon &#8220;**;**&#8220;. So now let&#8217;s say you need to add Java to your path you&#8217;ll need to find where you&#8217;ve installed your Java, if I was a betting man the path you would need to add would be something like **C:\Program Files (x86)\Java\jre7\bin**. When you&#8217;ve added what was needed, just click your way out of it by clicking **OK**. And now you can open up your command prompt and use commands like **java -version** or whatever you need it for.

<div style="font-size:0px;height:0px;line-height:0px;margin:0;padding:0;clear:both">
</div>