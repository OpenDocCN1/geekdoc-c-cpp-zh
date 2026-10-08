+   * **Representation:** A type “knows” how to represent the data needed in an object.
* **Operations:** A type “knows” what operations can be applied to objects.

Many ideas follow this pattern: “something” has data to represent its current value – sometimes called the *current state* – and a set of operations that can be applied. Think of a computer file, a web page, a toaster, a music player, a coffee cup, a car engine, a cell phone, a telephone directory; all can be characterized by some data and all have a more or less fixed set of standard operations that you can perform. In each case, the result of the operation depends on the data – the “current state” – of an object.

So, we want to represent such an “idea” or “concept” in code as a data structure plus a set of functions. The question is: “Exactly how?” This chapter presents the technicalities of the basic ways of doing that in C++.

C++ provides two kinds of user-defined types: classes and enumerations. The class is by far the most general and important, so we first focus on classes. A class directly represents a concept in a program. A *class* is a (user-defined) type that specifies how objects of its type are represented, how those objects can be created, how they are used, and how they can be destroyed (see §17.5). If you think of something as a separate entity, it is likely that you should define a class to represent that “thing” in your program. Examples are *vector*, *matrix*, *input stream*, *string*, FFT (fast Fourier transform), valve controller, robot arm, device driver, picture on screen, dialog box, graph, window, temperature reading, and clock.

In C++ (as in most modern languages), a class is the key building block for large programs – and very useful for small ones as well, as we saw for our calculator (Chapters 6 and 7).

# 9.2 Classes and members

A class is a user-defined type. It is composed of built-in types, other user-defined types, and functions. The parts used to define the class are called *members*. A class has zero or more members. For example:

```
class X { 
  public: 
    int m; // data member 
    int mf(int v) { int old = m; m=v; return old; } // function member 
};
```

Members can be of various types. Most are either data members, which define the representation of an object of the class, or function members, which provide