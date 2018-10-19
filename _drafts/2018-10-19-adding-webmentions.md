---
layout: post
title:  "Adding WebMentions"
date:   2018-10-19 14:16:38 +0300
categories: [software, programming, indieweb, webmentions]
---

One of the reasons I started this website was to have a small corner of the Internet all for myself. I love the liberating feeling of knowning that no matter what, I can have a contact point to the rest of the world via my personal domain and website (and email). I am not tied to Google or Facebook or Twitter etc for keeping me online and accessible.

I also like to keep the site static with minimal javascript so it remains accessible and fast for as long as it's up. I use [Jekyll](https://jekyllrb.com) to build the site from simple Markdown files.

A feature I would love to support is having conversations and interactivity with other people on the internet, but remain in control of the content on this site (no bots or spammers or assholes).

I found a community called [IndieWeb](https://indieweb.org) that seems aligned with my hopes for the future of the web, and one of the nice technologies they suggested was something I hadn't heard of before called [webmentions](https://www.w3.org/TR/webmention/).

There is a service called [webmention.io](https://webmention.io/) that makes it quite simple to begin supporting webmentions. They scrape your site for links to social media profiles that have a `rel="me"` attribute. They also provide an api that can be used during build time to automatically pull mentions.