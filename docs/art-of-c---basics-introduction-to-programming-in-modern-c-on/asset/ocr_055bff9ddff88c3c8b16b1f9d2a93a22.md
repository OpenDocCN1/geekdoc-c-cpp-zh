# Lesson 26. Ring Buffer

# 26.1. Problem

A ring buffer is a data structure that behaves like an array with a circle-like topology: Circular buffer [https://en.wikipedia.org/wiki/Circular_buffer]. It has many uses. It can be used as an efficient fixed size FIFO queue (first in first out). It can also be used as an MRU list (most recently used), among other things.

Let’s implement a circular data structure that supports both the FIFO queue and MRU list use cases.

In a typical FIFO queue use case, if the finite-size queue becomes “full”, then we will need to throw an error or otherwise we should be able to indicate this situation in some way (e.g., to the client program) so that no data is lost. When a finite-size buffer is used for temporarily caching data, however, as in the typical use case of an MRU list (e.g., in the “recently open file list” menu in many file-oriented apps), we can just overwrite the old/oldest data with new data.

We will implement a ring buffer data structure as a library and create two test apps to use this data structure, one for a FIFO queue and the other for an MRU list.