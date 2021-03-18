---
title: WIP - Biocontainers(101) - Containerised Bioinformatics
author: CSC Training
---

Biocontainers (101) is a basic level course to learn skills required for running bioinformatics applications in a containerised environment. This is a remote course and includes both lectures and hands-on exercises.

## Why this Bio course on containers

Bioinformatics tools often require installing different dependencies in a controlled environment. Containers allow you to logically package your application (e.g., a bioinformatics tool) together with libraries and other dependencies,providing isolated environments for running your software services. Containerised applications can be run in an isolated runtime environment independent of actual environment (e.g., private data center, the public cloud, or even a developer’s personal laptop) in which the applications are running in. These are recently gaining popularity as a standard way to distribute, deploy, and run services by developers and system administrators. They provide the means to start a light-weight virtualization environment, i.e., a container, based on Linux kernel namespaces and control groups (cgroups). Such virtualization environment is cheap to create, manage, and destroy, requires a negligible amount of time to set-up, and provides performance equatable with the one of the host. Docker offers an intuitive way to manage containers by abstracting and automating the low-level configuration of namespaces and cgroups, ultimately enabling the development of an entire ecosystem of tools and products around containers.


## Expected learning in this Course

In this basic course, you will be introduced to the fundamentals of container technology (mainly, docker) in addition to the selected examples of containerised bioinformatics applications. This basic understanding of containers is necessary to be able to work with bio applications in a containerised environment with different options and requirements.

More specifically, you will learn:

- The essential concepts of running docker containers
- How to use docker volumes to manage persistent data
- The basics of docker networks
- The containerised applications in Bioinformatics
- The basic Singularity concepts for running in HPC environment

After this course, one will be able to launch and work with pre-existing containerised applications in his or her work-life as a bioinformatician.


## Course targets

One will be able to launch and work with pre-existing containerised applications in their work life  as bioinformaticians.

## Pre-requisites

While we don't discourage anybody from joining this course, one should  be comfortable working with commandline environment e.g., in Linux terminal, editing files with common editors (e.g., vi, nano, emacs, etc.) in order to get maximum benefit from this course.

## Targeted audience for this course

Bioinformatician
Biologist with linux skills
Biologists who are willing to get some feel of containers may join the course


## How to get most advantage from this course

Practice ! practice ! and  practice !!!

## Expected way of learning

- Lectures
- hands-on tutorial



# Tutorials

{% for tutorial in site.tutorials %}
- [{{ tutorial.title }}]({{ tutorial.url | relative_url }})
{% endfor %}

# Excercises

{% for exercise in site.exercises %}
- [{{ exercise.title }}]({{ exercise.url | relative_url }})
{% endfor %}


# Tutorial Lectures

Lectures as HTML slides. Use cursor keys or click left/right side of
the slide to change it. You can print the slides to PDF with Chrome,
just tweak the print settings a bit.

{% for slide in site.lectures %}
- [{{ slide.title }}]({{ slide.url | relative_url }})
{% endfor %}
