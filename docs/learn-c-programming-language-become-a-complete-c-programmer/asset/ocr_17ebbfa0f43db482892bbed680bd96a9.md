# A Tour of C++: Concurrency and Utilities

> *When you wish to instruct, be brief.*
> – Cicero

+   - Introduction
+   - Resource Management **unique_ptr** and **shared_ptr**
+   - Concurrency

Tasks and **thread**s; Passing Arguments; Returning Results; Sharing Data; Communicating Tasks

+   - Small Utility Components

Time; Type Functions; **pair** and **tuple**

+   - Regular Expressions
+   - Math

Mathematical Functions and Algorithms; Complex Numbers; Random Numbers; Vector Arithmetic; Numeric Limits

+   - Advice

# 5.1 Introduction

From an end-user’s perspective, the ideal standard library would provide components directly supporting essentially every need. For a given application domain, a huge commercial library can come close to that ideal. However, that is not what the C++ standard library is trying to do. A manageable, universally available, library cannot be everything to everybody. Instead, the C++ standard library aims to provide components that are useful to most people in most application areas. That is, it aims to serve the intersection of all needs rather than their union. In addition, support for a few widely important application areas, such as mathematical computation and text manipulation, have crept in.

# 5.2 Resource Management

One of the key tasks of any nontrivial program is to manage resources. A resource is something that must be acquired and later (explicitly or implicitly) released. Examples are memory, locks, sockets, thread handles, and file handles. For a long-running program, failing to release a resource in a timely manner (“a leak”) can cause serious performance degradation and possibly even a miserable crash. Even for short programs, a leak can become an embarrassment, say by a resource shortage increasing the run time by orders of magnitude.

The standard library components are designed not to leak resources. To do this, they rely on the basic language support for resource management using constructor/destructor pairs