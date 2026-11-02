# 10.2.2 Defining Variables of Structure Types

Structure definitions do not reserve any space in memory; rather, each definition creates a new data type that’s used to define variables—like a blueprint of how to build instances of that struct. Structure variables are defined like variables of other types. The definition

```
struct card aCard, deck[52], *cardPtr;
```

declares aCard to be a variable of type struct card, declares deck to be an array with 52 elements of type struct card and declares cardPtr to be a pointer to struct card. After the preceding statement, we’ve reserved memory for one struct card object named aCard, 52 struct card objects in the deck array and an uninitialized pointer of type struct card. Variables of a given structure type may also be declared by placing a comma-separated list of the variable names between the closing brace of the structure definition and the semicolon that ends the structure definition. For example, the preceding definition could have been incorporated into the struct card definition as follows:

```
struct card {
    char *face;
    char *suit;
} aCard, deck[52], *cardPtr;
```

# 10.2.3 Structure Tag Names

The structure tag name is optional. If a structure definition does not contain a structure tag name, variables of the structure type may be declared only in the structure definition—not in a separate declaration.

> **Good Programming Practice 10.1**
> 
> *Always provide a structure tag name when creating a structure type. The structure tag name is required for declaring new variables of the structure type later in the program.*

# 10.2.4 Operations That Can Be Performed on Structures

The only valid operations that may be performed on structures are:

+   - assigning struct variables to struct variables of the *same* type (see Section 10.7)—for a pointer member, this copies only the address stored in the pointer.
+   - taking the address (&) of a struct variable (see Section 10.4).
+   - accessing the members of a struct variable (see Section 10.4).
+   - using the sizeof operator to determine the size of a struct variable.

> **Common Programming Error 10.3**
> 
> *Assigning a structure of one type to a structure of a different type is a compilation error.*

Structures may not be compared using operators == and !=, because structure members are not necessarily stored in consecutive bytes of memory. Sometimes there are “holes” in a structure, because computers may store specific data types only on certain memory boundaries such as half-word, word or double-word boundaries. A word is a memory unit used to store data in a computer—usually 4 bytes or 8 bytes. Consider the following structure definition, in which sample1 and sample2 of type struct are declared: