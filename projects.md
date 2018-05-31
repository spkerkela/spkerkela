---
layout: page
title: Projects
permalink: /projects/
---

Here are some projects I've published:

{% for project in site.projects %}
- [{{ project.name }}]({{ project.url }})
{% endfor %}