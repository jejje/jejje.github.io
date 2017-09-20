---
id: 135
title: Setup IntelliJ IDEA for Bukkit plugin development
date: 2015-03-12T20:44:43+00:00
author: JejjE
layout: post
guid: http://jejje.net/?p=135
permalink: /setup-intellij-idea-for-bukkit-plugin-development/
dsq_thread_id:
  - "3839612298"
banner_image: /wp-content/uploads/2015/03/setup_intellij_for_bukkit_plugin_development.png
categories:
  - Bukkit
  - Coding
  - Java
  - Minecraft
tags:
  - bukkit
  - IDE
  - java
  - jetbrains
---
There are a few really good texteditors out on the Internet for developing, and when programming you really need one that you like &#8211; since you&#8217;re going to stare at it quite a bit. When programming in a language like Java that is Object Oriented a good IDE is a lot help, it&#8217;s not a requirement but it sure helps. My favorite IDE for Java development is **IntelliJ IDEA**, there are a few other popular ones out there like Eclipse for example, but I really prefer IntelliJ.
<!--more-->
## Setup IntelliJ for Bukkit

It&#8217;s a bit different to start up a Bukkit plugin environment if you&#8217;re used to Eclipse for example, I&#8217;ll do my best to walk you through the process. Begin by making a new **Empty Project**. The project is where you will house all of your Bukkit plugins, or modules as it is called in IntelliJ.

[<img class="aligncenter size-full wp-image-137" src="https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/new_blank_project.png?resize=776%2C731" alt="Make a new blank Project" srcset="https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/new_blank_project.png?w=776 776w, https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/new_blank_project.png?resize=300%2C283 300w" sizes="(max-width: 776px) 100vw, 776px" data-recalc-dims="1" />](https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/new_blank_project.png)

As I briefly mentioned above, projects in IntelliJ is not quite as you&#8217;d think they are, they are actually more of the collection of your Plugins. I named my Project **Tutorials**, because in this project I will house all of my Tutorial plugins. Now it&#8217;s time to make a new **Module** which what a plugin actually is, a Java module. Click **File > New Module** choose to make a new Java Module. _(You could actually choose to make a Maven Module from the beginning, but I&#8217;m going to walk you through the long way.)_ Now it&#8217;s time to name our plugin, for this Tutorial I&#8217;ve decided to name it **SetupIntellijForBukkit**, quite fitting right?

[<img class="aligncenter size-full wp-image-138" src="https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/module_is_plugin.png?resize=772%2C459" alt="module_is_plugin" srcset="https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/module_is_plugin.png?w=772 772w, https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/module_is_plugin.png?resize=300%2C178 300w" sizes="(max-width: 772px) 100vw, 772px" data-recalc-dims="1" />](https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/module_is_plugin.png)

Our plugin needs to be within a package, I&#8217;m sure you&#8217;re familar with this but do not worry if you&#8217;re not, and we need to follow a <a title="Naming Java Packages" href="http://docs.oracle.com/javase/tutorial/java/package/namingpkgs.html" target="_blank" rel="nofollow">specific naming convention that Java uses</a>, you can use your GitHub or even your e-mail if you do not have your own domain. Most important is to have a unique name in all lower case and the name of your plugin appended at the end. That&#8217;s is why I named the package to **net.jejje.java.setupintellijforbukkit**. You create the package by right clicking the **src** folder like the image below indicates.

[<img class="aligncenter size-full wp-image-139" src="https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/make_our_package.png?resize=930%2C747" alt="make_our_package" srcset="https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/make_our_package.png?w=930 930w, https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/make_our_package.png?resize=300%2C241 300w" sizes="(max-width: 930px) 100vw, 930px" data-recalc-dims="1" />](https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/make_our_package.png)

I went a head and made our main class and named it **MyMainClass**, beacuse I like it, and I put it in our newly made package. If we would try to extend this class from Bukkit _(JavaPlugin)_ nothing would happen, we would only get an error like this image shows.

