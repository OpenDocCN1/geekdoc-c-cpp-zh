```
We are in outer block

m = 20
::m = 10
```

In the above program, the variable **m** is declared at three places, namely, outside the **main()** function, inside the **main()**, and inside the inner block.

> **NOTE:** *It is to be noted ::m will always refer to the global m. In the inner block, ::m refers to the value 10 and not 20.*

A major application of the scope resolution operator is in the classes to identify the class to which a member function belongs. This will be dealt in detail later when the classes are introduced.

# 3.16 Member Dereferencing Operators

As you know, C++ permits us to define a class containing various types of data and functions as members. C++ also permits us to access the class members through pointers. In order to achieve this, C++ provides a set of three pointer-to-member operators. [Table 3.5](#table-3.5) shows these operators and their functions.

**Table 3.5** *Member dereferencing operators*

| Operator | Function |
|---|---|
| `::*` | To declare a pointer to a member of a class |
| `.*` | To access a member using object name and a pointer to that member |
| `->*` | To access a member using a pointer to the object and a pointer to that member |