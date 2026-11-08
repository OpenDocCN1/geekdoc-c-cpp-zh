Strictly speaking, this is called an **explicit specialization** (as opposed to an instantiated or generated specialization).

As described in Section 2.6 on page 33, specializations that still have template parameters are called **partial specializations**.

Click here to view code image

```
template<typename T>          // partial specialization
class MyClass<T, 2> {
};
```

When talking about (explicit or partial) specializations, the general template is also called the **primary template**.

# 10.3 DECLARATIONS VERSUS DEFINITIONS

So far, the words declaration and definition have been used only a few times in this book. However, these words carry with them a rather precise meaning in standard C++, and that is the meaning that we use.

A declaration is a C++ construct that introduces or reintroduces a name into a C++ scope. This introduction always includes a partial qualification of that name, but the details are not required to make a valid declaration. For example:

Click here to view code image

```
class C;              // a declaration of C as a class
int f(int p);         // a declaration of f as a function
                      // and p as a named parameter
extern int x;         // a declaration of x as a variable
```

Notice that even though they have a “name,” named definitions are not considered declarations in C++.

Definitions become definitions when the details of their structure are made known, or, in the case of variables, when storage space must be allocated. For class-type definitions, this means a brace-enclosed body must be provided. For function definitions, this means a brace-enclosed body must be provided (in the common case), or the function must be designated as `= default` or `= delete`. For a variable, initialization or the absence of an `extern` specifier causes a declaration to become a definition. Here are examples that complement the preceding nondefinition declarations:

Click here to view code image

```
class C { };             // definition (and declaration)

void f(int p) {          // definition (and declaration)
  // function body
}

int x = 1;               // an initializer makes this a
                         // definition for x
int i;                   // global variable declaration
                         // not preceded by extern
```

By extension, the declaration of a class template or function template is called a definition if it has a body. Here:

Click here to view code image

```
template<typename T>
void f() { }
```

is a declaration that is not a definition, whereas

Click here to view code image

```
template<typename T>
class C { };
```