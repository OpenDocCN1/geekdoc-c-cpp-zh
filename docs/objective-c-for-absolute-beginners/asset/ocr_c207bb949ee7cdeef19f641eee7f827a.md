# A Note About ARC

While we covered a lot of the manual ways of handling memory if ARC isn't used, it is advisable to use ARC on any new project you create. What you learned here is that, while ARC hides how memory is retained and released, it is important to understand what's really happening under the covers.

# Summary

We've covered quite a bit in this chapter. Hopefully, you now have a clearer understanding of how memory, addresses, and pointers work. In this chapter, covered the following:

+   - Defining memory
- Using base-2, base-10, and base-16
- Defining and using memory addresses
- Defining and using pointers
- Allocating memory
- Using auto-variables and watching out for pitfalls so as not to cause a memory leak
- Deallocating memory and preventing memory leaks, including using the dealloc method
- Using the special pointers NULL and nil
- Understanding memory management using ARC
- Managing memory using Objective-C and its retain/release
- Detecting when things go wrong with memory allocation.

This chapter definitely covered a lot of ground, so congratulate yourself on making it through. Understanding how memory works on a Mac, iPhone, iPad, or any computing device is very important.

# Exercises

+   - In the following memory space, how large is the memory block? What is the address of the very last byte in this block of memory?