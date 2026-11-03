The structure's member values are displayed at Line 17 by using a printf() function. The statement is split between Lines 17 and 18, with the arguments for printf() on Line 18.

# Understanding struct

A structure is a collection. Think of it as a frame that holds multiple variable types. In many ways, a structure is similar to a record in a database. For example:

```
Name
Age
Gambling debt
```

These three items can be fields in a database record, but they can also be members in a structure: Name would be a string; Age, an integer; and Gambling Debt, an unsigned floating-point value. Here's how such a record would look as a structure in C:

```
struct record
{
    char name[32];
    int age;
    float debt;
};
```

struct is a C language keyword that introduces a structure. It's a definition that says, “This structure holds the following data types.”

record is the name of the new structure being created. It's not a variable — it's a structure type.

Within the curly brackets dwell the structure's members, the variables contained in the named structure. The record structure type contains three member variables: a string name, an int named age, and a float value, debt.

The struct keyword only defines a structure type, setting its contents. To use the structure, you must declare a structure variable of the structure type you created. For instance:

```
struct record human;
```

This statement declares a new variable human of the record structure type.