on lines 9 to 11. This structure is declared with two members, x and y, which are both variables of type int.

On line 11, a variable myPoint is also declared as an instance of the coord structure. This declaration could also have been done on a separate line as follows:

```
struct coord myPoint;
```

On lines 16 and 17, the members of myPoint are assigned values. As stated earlier, values are assigned by using the name of the structure variable, followed by the member operator (.), and finally followed by the name of the member. On lines 19 and 20, these variables are used in a printf statement.

# Syntax

# The struct Keyword

```
struct tag {
    structure_member(s);
    /* additional statements may go here */
} instance;
```

The struct keyword is used to declare structures. A structure is a collection of one or more variables (structure_members) that have been grouped under a single name for easy manipulation. The variables don't have to be of the same variable type, nor do they have to be simple variables. Structures can also hold arrays, pointers, and other structures.

The keyword struct identifies the beginning of a structure definition. It's followed by a tag that is name given to the structure. Following the tag are the structure members, enclosed in braces. An instance, the actual declaration of a structure, can also be defined. If you define the structure without the instance, it's a template, or definition, and can be used later in a program to declare structures. Here is a template's format:

```
struct tag {
    structure_member(s);
    /* additional statements may go here */
};
```

To use the template, you use the following format:

```
struct tag instance;
```

To use this format, you must have previously declared a structure with the given tag.

# Example 1

+   * /* Declare a structure template called SSN */
struct SSN (