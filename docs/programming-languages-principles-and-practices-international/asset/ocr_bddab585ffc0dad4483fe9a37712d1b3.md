overloading). For example, in C and Java, if x and y have type **int**, then integer division is meant (with the remainder thrown away) and the result of the division also has type **int**, and if x and y have type **double**, then floating-point division is inferred. Similarly, a translator can determine if the data type of z is appropriate to have the result of the division copied into it. In C, the type of z can be any numeric type (and any truncation is automatically applied), while in Java, z can only be a numeric type that can hold the entire result (without loss of precision).

The process a translator goes through to determine whether the type information in a program is consistent is called **type checking**. In the preceding example, type checking verifies that variables x, y, and z are used correctly in the given statement.

Type checking also uses rules for inferring types of language constructs from the available type information. In the example above, a type must be attached to the expression `x / y` so that its type may be compared to that of z (in fact, x / y may have type **int** or **double**, depending on the types of x and y). The process of attaching types to such expressions is called **type inference**. Type inference may be viewed as a separate operation performed during type checking, or it may be considered to be a part of type checking itself.

Given a group of basic types like **int**, **double**, and **char**, every language offers a number of ways to construct more complex types out of the basic types; these mechanisms are called **type constructors**, and the types created are called **user-defined types**. For example, one of the most common type constructors is the **array**, and the definition

```
int a[10];
```

creates in C (or C++) a variable whose type is “array of int” (there is no actual array keyword in C), and whose size is specified to be 10. This same declaration in Ada appears as:

```
a: array (1..10) of integer;
```

Thus, the “array” constructor takes a base type (**int** or **integer** in the above example), and a size or range indication, and constructs a new data type. This construction can be interpreted as implicitly constructing a new set of values, which can be described mathematically, giving insight into the way the values can be manipulated and represented.

New types created with type constructors do not automatically get names. Names are, however, extremely important, not only to document the use of new types but also for type checking (as we will describe in Section 8.6), and for the creation of recursive types (Section 8.3.5). Names for new types are created using a **type declaration** (called a **type definition** in some languages). For example, the variable a, created above as an array of 10 integers, has a type that has no name (an **anonymous type**). To give this type a name, we use a **typedef** in C:

```
typedef int Array_of_ten_integers[10];
Array_of_ten_integers a;
```

or a type declaration in Ada:

```
type Array_of_ten_integers is array (1..10) of integer;
a: Array_of_ten_integers;
```

> ⁶Ada, on the other hand, has different symbols for these two operations: `div` is integer division, while `/` is reserved for floating-point division.