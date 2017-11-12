---
title: 1st evaluation knocks!
date: 2017-06-28
categories:
 - GSoC
tags:
 - gsoc
 - open-source
 - sunpy
 - drms
comments: true
---

It’s a month now, since the coding period has begun, and here comes the week of evaluation. My mentors will be evaluating me on the work that has been done till now, and I wish I pass this.

There has been a little change in my plan, and last week, I stopped with writing tests for drms, and started doing the sunpy integration. Writing tests for 3 weeks got a bit monotonous for me, and hence I put up this idea with my mentors, on which they gladly agreed. It was going to give me a good break from writing tests for a while.
<!-- more -->
Until now, I have achieved the following tasks:

+ Covered the drms package to 66%
+ All the offline tests have been written, and jsoc tests have also been completed. The only thing that remains is testing the download function which will require mocking.
+ Mocking will also be required to avoid the online tests of jsoc.

I have planned to continue with the drms tests, especially mocking, from my 8th week of the coding period, just after my second evaluation. This phase of the coding period will be given to sunpy integration of the drms package.

The work done so far in drms is contained in this [PR](https://github.com/kbg/drms/pull/7).

In SunPy integration, I have integrated these parts:

+ Modified the query function of JSOC-Client to use the drms’ query function. Currently, basic requests can be made by providing keys only.

I aim to completely modify the query function, implementing all the necessary features, within a couple of days. I will go ahead with modifying the export method in the next week.
