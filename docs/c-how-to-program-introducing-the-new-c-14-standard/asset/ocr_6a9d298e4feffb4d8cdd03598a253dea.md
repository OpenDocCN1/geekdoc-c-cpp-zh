# 19.1 Introduction

We’ve studied *fixed-size data structures*—such as one- and two-dimensional template-based `arrays` (**Chapter 7**) and built-in arrays (**Chapter 8**)—and various C++ Standard Library **dynamic data structures** (`arrays` and `vectors` in **Chapter 7** and other template-based containers in **Chapter 15**) that can grow and shrink during execution.

In this chapter, we demonstrate how you can create your own custom templatized dynamic data structures. We discuss several popular and important data structures and implement programs that create and manipulate them:

+   - **Linked lists** are collections of data items logically “lined up in a row”—insertions and removals are made *anywhere* in a linked list.
+   - *Stacks* (which we introduced in **Section 6.11** and discussed again in **Section 15.7.1**) are important in compilers and operating systems: Insertions and removals are made *only* at one end of a stack—its *top*.
+   - *Queues* represent *waiting lines*; insertions are made at the *back* (also referred to as the tail) of a queue and removals are made from the *front* (also referred to as the *head*) of a queue.
+   - **Binary trees** facilitate searching and sorting data, *duplicate elimination* and *compiling* expressions into machine code.