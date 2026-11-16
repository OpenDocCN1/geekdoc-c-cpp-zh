# Chapter 27

# Date (and time) revisited - the BOOST libraries

In the introduction we used the construction of a _date_ class as an example of building a nontrivial (and useful) class. However, even if we follow the hints in the exercises, and use the operating system utilities for dealing with dates, at some point such a “homespun” date class needs to be replaced with something more reliable.

The date class that is most likely to spring to the programmers’ minds these days is one provided by the Boost C++ library. Let us therefore use this opportunity to introduce the Boost libraries, and show some examples of date usage. The Boost libraries are collections of C++ libraries, many of which may at some point become part of the C++ standard.¹ One of the most useful of the Boost libraries are complete libraries for date (gregorian) and date and time (date_time.

We are not going to go into detail here, we limit ourselves to showing some examples of usage:

¹Ten Boost libraries actually became part of the latest C++ standard (C++11). If you have a recent C++ implementation, the Boost libraries are typically included.