---
title: Using CSC HPC Environment Efficiently
author: CSC Training
---

# Hands-on

{% assign items = site.hands-on |  sort: "title" | reverse %}

## Connecting
{% for hands-on in items %}
{% if hands-on.topic == 'connecting' %}
- [{{ hands-on.title }}]({{ hands-on.url | relative_url }})
{% endif %}
{% endfor %}

## Disk-areas
{% for hands-on in items %}
{% if hands-on.topic == 'disk-areas' %}
- [{{ hands-on.title }}]({{ hands-on.url | relative_url }})
{% endif %}
{% endfor %}

## Allas
{% for hands-on in items %}
{% if hands-on.topic == 'allas' %}
- [{{ hands-on.title }}]({{ hands-on.url | relative_url }})
{% endif %}
{% endfor %}

## Batch Jobs
{% for hands-on in items %}
{% if hands-on.topic == 'Batch jobs' %}
- [{{ hands-on.title }}]({{ hands-on.url | relative_url }})
{% endif %}
{% endfor %}

## Modules
{% for hands-on in items %}
{% if hands-on.topic == 'modules' %}
- [{{ hands-on.title }}]({{ hands-on.url | relative_url }})
{% endif %}
{% endfor %}

## Singularity
{% for hands-on in items %}
{% if hands-on.topic == 'singularity' %}
- [{{ hands-on.title }}]({{ hands-on.url | relative_url }})
{% endif %}
{% endfor %}

## Throughput
{% for hands-on in items %}
{% if hands-on.topic == 'throughput' %}
- [{{ hands-on.title }}]({{ hands-on.url | relative_url }})
{% endif %}
{% endfor %}

## Installing
{% for hands-on in items %}
{% if hands-on.topic == 'installing' %}
- [{{ hands-on.title }}]({{ hands-on.url | relative_url }})
{% endif %}
{% endfor %}
