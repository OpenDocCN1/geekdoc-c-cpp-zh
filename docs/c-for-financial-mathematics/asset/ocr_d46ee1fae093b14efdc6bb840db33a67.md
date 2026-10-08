# ## Chapter 5

# ## Working with Multiple Files

A realistic C++ project will be divided across many files. This helps you organise your code logically into manageable units. This makes it possible to follow large software projects without having to understand every detail.

# 5.1 The project FMLib

If you have completed all the exercises in the previous chapters, you should now have developed quite a collection of functions.

In particular, during the exercises we have written the functions normcdf (to compute the cumulative density of the normal distribution) and norminv (to compute its inverse). We will want to use these functions repeatedly.

This means that it is time to start creating a better structure for our project. We will stop throwing code away and start work on a long-term project called FMLib.

The goal is that FMLib will be a library of useful financial maths functions. The FM stands for financial maths.

We’re not the first people to think of writing C++ code for financial mathematics. There are many libraries available that you can already download. However, in this book we will pretend that no libraries exist except those built into the C++ standard. We will build everything else ourselves from scratch.

This is a great way to learn C++, but not an intelligent way to build a real-world trading platform. You should, of course, take full advantage of the work done by other people in writing libraries (and even more importantly the work they have put in to designing, testing, and debugging these libraries). Some libraries that you may want to consider using are Boost, GSL, and Quantlib. Boost is a general purpose C++ library that fills in the many gaps in the C++ standard. GSL is a scientific computing library written in C which contains many useful algorithms. QuantLib is a C++ library for mathematical finance.

At this stage, you will probably find the documentation for these libraries impossible to understand. This is because the documentation assumes considerable expertise in the C++ language.

That is why in the rest of this book we will study how to write our own