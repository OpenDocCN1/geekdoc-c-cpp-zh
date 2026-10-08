Here we can’t even be sure what memory is overwritten. Maybe **j** and part of **p**? Maybe some memory used to manage the call of **f()** (f’s stack frame)? Whatever data is being overwritten here, a call of **f()** is bad news.

Note that (the opposite) conversion of a **T*** to a **void*** is perfectly safe – you can’t construct nasty examples like the one above for that – and those are allowed in both C and C++.

Unfortunately, implicit **void***-to-**T*** conversions are common in C and possibly the major C/C++ compatibility problem in real code (see §27.4).

# 27.3.6 enum

In C, you can assign an **int** to an **enum** without a cast. For example:

```
```c
enum color { red, blue, green };
int x = green;         /* OK in C and C++ */
enum color col = 7;    /* OK in C; error in C++ */
```
```

One implication of this is that we can use increment (**++**) and decrement (**--**) on variables of enumeration type in C. That can be convenient but does imply a hazard:

```
```c
enum color x = blue;
++x;      /* x becomes green; error in C++ */
++x;      /* x becomes 3; error in C++ */
```
```

“Falling off the end” of the enumerators may or may not have been what we wanted.

Note that like structure tags, the names of enumerations are in their own namespace, so you have to prefix them with the keyword **enum** each time you use them:

```
```c
color c2 = blue;      /* error in C: color not in scope; OK in C++ */
enum color c3 = red;  /* OK */
```
```

# 27.3.7 Namespaces

There are no namespaces (in the C++ sense of the word) in C. So what do you do when you want to avoid name clashes in large C programs? Typically, people use prefixes or suffixes. For example:

```
```c
/* in bs.h: */
typedef struct bs_string {/ . . . */} bs_string;  /* Bjarne’s string */
typedef int bs_bool;                          /* Bjarne’s Boolean type */
```
```