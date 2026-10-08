The benefit of this interoperability is obvious: code can be written in a mix of C and C++. In particular, a C++ program can use libraries written in C, and C programs can use libraries written in C++. Furthermore, most languages (notably Fortran) have an interface for calling to/from C.

In the examples above, we assumed that C and C++ could share the class object pointed to by **p**. That is true for most class objects. In particular, if you have a class like this,

```
// in C++:
class complex {
double re, im;
public:
// all the usual operations
};
```

you can get away with passing a pointer to an object to and from C. You can even access **re** and **im** in a C program using a declaration:

```
/* in C: */
struct complex {
double re, im;
/* no operations */
};
```

The rules for layout in any language can be complex, and the rules for layout among languages can even be hard to specify. However, you can pass built-in types between C and C++ and also classes (**structs**) without virtual functions. If a class has virtual functions, you should just pass pointers to its objects and leave the actual manipulation to C++ code. The **call_f()** was an example of this: **f()** might be **virtual** and then that example would illustrate how to call a virtual function from C.

Apart from sticking to the built-in types, the simplest and safest sharing of types is a **struct** defined in a common C/C++ header file. However, that strategy seriously limits how C++ can be used, so we don’t restrict ourselves to it.

# ## 27.2.5 Pointers to functions

What can we do in C if we want to use object-oriented techniques (§14.2–4)? Basically, we need an alternative to virtual functions. For most people, the first idea that springs to mind is to use a **struct** with a “type field” that describes what kind of shape a given object represents. For example: