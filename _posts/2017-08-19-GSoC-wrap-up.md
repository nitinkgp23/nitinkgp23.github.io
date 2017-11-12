---
title: GSoC wrap-up!
description: One of the various tutorials to help myself with repetitive tasks, such as getting a droplet on DO and configuring it.
date: 2017-08-19
categories:
 - GSoC
tags:
 - gsoc
 - open-source
 - sunpy
 - drms
comments: true
---

How time flies! Three months of the GSoC coding period are coming to an end now; most of the coding is done; documentation is done; testing is done. After missing 3 blog posts, unfortunately (I postponed it due to some rough time I had), here is a long one, describing whatever I did during my summers, and what else needs to be done before the PR gets merged.

My GSoC project was divided into 2 parts, one was writing a full test-suite for the [drms package](https://github.com/kbg/drms), and the second one was integrating this package into SunPy’s JSOC Client. While there are a few tests still remaining to be done for the first part, the second part is complete. Only blocker is passing of Travis build, which Cadair said, he will look into.

## Test-suite for drms

[This](https://github.com/kbg/drms/pull/7) is the PR that contains all of my tests for the drms package :

This PR adds tests for utils.py, config.py and client.py Covers config.py to 100% Covers utils.py to 81% WIP for client.

The coverage for the drms package > 80% , after excluding those files for which tests are not required, for example, config.py . The only function that needs to be tested, is the download function, for which I couldn’t get enough time to do, due to some extra modifications that had to done in my Part-2 of the project.

All the above tests are passing, as checked on my local computer, and all the functions other than the download function, are covered with the test-suite. Once the tests for the download function have been written, Travis can be added in the repository for the online builds, and can be converted into a conda package, later.

## The new JSOC-Client

My Part-2 of the project is contained in this [PR](https://github.com/sunpy/sunpy/pull/2188):

This PR aims to convert the old JSOC Client to use [drms](https://github.com/kbg/drms), as its backend.

This PR contains a total of 53 commits, with 1019 lines of code added, and 451 deletions as of now. It contains all of the summer project code, related to drms - SunPy integration, and contains the test-suite, documentation and the main code.

The main changes that have been done in the SunPy client are:

+ `search()`, `fetch()`, `get_request()` and `request_data()` functions have their backend changed. Now, it does all its operations through the drms package.
+ Note the change in the naming of the functions, `search()` which was `query()` earlier, and `fetch()` which was `get()` earlier. This change hasn’t been made in this PR.
+ A new function `search_metadata()` has been added, that takes the same input as the `search()` function and returns the whole set of metadata for the queried files. 
+ It returns a Pandas Dataframe that has rows as the queried files, and the columns as the name of keys for each file.
+ `jsoc.attrs.Compression()` property has been removed, since downloading of uncompressed files are not supported.
+ Now, `Series()` is the only mandatory attribute that needs to be provided. Other than Series, you must provide the value of at least one prime-key. Passing of time attributes isn't mandatory anymore.
+ You can pass Primekeys manually through `jsoc.attrs.PrimeKeys()` attribute.
+ Basically, PrimeKeys are the keys that can identify one queried file from another. Not providing a PrimeKey will give an error, as more than one file can be located for the same set of keys passed. Hence, passing of at least one PrimeKey is mandatory.
+ Time is one of the primekeys that is common across all series. Hence, it has been predefined in `jsoc.attrs.Time()` . Another common primekey in aia series data is `jsoc.attrs.Wavelength()` which has also been predefined. 
+ If you need to pass any other primekey manually, pass it through `jsoc.attrs.PrimeKeys()` attribute, like `jsoc.attrs.PrimeKeys({'HARPNUM':'5264'})` .
+ Keys can be manually passed. There is a default set of keywords like before, but you can override it by passing a list of keywords using `jsoc.attrs.Keys()` attribute.
+ More than 1 segment can be passed at a time, and that won’t result in formation of two query blocks. i.e. Segments can be ANDed. That is, this is possible :
`jsoc.attrs.Segment('Dopplergram')` & `jsoc.attrs.Segment('magnetogram')`
+ An interactive interface is built, in which when you pass an invalid segment name, or prime-key’s name, the code will break, and will give you the list of supported primekeys or segments, whichever be the case.
For example,
```
responses = client.search(jsoc.attrs.Time(‘2012/1/1T1:00:36’, ‘2012/1/1T01:00:38’),
       jsoc.attrs.Series(‘hmi.M_45s’), jsoc.attrs.Segment(‘foo’))
``` 
gives an error this:
```
ValueError: Unexpected Segments were passed. The series hmi.M_45s contains the following Segments [‘magnetogram’]
which clearly mentions, which segment names can be passed for the given series.
```

These are the features of the new JSOC Client.

+ Apart from these, the PR contains, an extensive test-suite, that primarily focuses on the sunpy functionalities, that is, the functions `_lookup_records()` and `_make_recordset()`. All corner cases and combinations have been tested. The part that uses the drms package, hasn’t been tested extensively (though, at least one check has been added for all the functions), since drms already covers those tests.

+ The docstrings after each function in the file jsoc.py is very detailed, and is full of examples. The narrative documentation is also detailed, explaining how to use jsoc client, both through Fido and direct usage. The narrative docs are also full of examples.

Hence, the sunpy integration of drms is complete. The only remaining blocker is that Travis fails for python 2.7 in installing drms. It will hopefully be solved soon.


## Modifying Time attribute of VSO

[This](https://github.com/sunpy/sunpy/pull/2260) is one of my very recent PRs :

This is WIP, and is a very initial effort to modify the Time attribute of VSO Client to return an astropy.time object instead of a datetime.datetime object. This was needed in order to support input of time in other Time scales, such as TAI.

This is WIP, and will be hopefully completed before the coding period is over.

And so, the summer time flew! I really enjoyed working on the project, and learned a great deal, about how to write software, and especially how to test them. My other project proposal, which was about developing the package Sunkit-image, is still in my wishlist, and would love to take it up after I have wrapped this whole thing up.

GSoC was one hell of an experience! Thank you Sunpy! Thank you Google! :D :D

