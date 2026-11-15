data members are name, year, and category. A data member is referenced using the structure variable name followed by a period (called the **structure member operator**) and a data member name. Note the difference between referencing a value in a structure and in an array: A value in an array is referenced with the array name and a subscript.

# Definition and Initialization

To use a structure in a program, you must first define the structure. The keyword `struct` is used to define the name of the structure (also called the structure **tag**) and the data members that are included in the structure. After the structure has been defined, structure variables can be defined using declaration statements. Consider the previous definition for a variable representing a hurricane. The name of the structure is `hurricane`. The three data members are name, year, and category. Note that a semicolon is required after the structure definition.

The statements to define a structure can appear before the `main` function but they are often stored in a header file. It is important to note that these statements do not reserve any memory—they only define the structure. To define a variable of this structure type, we use the following statement in the declaration section of our program:

```
struct hurricane h1;
```

The preceding statement defines a variable named h1 that has three data members; this is shown in the following diagram:

| h1 | ? | name |
|---|---|---|
| | ? | year |
| | ? | category |

The declaration statement allocates memory for the three data members, but initial values have not been assigned; thus, their values are unknown.

The data members of a structure can be initialized in a declaration statement or with program statements. To initialize a structure with a declaration statement, the values are specified in a sequence that is separated by commas and enclosed in braces. The following declaration statement defines and initializes the example structure h1:

```
struct hurricane h1={"Camille", 1969, 5};
```

The data members of h1 are now initialized:

| h1 | "Camille" | name |
|---|---|---|
| | 1969 | year |
| | 5 | category |

To initialize the structure h1 using program statements, we can use statements such as the following:

```
h1.name = "Camille";
h1.year = 1969;
h1.category = 5;
```