---
layout: post
title: 'Hosting your own GitHub alternative'
date: 2018-10-23 22:00:00 +0300
categories: [software, self-hosting]
---

Yesterday, October 22, 2018 [GitHub](https://github.com) was down for some hours and I started wondering how much work and productivity was put on hold globally because of it.

Even though one of the greatest assets of `git` is it's decentralized nature and capability to do work offline, a single service being down can cause a lot of disruption for many people. I like GitHub, the UI is great, and pull requests and issues are a great way to see and review changes to a project, so it's natural many people depend on the service.

I started to search for a way to have a possible "backup" GitHub, and while naturally the same source could live in [BitBucket](https://bitbucket.org) and [GitLab](https://about.gitlab.com), I kept coming back to the idea of self hosting one. I also wanted to have a service I could possibly use in the future as an "origin" repository if for whatever reason I didn't want to host stuff overseas. Keeping a clean UI with pull requests and issues was another requirement, as well as being able to run on a smaller server.

Finally I came across [Gitea](https://gitea.io/en-us/), a resource efficient Git-service written in Go, deployed as a single binary, and became intrigued.

I decided to use this opportunity to also test out [DigitalOcean](https://www.digitalocean.com), so I started up an Ubuntu
droplet, installed [postgresql](https://www.postgresql.org) and [nginx](https://nginx.org) on it, created a SSL certificate with [letsencrypt](https://letsencrypt.org), pointed nginx to my Gitea service and voilá: [my own git service running over https!](https://git.spkerkela.com)

This was a fun and relatively quick project that I recommend for anyone interested in having a GitHub-like place to keep their code (Gitea also supports private repos) and is worried about all of their precious source being on _someone elses server_.

From now on I will be keeping all my source in both GitHub and my own Gitea. An easy way to do this is running these commands in your repo:

```bash
$ git config --add remote.all.url git@github.com:username/repo.git
$ git config --add remote.all.url git@git.selfhosted.com:username/repo.git
$ git push all # boom, push to both repos!
```
