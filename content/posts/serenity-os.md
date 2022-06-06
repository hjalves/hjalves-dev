---
title: "Serenity OS"
date: 2022-06-06T17:00:00+01:00
author: Humberto Alves
---

SerenityOS is a POSIX compliant system with a retro-style UI (heavily inspired 
in Windows 2000), written in modern C++ and a custom, nicer alternative to STL 
(the C++ stdlib equivalent). It was started in 2018 by Andreas Kling, and since 
then, it just kept growing and amassing a vibrant community of developers and 
enthusiasts.

There is an ongoing effort to make a new programming language to (hopefully) replace
C++, but it's still too early to say if it will be a successful operation.

Every piece of software from the kernel to the userland applications live in 
the same repository (monorepo approach). And one of the core philosophies is to 
implement every component of the system ‘in home’ - drivers, protocols and tools. 
It even has a browser built completely from scratch (which is quite insane!).

Although it tries to not depend on third-party software and libraries, it still 
gives you the choice to install many ports of popular software, like Python 3 or Quake.

Since discovering the project last year, I started keeping track of its progress 
by watching many of the videos posted by the creator of the system in his YouTube 
channel (especially the monthly updates and the weekly Q&A on Fridays afternoons).

But after lurking around for many months, I finally decided to contribute, 
even thought I don’t really know how to code in C++. I have a small list of 
things I would like to fix and improve.

I’m going to try posting regular updates describing my journey and experiences 
into the system and documenting the progress of the projects I have in mind. 
