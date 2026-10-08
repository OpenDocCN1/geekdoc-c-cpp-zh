
*   **Representation:** A type “knows” how to represent the data needed in an object.
*   **Operations:** A type “knows” what operations can be applied to objects.

Many ideas follow this pattern: “something” has data to represent its current value – sometimes called the *current state* – and a set of operations that can be applied. Think of a computer file, a web page, a toaster, a music player, a coffee cup, a car engine, a cell phone, a telephone directory; all can be characterized by some data and all have a more or less fixed set of standard operations that you can perform. In each case, the result of the operation depends on the data – the “current state” – of an object.

So, we want to represent such an “idea” or “concept” in code as a data structure plus a set of functions. The question is: “Exactly how?” This chapter presents the technicalities of the basic ways of doing that in C++.

C++ provides two kinds of user-defined types: classes and enumerations. The class is by far the most general and important, so we first focus on classes. A class directly represents a concept in a program. A *class* is a (user-defined) type that specifies how objects of its type are represented, how those objects can be created, how they are used, and how they can be destroyed (see §17.5). If you think of something as a separate entity, it is likely that you should define a class to represent that “thing” in your program. Examples are *vector*, *matrix*, *input stream*, *string*, FFT (fast Fourier transform), valve controller, robot arm, device driver, picture on screen, dialog box, graph, window, temperature reading, and clock.

In C++ (as in most modern languages), a class is the key building block for large programs – and very useful for small ones as well, as we saw for our calculator (Chapters 6 and 7).

### 9.2 Classes and members

A class is a user-defined type. It is composed of built-in types, other user-defined types, and functions. The parts used to define the class are called *members*. A class has zero or more members. For example:

```cpp
class X { 
  public: 
    int m; // data member 
    int mf(int v) { int old = m; m=v; return old; } // function member 
};
```

Members can be of various types. Most are either data members, which define the representation of an object of the class, or function members, which provide operations on such objects. We access members using the *object.member* notation. For example:

```cpp
X var;
var.m = 7;    // assign to var's data member m
int x = var.mf(9);   // call var's member function mf()
// var is a variable of type X
```

You can read **var.m** as **var's m**. Most people pronounce it "**var dot m**" or "**var's m**". The type of a member determines what operations we can do on it. We can read and write an **int** member; call a function member; etc.

A member function, such as **X's** **mf()**, does not need to use the **var.m** notation. It can use the plain member name (**m** in this example). Within a member function, a member name refers to the member of that name in the object for which the member function was called. Thus, in the call **var.mf(9)**, the **m** in the definition of **mf()** refers to **var.m**.

### 9.3 Interface and implementation

Usually, we think of a class as having an interface plus an implementation. The interface is the part of the class's declaration that its users access directly. The implementation is that part of the class's declaration that its users access only indirectly through the interface. The public interface is identified by the label **public:** and the implementation by the label **private:**. You can think of a class declaration like this:

```cpp
class X {   // this class's name is X
public:
  // public members:
  //  -- the interface to users (accessible by all)
  // functions
  // types
  // data (often best kept private)
private:
  // private members:
  //  -- the implementation details (used by members of this class only)
  // functions
  // types
  // data
};
```

Class members are private by default; that is,

```cpp
class X {
    int mf(int);
    // ...
};
```

means

```cpp
class X {
private:
    int mf(int);
    // ...
};
```

so that

```cpp
X x;              // variable x of type X
int y = x.mf();    // error: mf is private (i.e., inaccessible)
```

A user cannot directly refer to a private member. Instead, we have to go through a public function that can use it. For example:

```cpp
class X {
    int m;
    int mf(int);
public:
    int f(int i) { m=i; return mf(i); }
};

X x;
int y = x.f(2);
```

We use private and public to represent the important distinction between an interface (the user’s view of the class) and implementation details (the implementer’s view of the class). We explain that and give lots of examples as we go along. Here we’ll just mention that for something that’s just data, this distinction doesn’t make sense. So, there is a useful simplified notation for a class that has no private implementation details. A **struct** is a **class** where members are public by default:

```cpp
struct X {
    int m;
    // ...
};
```

means

```cpp
class X {
  public:
    int m;
    // ...
};
```

**structs** are primarily used for data structures where the members can take any value; that is, we can't define any meaningful invariant (§9.4.3).

### 9.4 Evolving a class

Let's illustrate the language facilities supporting classes and the basic techniques for using them by showing how – and why – we might evolve a simple data structure into a class with private implementation details and supporting operations. We use the apparently trivial problem of how to represent a date (such as August 14, 1954) in a program. The need for dates in many programs is obvious (commercial transactions, weather data, calendar programs, work records, inventory management, etc.). The only question is how we might represent them.

#### 9.4.1 struct and functions

How would we represent a date? When asked, most people answer, “Well, how about the year, the month, and the day of the month?” That's not the only answer and not always the best answer, but it's good enough for our uses, so that's what we'll do. Our first attempt is a simple **struct**:

```cpp
// simple Date (too simple?)
struct Date {
  int y;    // year
  int m;    // month in year
  int d;    // day of month
};

Date today;   // a Date variable (a named object)
```

A **Date** object, such as **today**, will simply be three **ints**:

| | Date: |
|---|:---:|
| y: | **2005** |
| m: | **12** |
| d: | **24** |

There is no “magic” relying on hidden data structures anywhere related to a **Date** — and that will be the case for every version of **Date** in this chapter.
So, we now have **Dates**; what can we do with them? We can do everything in the sense that we can access the members of **today** (and any other **Date**) and read and write them as we like. The snag is that nothing is really convenient. Just about anything that we want to do with a **Date** has to be written in terms of reads and writes of those members. For example:

```cpp
// set today to December 24, 2005
today.y = 2005;
today.m = 12;
today.d = 24;
```

This is tedious and error-prone. Did you spot the error? Everything that’s tedious is error-prone! For example, does this make sense?

```cpp
Date x;
x.y = -3;
x.m = 13;
x.d = 32;
```

Probably not, and nobody would write that – or would they? How about

```cpp
Date y;
y.y = 2000;
y.m = 2;
y.d = 29;
```

Was year 2000 a leap year? Are you sure?
What we do then is to provide some helper functions to do the most common operations for us. That way, we don’t have to repeat the same code over and over again and we won’t make, find, and fix the same mistakes over and over again. For just about every type, initialization and assignment are among the most common operations. For **Date**, increasing the value of the **Date** is another common operation, so we write

```cpp
// helper functions:

void init_day(Date& dd, int y, int m, int d)
{
      // check that (y,m,d) is a valid date
      // if it is, use it to initialize dd
}
```
