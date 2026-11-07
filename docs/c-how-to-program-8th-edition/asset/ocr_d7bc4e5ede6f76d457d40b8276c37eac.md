+   - **20.1** Introduction
+   - **20.2** Self-Referential Classes
+   - **20.3** Dynamic Memory Allocation and Data Structures
+   - **20.4** Linked Lists
+   - **20.5** Stacks
+   - **20.6** Queues
+   - **20.7** Trees
+   - **20.8** Wrap-Up

Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

Special Section: Building Your Own Compiler

# 20.1 Introduction

We’ve studied fixed-size **data structures** such as one-dimensional arrays and two-dimensional arrays. This chapter introduces **dynamic data structures** that grow and shrink during execution. **Linked lists** are collections of data items logically “lined up in a row”—insertions and removals are made *anywhere* in a linked list. **Stacks** are important in compilers and operating systems: insertions and removals are made *only at one end* of a stack—its **top**. **Queues** represent *waiting lines*; insertions are made at the *back* (also referred to as the *tail*) of a queue and removals are made from the *front* (also referred to as the *head*) of a queue. **Binary trees** facilitate high-speed searching and sorting of data, efficient *elimination of duplicate data items*, representation of *file-system directories* and *compilation of expressions* into machine language. These data structures have many other interesting applications.

We discuss several popular and important data structures and implement programs that create and manipulate them. We use classes, class templates, inheritance and composition to create and package these data structures for reusability and maintainability.

This chapter is solid preparation for Chapter 22, Standard Template Library (STL). The STL is a major portion of the C++ Standard Library. The STL provides *containers*, *iterators* for traversing those containers and *algorithms* for processing the containers’ elements. You’ll see that the STL has taken each of the data structures we discuss in this chapter and packaged them into templatized classes. The STL code is carefully written to be portable, efficient and extensible. Once you understand the principles and construction of data structures, you’ll be able to make the best use of the prepackaged data structures, iterators and algorithms in the STL, a world-class set of reusable components.

The chapter examples are practical programs that you’ll be able to use in more advanced courses and in industry applications. The programs employ extensive pointer manipulation. The exercises include a rich collection of useful applications.

We encourage you to attempt the optional major project described in the Special Section: Building Your Own Compiler. You’ve been using a C++ compiler to translate your programs to machine language so that you could execute these programs on your computer. In this project, you’ll actually build your own compiler. It will read a file of statements written in a simple, yet powerful, high-level language similar to early versions of the popular language BASIC. Your compiler will translate these statements into a file of Simpletron Machine Language (SML) instructions—SML is the language you learned in the Chapter 8 Special Section, Building: Your Own Computer. Your Simpletron Simulator program will then execute the SML program produced by your compiler! The special sec-