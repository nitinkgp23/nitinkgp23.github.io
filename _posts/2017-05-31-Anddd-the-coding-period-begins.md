---
title: Anddd.. The coding period begins!
date: 2017-05-31
excerpt: GSoC warm-up blog.
categories:
 - GSoC
tags:
 - gsoc
 - open-source
 - sunpy
 - drms
comments: true
---

After wasting away a full month of community bonding period (Naah, not wasting :/. I was busy doing an internship.), the coding period has finally arrived at my doors. I still have no idea about how I will begin with writing mock tests, and how will I achieve a full code coverage of 100% within 4 weeks.
[gif](https://cdn-images-1.medium.com/max/800/1*1EUR27g31w4wltCoEbOP5g.gif)
Absolutely no idea what’s happening!
<!-- more -->
Anyways, let’s see what happens next.

Kolja has been helping me by pushing some of his already written tests, and the coverage has already reached to almost 35%. But, the most challenging part of Phase 1 is yet to be started — writing Mocks.

    Mocking is simply the act of replacing the part of the application you are testing with a dummy version of that part called a mock. Instead of calling the actual implementation, you would call the mock, and then make assertions about what you expect to happen.

Python has a built-in library called unittest.mock that is used for creating mock objects. Going through numerous articles, blogs and video lectures, I have finally made sense of this weird technique. Yeah, weird, because although I say, I have made sense of it, I won’t be able to mock even a simple API call.
[gif](https://cdn-images-1.medium.com/max/800/1*oLlrmK5ps4sJDpRW8hwwpg.gif)
I am so ashamed of myself! :’(

The drms module for which, I have to write tests, fetches data from a server. So, to avoid interacting with the servers, or connecting online, every time the tests are run is, not a very good idea. With other alternatives to this option, one of them is to mock the objects. I have planned to finish up the testing part, in 3 weeks, and kept the last 1 week as buffer. I hope I pass my 1st evaluation!

[gif](https://cdn-images-1.medium.com/max/800/1*Jy-G4hziENez5JVhwx1hHA.gif)
Dear Lord, give me strength!
