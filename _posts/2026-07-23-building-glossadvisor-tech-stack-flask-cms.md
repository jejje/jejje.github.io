---
title: "Building GlossAdvisor: What Actually Goes Into a Flask Side Project"
date: '2026-07-23 08:00:00'
author: JejjE
layout: post
permalink: "/2026-07-23-building-glossadvisor-tech-stack-flask-cms"
categories:
- Projects
- Web Dev
tags:
- flask
- python
- side project
- glossadvisor
- oauth
- affiliate
- seo
banner_image: "/glossadvisor-tech.png"
---

A while ago I wrote about the idea behind [GlossAdvisor](https://glossadvisor.com). This post is the follow-up for the people who are more interested in the how than the what. How it's built, what gave me trouble, and what I'd do differently.

<!--more-->

Spoiler: it ended up being a lot more than I originally planned for.

## It Became a Full CMS

My first thought was something like "Flask app, a few routes, a database, done." What I ended up building is closer to a full content management system. The admin panel covers brands, product categories, products with pricing and affiliate links, wash step templates, an article editor with image handling, ad slot configuration, site settings, user management - the whole thing.

The reason I went this direction is that I didn't want to touch code every time I needed to add a product or tweak an article. Having a real admin interface means I can actually maintain the content without a deploy. Worth the extra work upfront.

For translations I went with a `TranslatableMixin` that stores SV/EN strings as JSON in a single column. Nothing fancy, just a dict. Works fine for the scale I'm at and avoids the complexity of separate translation tables.

Database migrations go through Flask-Migrate (Alembic), so schema changes are versioned and reproducible. Early on I had a bad habit of just `ALTER TABLE`-ing things directly and it bit me a couple of times. Now everything goes through proper migrations and it's much less stressful.

## The Wash Wizard

The main feature is a questionnaire that builds a personalized wash session. Season, dirt level, location (washing at home or at a professional facility), skill level, what equipment you own. From those answers the app filters a library of wash step templates and builds a step-by-step guide.

Each step template has metadata for which seasons it applies to, which dirt levels, which equipment is required. Filtering is just matching the user's answers against those fields. Simple but effective.

Product recommendations sit on top of that. For each step, there's a priority queue: user's marked favorite first, then their highest-priority owned product, then the system's premium pick, then whatever's available. If the user has added products to their personal cabinet (a list of what they own), those get preferred. It's not machine learning, it's a ranked list — but it feels personal because it actually uses your data.

## External APIs Are Always More Work Than You Think

The biggest time sink was the Adtraction affiliate feed API. The idea is simple: sync prices from their feed into my database nightly. The reality: every advertiser in their network formats their product feed slightly differently.

The problem was that some of the affilaite stores hade insane data, importing all the products was about 1 million products - and I did not need that. Stock status comes back as a boolean from some advertisers and a string from others. I ended up writing defensive field extraction with explicit fallback chains, try the most common key first, fall through to alternates, log what came in so I can debug it later. Not the prettiest code but it handles the variety.

SKU matching was another thing I underestimated. When syncing a price update, I need to match the feed item to the right product in my database. The feed might have a SKU, an EAN, a product URL, or some combination. I try exact ID match first, then product URL, then create a new entry if nothing matches. Got that wrong a couple of times before the logic was solid.


## SMTP and Google OAuth

These are the two things that always sound like they'll take an afternoon and end up taking a week.

Email I handled with Flask-Mail. The flow is standard: register, get a verification email with a time-limited token (24 hours), click, account active. Password resets expire after one hour. Rate limiting on the email endpoints so nobody can hammer the resend button. The actual sending is maybe 30 lines of code. Testing all the failure cases (expired token, already-used link, too many resend attempts) is what takes time.

Google OAuth was a similar story. The happy path with Authlib is genuinely pretty clean, register the OAuth client, two routes, done. The edge cases are where it gets messy. What if someone tries to sign in with Google using an email that already has a password account? I link them automatically. What if they later delete their account? I revoke the Google token first. What about the redirect after login, how do you get them back to where they were? Save the `next` URL in session before the OAuth redirect, restore it in the callback.

And then there's the Google Cloud Console setup. Getting the redirect URIs exactly right, trailing slashes matter, HTTP vs HTTPS matters, localhost vs 127.0.0.1 sometimes matters. Debugging OAuth failures when the error message is just "invalid_request" is genuinely annoying. Took me longer than I'd like to admit.

## SEO: A Lot of Small Things

I spent more time on SEO than I expected, partly because it's technically interesting and partly because a content site with no search traffic is not very useful.

Every article gets structured JSON-LD: Article schema with headline, dates, author, publisher; BreadcrumbList for context; FAQPage schema when the article has Q&A content; VideoObject when there's a YouTube embed in the content (auto-detected from the HTML). Getting the structured data right per Google's spec takes some back-and-forth with their Rich Results Test tool.

I also implemented hreflang for the Swedish/English language split. Every page links to its counterpart in the other language. The URL path logic for figuring out which language you're viewing and what the equivalent URL is took more thought than I expected, especially for the homepage and for articles where the slug differs between languages.

Beyond that: canonical URLs everywhere, Open Graph and Twitter card tags, meta descriptions written per-article in the admin. Cache headers on static assets set to one year with `immutable` so browsers don't re-request them. Images get converted to WebP automatically on upload.

None of this is a silver bullet. It's just a lot of small things done correctly rather than one big trick.

## What Surprised Me

The scope. When you start connecting the pieces: user accounts, email, OAuth, affiliate feeds, an article CMS, SEO infrastructure, a product recommendation engine, it's a real project, not a weekend build. That's fine, I enjoyed it. But I didn't go in expecting it.

Working with external APIs taught me to be paranoid about response format variations. Always log the raw response during development. Write your field extraction so it's easy to add fallbacks. Don't assume the format stays consistent across different partners on the same platform.

OAuth and email are both areas where the happy path is easy and the edge cases are where you earn your keep. Write out all the states (token expired, account already exists, user is not verified yet) before writing any code.

If you're curious how it's all running, it's live at [GlossAdvisor.com](https://glossadvisor.com). Still building but the foundation starting to feel solid.

## What I'd Do Differently

If I started over, I'd design the affiliate feed integration before writing a single admin route, not after. Prices and stock status turned out to be the load-bearing part of the whole product, and I built the CMS first because it felt like the "real" work. That meant the defensive field-extraction and SKU-matching logic got retrofitted onto a schema that wasn't shaped for it, instead of the other way around. 

I'd tackle email and OAuth earlier rather than treating them as things to bolt on later. I underestimated them going in, so they landed near the end of the build when I was already tired of edge cases, when really they deserved to be one of the first things built and battle-tested.
