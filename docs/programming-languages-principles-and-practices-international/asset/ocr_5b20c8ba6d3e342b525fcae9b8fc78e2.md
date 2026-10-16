```
struct A{
    int data;
    struct A * next;
};
```

This is “old-style” C in which the data type is given by the struct name A, but the keyword struct must also always appear. Using a typedef one can remove the need for repeating the struct:

```
typedef struct A A;
struct A{
    int data;
    A * next;
};
```

Notice that we have used the same name, A, both for the struct name and the typedef name. This is legal in C, and it is useful in this case, since it reduces the number of names that we need to remember.12 This implies that struct names in C occupy a different symbol table than other names, so the principle of unique names for types (and variables) can be preserved.13 Some languages have extreme forms of this principle, with different symbol tables for each of the major kinds of definitions, so that one could, for example, use the same name for a type, a function, and a variable (why this might be useful is another question).

Java is a good example of this extreme form of name overloading, where the code of Figure 7.26 is perfectly acceptable to a Java compiler.14

```
class A
{  A A(A A)
{  A:
    for(; ;)
    { if (A.A(A) == A) break A; }
    return A;
  }
}
```

Figure 7.26 Java class definition showing overloading of the same name for different language constructs (adapted from Arnold, Gosling, and Holmes [2000], p. 153)

Figure 7.26 includes a definition of a class, a method (a function), a parameter, and a label, all of which share the name A. In Exercise 7.20, you will have the chance to explain which instances of a name represent definitions and which represent references.

12 In C++, the typedef is unnecessary, since the definition of struct A automatically creates a typedef named A.
13 In fact, C implementations often simply add a prefix like struct_ to a struct name and use the same symbol table, so the struct name A becomes struct_A and remains unique.
14 In Java, the different symbol tables for different kinds of definitions are called namespaces, not to be confused with the namespaces of C++.