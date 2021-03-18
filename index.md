---
title: Using CSC HPC Environment Efficiently
author: CSC Training
---

# Handson

{% for hands-on in site.hands-on %}
- [{{ hands-on.title }}]({{ hands-on.url | relative_url }})
{% endfor %}

# Tutorial Lectures

Lectures as HTML slides. Use cursor keys or click left/right side of
the slide to change it. You can print the slides to PDF with Chrome,
just tweak the print settings a bit.

{% for slide in site.lectures %}
- [{{ slide.title }}]({{ slide.url | relative_url }})
{% endfor %}
