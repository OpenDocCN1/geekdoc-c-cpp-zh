# Overview

As hardware becomes more complex and powerful, the software that they run becomes larger and more complex. As software grows, the number of programmers needed to write and maintain the software increases. As anyone who has experienced large programming teams will tell you, the more programmers you have working on one product, the more time you need to spend policing the code structure and managing its complexity.

As different programmers create and modify game systems, it is easy for the code to become a mismatch of different patterns and styles. Programmers also tend to have their own personal preferences when it comes to object creation, initialization, updating, and deletion.

Inter-object communication, if not tightly regulated, can become a spaghetti of code dependencies and object graph traversals. As programmers build objects that require data from other objects, it is all too easy to create monolithic dependency graphs and be forced to navigate awkward and non-intuitive object linkages. It is also too easy to create header file dependencies that have nothing to do with the actual job you are trying to accomplish, but are required so you can connect to other objects in the code.

Keeping track of code construction can become a full-time job, and modifying the code during the latter stages of a project can become error prone and dangerous. Fragile code is difficult to bug-fix without causing more bugs.

This gem discusses code execution hierarchies (CEH) as a way of controlling these problems and visualizing your code when things get confusing.