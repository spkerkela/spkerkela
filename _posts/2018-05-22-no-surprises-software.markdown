---
layout: post
title:  "No Surprises Software"
date:   2018-05-22 13:49:38 +0300
categories: [software, minimalism]
---

I have recently been increasingly frustrated with the tools that I've been using in my day to day job. I constantly stumble into unexpected and surprising behaviour, leaving me to read and debug more and more code that others have written.

A few days ago I spent a day fighting with [pipenv](https://docs.pipenv.org/) not installing the correct version of `pip` on our CI machine as described in the `Pipfile`. I was downgrading our `pip` because [Zappa](https://github.com/Miserlou/Zappa) (and apparently many other packages) were relying on deprecated features of `pip` that were removed in the recent version upgrade.

So many surprises in succession left me somewhat tired and angry at the status of the so called _state of the art_ in the Python world. And while my woes happened to materialize with `pip` and `pipenv` in this case, similar issues and worse are very prevalent in other ecosystems as well,  such as the modern web-stack for example, whatever it happens to be today.

I have also recently gotten more familiar with the [Unix](http://www.catb.org/~esr/writings/taoup/html/ch01s06.html) and [suckless](https://suckless.org/philosophy/) philosophies and this combined with the aforementioned struggles have inspired me to start creating "No Surprises Software".

I have decided to start a small experiment. Whenever I come across a program that I think works in a surprising way, I will try to create a "No Surprises" version of it and blog about the experience. If you share my annoyance at constant surprising behaviour, perhaps you will join me in trying to reduce the number of surprises us developers have to face daily.

May you have a surprise free, perhaps even boring day!