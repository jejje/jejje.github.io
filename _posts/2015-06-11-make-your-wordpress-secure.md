---
id: 165
title: Make your WordPress Secure
date: 2015-06-11T10:21:05+00:00
author: JejjE
layout: post
guid: http://jejje.net/?p=165
permalink: /make-your-wordpress-secure/
dsq_thread_id:
  - "3839639038"
banner_image: /wp-content/uploads/2015/06/make_wordpress_secure.png
categories:
  - Security
  - Website
tags:
  - how-to
  - plugins
  - security
  - wordpress
---
Security is an really important topic, and if you&#8217;re one of many other WordPress users you might have seen many login attempts, and some of you may even have been unfortunate enoguh to have your site hacked &#8211; that sucks, and that&#8217;s why we need to step up our game and increase the security with a few simple steps that I will walk you through. We wouldn&#8217;t want our WordPress site be a part of the problem would we?
<!--more-->
##  How to make WordPress secure

When I was going to secure my own websites I begun researching different plugins that would help out with the major WordPress security issues, one to mention is the fact that every WordPress installation has the same address to the admin dashboard **/wp-admin/** changing only this would make it a lot safer, or the fact that you might have an actual admin account named **admin**. But how would one go about doing all of these stuff? Well you could get one plugin to fix each problem separately, or you could use one of a few whole-package-kind-of-deal. I went with the latter option, and I will list three highly recommended ones that you can try out for yourself.

### iThemes Security &#8211; 4,7/5

Let&#8217;s begin with <a href="https://wordpress.org/plugins/better-wp-security/" target="_blank" rel="nofollow">iThemes Security plugin</a>, I feel this plugin is a really good _all-in-one solution _ and it&#8217;s ease of use is really appealing. When you&#8217;ve installed it you can see a long list of items that needs your attention color coded according to priority.

[<img class="aligncenter size-full wp-image-169" src="https://i1.wp.com/jejje.net/wp-content/uploads/2015/06/suggested_actions_to_secure_wordpress_ithemes.png?resize=755%2C473" alt="iThemes suggestions to secure your WordPress" srcset="https://i1.wp.com/jejje.net/wp-content/uploads/2015/06/suggested_actions_to_secure_wordpress_ithemes.png?w=755 755w, https://i1.wp.com/jejje.net/wp-content/uploads/2015/06/suggested_actions_to_secure_wordpress_ithemes.png?resize=300%2C188 300w" sizes="(max-width: 755px) 100vw, 755px" data-recalc-dims="1" />](https://i0.wp.com/jejje.net/wp-content/uploads/2015/06/suggested_actions_to_secure_wordpress_ithemes.png)

Follow this easy interface and secure as many of them as you can, and as you see fit &#8211; you should at least take care of the High Priority and most of the Medium Priority, one of the high priority you should take care of is the admin account with it&#8217;s id of 1, this is not a good idea.

[<img class="aligncenter size-full wp-image-172" src="https://i0.wp.com/jejje.net/wp-content/uploads/2015/06/secure_admin_user_ithemes.png?resize=655%2C387" alt="Securing your admin account is a high priority" srcset="https://i0.wp.com/jejje.net/wp-content/uploads/2015/06/secure_admin_user_ithemes.png?w=655 655w, https://i1.wp.com/jejje.net/wp-content/uploads/2015/06/secure_admin_user_ithemes.png?resize=300%2C177 300w" sizes="(max-width: 655px) 100vw, 655px" data-recalc-dims="1" />](https://i1.wp.com/jejje.net/wp-content/uploads/2015/06/secure_admin_user_ithemes.png)

It will not take you long to complete many of the steps this plugin suggest and it will give you peace of mind, be proactive with security!

### All In One WP Security & Firewall &#8211; 4.9/5

This one has a lot <a href="https://wordpress.org/plugins/all-in-one-wp-security-and-firewall/" target="_blank" rel="nofollow">nifty features at the cost of a little harder setup</a>, some of the nice tools are **WHOIS Lookup** and **Maintenance Mode** which can be a really practical way to be able to try out new themes and plugins before it goes live in front of your users. You&#8217;ll also get a pretty nice, and something that is both nice and a flaw in my opinion is the ability to edit your **.htaccess** and your **wp-config**, the latter is in my opinion a security flaw since it contains your database information &#8211; but the **.htaccess** one can make it easier to put on an extra layer of security &#8211; but it can also give you headache setting it up . This image below shows a <span class="_5yl5" data-reactid=".7f.$mid=11433955738474=24046dbd0cc6b7f3d92.2:0.0.0.0.0"><span data-reactid=".7f.$mid=11433955738474=24046dbd0cc6b7f3d92.2:0.0.0.0.0.0">gauge </span></span>and a pie chart to give a visual of how secure your wordpress is, but I still found this plugin a bit hard to setup &#8211; maybe for the little more tech savy.

[<img class="aligncenter wp-image-174 size-full" src="https://i2.wp.com/jejje.net/wp-content/uploads/2015/06/security_gauge.png?resize=608%2C204" alt="All In One WP Security & Firewall has a nice guage to represent the security level of your WordPress" srcset="https://i1.wp.com/jejje.net/wp-content/uploads/2015/06/security_gauge.png?w=608 608w, https://i1.wp.com/jejje.net/wp-content/uploads/2015/06/security_gauge.png?resize=300%2C101 300w" sizes="(max-width: 608px) 100vw, 608px" data-recalc-dims="1" />](https://i1.wp.com/jejje.net/wp-content/uploads/2015/06/security_gauge.png)

It still has basically everything you need and about the same features as iThemes has, but it is not as easy as clicking &#8220;just fix it already&#8221; &#8211; well almost at least. I found that this took a little bit longer to setup but it&#8217;s packed with good features, and as I mentioned above a few flaws ([in my opinion]({{ site.baseurl }}/wp-content/uploads/2015/06/big-lebowski.jpg)).

### Wordfence Security &#8211; 4,9/5

At a first glance, this plugin gives you a well documented tour of all it&#8217;s feature and that is an impressive way to introduce you to something as important as securtiy. It&#8217;s packed with features, every single one of them have a link to a fairly well documented page. But I must say I miss a few features that both **iThemes** and **All In One WP Security & Firewall** have &#8211; to obscure the _wp-admin_**, **changing username and so on.

[<img class="aligncenter size-full wp-image-179" src="https://i0.wp.com/jejje.net/wp-content/uploads/2015/06/live_traffic_stats.png?resize=494%2C280" alt="Live Traffic stats is one of many nice features WordFence has to offer" srcset="https://i1.wp.com/jejje.net/wp-content/uploads/2015/06/live_traffic_stats.png?w=494 494w, https://i1.wp.com/jejje.net/wp-content/uploads/2015/06/live_traffic_stats.png?resize=300%2C170 300w" sizes="(max-width: 494px) 100vw, 494px" data-recalc-dims="1" />](https://i0.wp.com/jejje.net/wp-content/uploads/2015/06/live_traffic_stats.png)

Maybe it would be a good idea to use **WordFence** in tandem with one of the above plugins but that is of personal preference, and you&#8217;d have to try it out and see what you think yourself. I&#8217;ve heard much good about WordFence both free version and paid premium version, but I&#8217;d really need to bang on my own WordPress to actually make a proper decision &#8211; or be under attack.

## More ways of securing your WordPress

It&#8217;s easy to focus on WordPress it self, but there is more you can focus on to keep your site safe &#8211; and every bit counts.

### Adding an .htaccess file

One of these is the **.htaccess** I mentioned above. This simple file will put an extra layer of security, will give you the little bit of extra peace of mind while you sleep at night. But I&#8217;d also like to mention that your site performance might take a small hit, unless you have your own server or VPS and can put it in your apache config, since it will be read every time the site is accessed. But if you feel like the trade off is worth it, and you&#8217;re a bit patient and tech savvy you can try out these resources:

  * <a href="http://www.htaccesstools.com/htaccess-authentication/" target="_blank" rel="nofollow">htaccess tools authentication generator</a>
  * <a href="http://www.htaccesstools.com/htpasswd-generator/" target="_blank" rel="nofollow">htpasswd tool for generating password file</a>
  * <a href="http://www.wpwhitesecurity.com/definite-guide-htaccess-wordpress/" target="_blank" rel="nofollow">The definitive guide to htaccess and WordPress</a>

### The wallet

This is my least favorite part of all the tips and tricks of securing your site, choosing a web host just because it&#8217;s the cheapest is not really a good idea &#8211; they&#8217;re usually the cheapest one for a reason. Try and find a few reviews before you decide on a web hosting company, it shouldn&#8217;t take you too long. If you&#8217;ve found a good web host they might even be able to help you secure your WordPress site.

## Conclusion

I&#8217;ve talked some about three of the more popular plugins to secure your WordPress, and I also made a poll on Facebook to see what other users had and what their opinions were &#8211; the champion of these three were **WordFence **with amazing **53%**, were many used this plugin on all of their sites. **iThemes Security** & **All In One WP Security & Firewall** got the same amount of votes and landed on **21%**, and the last option which were **Another plugin** got only **5%** of all the votes.

Try out some of these plugins and you&#8217;ll probably notice how valuable these are and hopefully your site will be much safer from hackers and ill-doers, you should try them out and see which one you like the best, leave a comment and tell me which ones you like the best.

&nbsp;

<div style="font-size:0px;height:0px;line-height:0px;margin:0;padding:0;clear:both">
</div>