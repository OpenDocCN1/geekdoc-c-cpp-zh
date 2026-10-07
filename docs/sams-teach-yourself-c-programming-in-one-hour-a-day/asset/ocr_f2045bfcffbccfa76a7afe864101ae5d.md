These statements define the structure type coord and declare two structures, first
and second, of type coord. first and second are each instances of type coord; first
contains two integers named x and y, and so does second.

This method of declaring structures combines the declaration with the definition. The
second method is to declare structure variables at a different location in your source code
from the definition. The following statements also declare two instances of type coord:

```
struct coord {
    int x;
    int y;
};
/* Additional code may go here */
struct coord first, second;
```

In this example, you can see that the definition of the coord structure is separate from
the declaration of variables. When declaring variables, you use the struct
keyword followed by the structured tag followed by the name of the variable or variables
you to create.

# Accessing Members of a Structure

Individual structure members can be used like other variables of the same type. Structure
members are accessed using the structure member operator (.), also called the dot
operator, between the structure name and the member name. Thus, to have the structure
named first refer to a structure location that has coordinates x=50, y=100, you could write

```
first.x = 50;
first.y = 100;
```

To display the screen locations stored in the structure second, you could write
printf("%d,%d", second.x, second.y);

At this point, you might wonder what the advantage is of using structures rather than
individual variables. One major advantage is that you can copy information between
structures of the same type with a simple equation statement. Continuing with the
preceding example, the statement

```
first = second;
```

is equivalent to this statement:

```
first.x = second.x;
first.y = second.y;
```