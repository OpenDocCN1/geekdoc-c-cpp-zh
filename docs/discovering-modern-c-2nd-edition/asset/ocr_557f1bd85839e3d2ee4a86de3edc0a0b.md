# 4.6 Concurrency

C++11 Every general-purpose processor sold these days contains multiple cores. Nevertheless, it is still a challenge for many programmers to explore the computing power of multi-core platforms. C++11 has introduced a number of new libraries for this purpose, which we would like to introduce in this section.

# 4.6.1 Terminology

When computers perform multiple operations simultaneously, we speak of parallelism and/or concurrency. Unfortunately, these terms are not unambiguously defined and not clearly distinguished from each other. So let’s first clarify how we use the terms.

> **Definition 4-1. parallelism and concurrency:** _parallelism_ is any form of simultaneous processing and _concurrency_ is the simultaneous execution of multiple lightweight processes called _threads_ in a shared address space.

Thus, concurrency is a special case of parallelism. Another understanding of the term is often found in high-performance computing (HPC), where the use of multiple processors and the development of software for them is called parallelism. In this section we will deal exclusively with concurrency, but we will also use the more general term parallelism. This is enough for oncological subtleties! Now we finally want to focus on the technical realization.

# 4.6.2 Overview

The concurrency introduced in C++11 is realized in the form of multi-threading. In addition to using multiple cores, multi-threading can also be useful on a single core in order to use it more efficiently, for example, to load data from the web while the previously received data is being processed. Finding the right abstractions to provide maximum clarity and expressiveness on the one hand and optimal performance on the other is one of the biggest challenges of C++ development. The concurrent features