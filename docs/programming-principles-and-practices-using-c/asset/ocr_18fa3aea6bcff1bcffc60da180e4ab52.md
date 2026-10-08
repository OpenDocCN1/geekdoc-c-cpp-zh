because that’s conventionally reserved for macros (§27.8 and §A.17.2), which we avoid. We use an initial capital letter for types we define, such as **Square** and **Graph**. The C++ language and standard library don’t use the initial-capital-letter style, so it’s **int** rather than **Int** and **string** rather than **String**. Thus, our convention helps to minimize confusion between our types and the standard ones.

Avoid names that are easy to mistype, misread, or confuse. For example:

Name | names | nameS | foo | f00 | fl | fi | fi

The characters **0** (zero), **o** (lowercase **O**), **O** (uppercase **o**), **1** (one), **l** (uppercase **i**), and **l** (lowercase **L**) are particularly prone to cause trouble.

# ## 3.8 Types and objects

The notion of type is central to C++ and most other programming languages. Let’s take a closer and slightly more technical look at types, specifically at the types of the objects in which we store our data during computation. It’ll save time in the long run, and it may save you some confusion.

+   *   A *type* defines a set of possible values and a set of operations (for an object).
*   An *object* is some memory that holds a value of a given type.
*   A *value* is a set of bits in memory interpreted according to a type.
*   A *variable* is a named object.
*   A *declaration* is a statement that gives a name to an object.
*   A *definition* is a declaration that sets aside memory for an object.

Informally, we think of an object as a box into which we can put values of a given type. An **int** box can hold integers, such as *7, 42,* and *−399*. A **string** box can hold character string values, such as “Interoperability”, “tokens: !@#%\^&*\”, and “Old MacDonald had a farm”. Graphically, we can think of it like this:

```
int a = 7;    int b = 9;    char c = 'a';    double x = 1.2;    string s1 = "Hello, World!";    string s2 = "1.2";
```

![](bbox=[0.5, 0.73, 0.87, 0.91])