[<img class="aligncenter size-full wp-image-148" src="https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/cannot_resolve_javaplugin.png?resize=454%2C182" alt="cannot_resolve_javaplugin" srcset="https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/cannot_resolve_javaplugin.png?w=454 454w, https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/cannot_resolve_javaplugin.png?resize=300%2C120 300w" sizes="(max-width: 454px) 100vw, 454px" data-recalc-dims="1" />](https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/cannot_resolve_javaplugin.png)

This is because we haven&#8217;t told IntelliJ where or what dependencies we need. We will need Bukkit as our dependency, let&#8217;s go a head and add that now. Do that by navigating to **File > Project Structure** or by using the hot key for **Ctrl + Alt + Shift + S** and navigate to the **Modules** and under the **Dependencies** tab click the green **plus sign** and click the **Jars and directories** and then locate your **craftbukkit** file, if you don&#8217;t have one yet follow [my tutorial on how to setup Bukkit on Windows](http://jejje.net/how-to-setup-a-minecraft-server-on-windows/ "How to setup a Minecraft server on Windows") and when the tutorial is finished you will both have the craftbukkit jar and a testing environment to later test out our plugins on.

[<img class="aligncenter size-full wp-image-141" src="https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/add_bukkit_jars_as_dependencies.png?resize=865%2C581" alt="add_bukkit_jars_as_dependencies" srcset="https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/add_bukkit_jars_as_dependencies.png?w=865 865w, https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/add_bukkit_jars_as_dependencies.png?resize=300%2C202 300w" sizes="(max-width: 865px) 100vw, 865px" data-recalc-dims="1" />](https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/add_bukkit_jars_as_dependencies.png)

Now IntelliJ suggests that we import Bukkit and we can do that by hitting **Alt + Enter** and now we can soon begin our development, as I mentioned before when we created our Module that we would add Maven support, it is now time to do that &#8211; and I chose to show you this longer approach so that if you in the future would forget it would be good to know how to add the framework afterwards, and we&#8217;ll add this by right clicking our **SetupIntelliJForBukkit** module and clicking **Add Framework Support&#8230;** and tick the Maven framework and it will be added.

[<img class="aligncenter size-full wp-image-144" src="https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/add_framework_support.png?resize=523%2C252" alt="add_framework_support" srcset="https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/add_framework_support.png?w=523 523w, https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/add_framework_support.png?resize=300%2C145 300w" sizes="(max-width: 523px) 100vw, 523px" data-recalc-dims="1" />](https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/add_framework_support.png)

Now if we would want to build our plugin, or artifact as it is called &#8211; we will need to tell IntelliJ which class is our main class. Remember when we went into the **Project Structure**, let&#8217;s go there again and click yourself into **Artifact**, and click the green plus sign and choose **Jar > From module with dependencies**.

[<img class="aligncenter size-full wp-image-146" src="https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/add_mainclass_path.png?resize=510%2C344" alt="add_mainclass_path" srcset="https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/add_mainclass_path.png?w=510 510w, https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/add_mainclass_path.png?resize=300%2C202 300w" sizes="(max-width: 510px) 100vw, 510px" data-recalc-dims="1" />](https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/add_mainclass_path.png)

Just clicking OK will find your Main class, but you can also try to locate it using the &#8220;&#8230;&#8221; on the Main Class field. Now finally, we can begin our Bukkit development and when it&#8217;s time to test our plugin out you will need to build the jar file, as I mentioned our plugin is an Artifact and when we&#8217;re going to build it we will navigate to **Build > Build Artifacts&#8230;** this will begin the process. So where will this jar file be saved, you might ask, when you where in the **Project Structure** under the **Artifacts** setting there is an input field named **Output Directory**. I usually set this directory to my plugins folder within my developing server, and I would recommend you to do the same.

<div style="font-size:0px;height:0px;line-height:0px;margin:0;padding:0;clear:both">
</div>