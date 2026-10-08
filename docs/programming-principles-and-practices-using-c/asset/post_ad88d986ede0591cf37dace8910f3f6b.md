
Amazingly enough, thanks to a devious compatibility hack, this also works in C++. Having a variable (or a function) with the same name as a `struct` is a fairly common C idiom, though not one we recommend.

If you don't want to write `struct` in front of every structure name, use a `typedef` (§20.5). The following idiom is common:

```c
typedef struct { int x, y; } pair;  

pair p1 = { 1, 2 };
```

In general, you'll find `typedefs` more common and more useful in C, where you don't have the option of defining new types with associated operations.

In C, names of nested `structs` are placed in the same scope as the `struct` in which they are nested. For example:

```c
struct S {
    struct T { /* … */ };
    /* … */
};

struct T x;   /* OK in C (not in C++) */
```

In C++, you would write

```cpp
S::T x;       // OK in C++ (not in C)
```

Whenever possible, don't nest `structs` in C: their scope rules differ from what most people naively (and reasonably) expect.

### 27.3.2 Keywords

Many keywords in C++ are not keywords in C (because C doesn't provide the functionality) and can be used as identifiers in C:

**C++ keywords that are not C keywords**

| alignas | class | inline | private | true |
| :--- | :--- | :--- | :--- | :--- |
| alignof | compl | mutable | protected | try |
| and | concept | namespace | public | typeid |
| and_eq | const_cast | new | reinterpret_cast | typename |
| asm | constexpr | noexcept | requires | using |
| bitand | delete | not | static_assert | virtual |
| bitor | dynamic_cast | not_eq | static_cast | wchar_t |
| bool | explicit | nullptr | template | xor |
| catch | export | operator | this | xor_eq |
| char16_t | false | or | thread_local | |
| char32_t | friend | or_eq | throw | |

Don't use these names as identifiers in C, or your code will not be portable to C++. If you use one of these names in a header file, that header won't be useful from C++.

Some C++ keywords are macros in C:

**C++ keywords that are C macros**

| and | bitor | false | or | wchar_t |
| :--- | :--- | :--- | :--- | :--- |
| and_eq | bool | not | or_eq | xor |
| bitand | compl | not_eq | true | xor_eq |

In C, they are defined in `<ciso646.h>` and `<stdbool.h>` (bool, true, false). Don't take advantage of the fact that they are macros in C.

### 27.3.3 Definitions

C++ allows definitions in more places than C89. For example:

```c
for (int i = 0; i<max; ++i) x[i] = y[i];    // definition of i not allowed in C

while (struct S* p = next(q)) {               // definition of p not allowed in C
    /* ... */
}

void f(int i)
{
    if (i<0 || max<=i) error("range error");
    int a[max];       // error: declaration after statement not allowed in C
    /* ... */
}
```

C (C89) doesn't allow declarations as initializers in for-statements, as conditions, or after a statement in a block. We have to write something like

```c
int i;
for (i = 0; i<max; ++i) x[i] = y[i];

struct S* p;
while (p = next(q)) {
    /* ... */
}

void f(int i)
{
    if (i<0 || max<=i) error("range error");
    {
        int a[max];
        /* ... */
    }
}
```

In C++, an uninitialized declaration is a definition; in C, it is just a declaration so that there can be two of them:

```c
int x;
int x;    /* defines or declares a single integer called x in C; error in C++ */
```

In C++, an entity must be defined exactly once. This gets a bit more interesting if the two **ints** are in different translation units:

```c
/* in file x.c: */
int x;

/* in file y.c: */
int x;
```

No C or C++ compiler will find any fault with either **x.c** or **y.c**. However, if **x.c** and **y.c** are compiled as C++, the linker will give a “double definition” error. If **x.c** and **y.c** are compiled as C, the linker accepts the program and (correctly according to C rules) considers there to be just one **x** that is shared between code in **x.c** and **y.c**. If you want a program where a global variable **x** is shared, say so explicitly:

```c
/* in file x.c: */
int x = 0;             /* the definition */

/* in file y.c: */
extern int x;         /* a declaration, not a definition */
```

Better still, use a header file:

```c
/* in file x.h: */
extern int x;        /* a declaration, not a definition */

/* in file x.c: */
#include "x.h"
int x = 0;            /* the definition */

/* in file y.c: */
#include "x.h"
/* the declaration of x is in the header */
```

Better still, avoid the global variable.

### 27.3.4 C-style casts

In C (and C++), you can explicitly convert a value `v` to a type `T` by this minimal notation:

```c
(T)v
```

This “C-style cast” or “old-style cast” is beloved by poor typists and sloppy thinkers because it’s minimal and you don’t have to know what it takes to make a **T** from **v**. On the other hand, this style of cast is rightfully feared by maintenance programmers because it is just about invisible and leaves no clue about the writer’s intent. The C++ casts (*named casts* or *template-style casts*; see §A.5.7) were introduced to make explicit type conversion easy to spot (ugly) and specific. In C, you have no choice:

```c
int* p = (int*)7;     /* reinterpret bit pattern: reinterpret_cast<int*>(7) */
int x = (int)7.5;     /* truncate double: static_cast<int>(7.5) */

typedef struct S1 { /* . . . */ } S1;
typedef struct S2 { /* . . . */ } S2;
S2 a;
const S2 b;           /* uninitialized consts are allowed in C */

S1* p = (S1*)&a;     /* reinterpret bit pattern: reinterpret_cast<S1*>(&a) */
S2* q = (S2*)&b;     /* cast away const: const_cast<S2*>(&b) */
S1* r = (S1*)&b;     /* remove const and change type; probably a bug */
```

We hesitate to recommend a macro (§27.8) even in C, but it may be an idea to express intent like this:

```cpp
#define REINTERPRET_CAST(T, v) ((T) (v))
#define CONST_CAST(T, v) ((T) (v))

S1* p = REINTERPRET_CAST(S1*, &a);
S2* q = CONST_CAST(S2*, &b);
```

This does not give the type checking done by **reinterpret_cast** and **const_cast**, but it does make these inherently ugly operations visible and the programmer’s intent explicit.

### 27.3.5 Conversion of void*

In C, a **void\*** may be used as the right-hand operand of an assignment to or initialization of a variable of any pointer type; in C++ it may not. For example:

```cpp
void* alloc(size_t x);            /* allocate x bytes */

void f(int n)
{
    int* p = alloc(n * sizeof(int));  /* OK in C; error in C++ */
    /* ... */
}
```

Here, the **void\*** result of **alloc()** is implicitly converted to an **int**. In C++, we would have to rewrite that line to

```cpp
int* p = (int*) alloc(n * sizeof(int));  /* OK in C and C++ */
```

We used the C-style cast (§27.3.4) so that it would be legal in both C and C++.

Why is the **void\*-to-T\*** implicit conversion illegal in C++? Because such conversions can be unsafe:

```cpp
void f()
{
    char i = 0;
    char j = 0;
    char* p = &i;
    void* q = p;
    int* pp = q;       /* unsafe; legal in C, error in C++ */
    *pp = -1;          /* overwrite memory starting at &i */
}
```

Here we can’t even be sure what memory is overwritten. Maybe **j** and part of **p**? Maybe some memory used to manage the call of **f()** (f’s stack frame)? Whatever data is being overwritten here, a call of **f()** is bad news.

Note that (the opposite) conversion of a **T\*** to a **void\*** is perfectly safe – you can’t construct nasty examples like the one above for that – and those are allowed in both C and C++.

Unfortunately, implicit **void\***-to-**T\*** conversions are common in C and possibly the major C/C++ compatibility problem in real code (see §27.4).

### 27.3.6 enum

In C, you can assign an **int** to an **enum** without a cast. For example:

```c
enum color { red, blue, green };
int x = green;         /* OK in C and C++ */
enum color col = 7;    /* OK in C; error in C++ */
```

One implication of this is that we can use increment (**++**) and decrement (**--**) on variables of enumeration type in C. That can be convenient but does imply a hazard:

```c
enum color x = blue;
++x;      /* x becomes green; error in C++ */
++x;      /* x becomes 3; error in C++ */
```

“Falling off the end” of the enumerators may or may not have been what we wanted.

Note that like structure tags, the names of enumerations are in their own namespace, so you have to prefix them with the keyword **enum** each time you use them:

```c
color c2 = blue;      /* error in C: color not in scope; OK in C++ */
enum color c3 = red;  /* OK */
```

### 27.3.7 Namespaces

There are no namespaces (in the C++ sense of the word) in C. So what do you do when you want to avoid name clashes in large C programs? Typically, people use prefixes or suffixes. For example:

```c
/* in bs.h: */
typedef struct bs_string { /* ... */ } bs_string;  /* Bjarne’s string */
typedef int bs_bool;                          /* Bjarne’s Boolean type */
```
