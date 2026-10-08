# A.12.2  Class member definitions

Class members that are integer constants, functions, or types can be defined/initialized either *in-class* (§9.7.3) or *out-of-class* (§9.4.4):

```
```
struct S {
    int c = 1;
    int c2;

    void f0() { }
    void f2();

    struct SS { int a; };
    struct SS2;
};
```
```

The members that were not defined in-class must be defined “elsewhere”:

```
```
int S::c2 = 7;

void S::f2() { }

struct S::SS2 { int m; };
```
```

If you want to initialize a data member with a value specified by the creator of an object, do it in a constructor.

Function members do not occupy space in an object:

```
```
struct S {
    int m;
    void f0;
};
```
```

Here, `sizeof(S)==sizeof(int)`. That’s not actually guaranteed by the standard, but it is true for all implementations we know of. But note that a class with a virtual function has one “hidden” member to allow virtual calls (§14.3.1).

# A.12.3  Construction, destruction, and copy

You can define the meaning of initialization for an object of a class by defining one or more *constructors*. A constructor is a member function with the same name as its class and no return type: