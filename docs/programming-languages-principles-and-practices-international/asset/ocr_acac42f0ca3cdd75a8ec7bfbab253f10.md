Finally, a module mechanism can document the dependencies of a module on other modules by requiring explicit import lists whenever code from other modules is used. These dependencies can be used by a compiler to automatically recompile out-of-date modules and to automatically link in separately compiled code.

In the following sections, we describe the mechanisms that several different languages (with very different approaches) offer to provide modular facilities.

# 11.3 Separate Compilation in C, C++ Namespaces, and Java Packages

We collect three different mechanisms in this section, because they are all less concerned with the full range of modular properties and are aimed primarily at separate compilation and name control.

# 11.3.1 Separate Compilation in C and C++

The first language we consider is C. C does not have any module mechanisms as such, but it does have separate compilation and name control features that can be used to at least simulate modules in a reasonably effective way. Consider, for example, a queue data structure in C. A typical organization would be to place type and function specifications in a so-called header file queue.h, as in Figure 11.5. Only type definitions and function declarations without bodies (called prototypes in C) go into this file. This file is used as a specification of the queue ADT by textually including it in client code as well as implementation code using the C preprocessor #include directive. Sample implementation code and client code are provided in Figures 11.6 and 11.7, respectively. Graphically, the separation of specification, implementation, and client code is as shown in Figure 11.4 (with the inclusion dependencies represented by the arrows).

![](bbox=[0.26, 0.53, 0.72, 0.71])

Figure 11.4 Separation of specification, implementation, and client code

```
(1) #ifndef QUEUE_H
(2) #define QUEUE_H

(3) struct Queuere p;
(4) typedef struct Queuere p * Queue;
```

Figure 11.5 A queue.h header file in C (continues)