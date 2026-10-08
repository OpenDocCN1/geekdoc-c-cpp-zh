The `#ifdef WINDOWS` test doesn't care what `WINDOWS` is defined to be; it just tests that it is defined.

Most major systems (including all operating system variants) have macros defined so that you can check. The check whether you are compiling as C++ or compiling as C is

```
```
  #ifdef __cplusplus
    // in C++
  #else
    /* in C */
  #endif
```
```

A similar construct, often called an include guard, is commonly used to prevent a header file from being #included twice:

```
```
  /* my_windows_header.h: */
  #ifndef MY_WINDOWS_HEADER
  #define MY_WINDOWS_HEADER
    /* here is the header information */
  #endif
```
```

The #ifndef test checks that something is not defined; i.e., `#ifndef` is the opposite of `#ifdef`. Logically, these macros used for source file control are very different from the macros we use for modifying source code. They just happen to use the same underlying mechanisms to do their job.

# 27.9 An example: intrusive containers

The C++ standard library containers, such as `vector` and `map`, are non-intrusive; that is, they require no data in the types used as elements. That is how they generalize nicely to essentially all types (built-in or user-defined) as long as those types can be copied. There is another kind of container, an intrusive container, that is popular in both C and C++. We will use an intrusive list to illustrate C-style use of structs, pointers, and free store.

Let's define a doubly-linked list with nine operations:

```
```
  void init(struct List* lst);       /* initialize lst to empty */
  struct List* create();              /* make a new empty list on free store */
  void clear(struct List* lst);       /* free all elements of lst */
  void destroy(struct List* lst);     /* free all elements of lst, then free lst */

  void push_back(struct List* lst, struct Link* p); /* add p at end of lst */
  void push_front(struct List*, struct Link* p);    /* add p at front of lst */
```
```