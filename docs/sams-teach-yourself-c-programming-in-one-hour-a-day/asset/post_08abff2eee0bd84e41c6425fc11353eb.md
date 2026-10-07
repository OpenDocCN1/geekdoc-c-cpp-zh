
# LESSON 11
Implementing Structures, Unions, and TypeDefs

Many programming tasks are simplified by the C data constructs called structures. A structure is a data storage type designed by you, the programmer, to suit your programming needs exactly. In this lesson you learn:

- What simple and complex structures are
- How to define and declare structures
- How to access data in structures
- How to create structures that contain arrays and arrays of structures
- How to declare pointers in structures and pointers to structures
- How to pass structures as arguments to functions
- How to define, declare, and use unions
- How to use type definitions with structures

## Working with Simple Structures

A structure is a collection of one or more variables grouped under a single name for easy manipulation. The variables in a structure, unlike those in an array, can be of different data types. A structure can contain any of C's data types, including arrays and other structures. Each variable within a structure is called a member of the structure. The next section shows a simple example.

You should start with simple structures. Note that the C language makes no distinction between simple and complex structures, but it's easier to explain structures in this way.

## Defining and Declaring Structures

If you write a graphics program, your code needs to deal with the coordinates of points on the screen. Screen coordinates are written as an x value, giving the horizontal position, and a y value, giving the vertical position. You can define a structure named coord that contains both the x and y values of a screen location as follows:

```
struct coord {
  int x;
  int y;
};
```

The struct keyword identifies the beginning of a structure definition. this struct keyword must be followed immediately by the name of the structure. This is the same rule that applies to the other data types you have created in C. The name of a structure is also known as the structure's tag or type name. Later you see how the tag is used.

Following the structure tag is an opening brace. Within the braces following the structure name is the list of the structure's member variables. You must give a variable type and name for each member.

The preceding code statements define a structure type named coord that contains two integer variables, x and y. This declaration of coord and its members, x and y, does not, however, actually create any instances of the structure coord or of the x and y variables. In other words, they don't declare (set aside storage for) any structures. There are two ways to declare structures. One is to follow the structure definition with a list of one or more variable names, as is one done here:

```
struct coord {
  int x;
  int y;
} first, second;
```

These statements define the structure type coord and declare two structures, first and second, of type coord. first and second are each instances of type coord; first contains two integers named x and y, and so does second.

This method of declaring structures combines the declaration with the definition. The second method is to declare structure variables at a different location in your source code from the definition. The following statements also declare two instances of type coord:

```
struct coord {
    int x;
    int y;
};
/* Additional code may go here */
struct coord first, second;
```

In this example, you can see that the definition of the coord structure is separate from the declaration of variables. When declaring variables, you use the struct keyword followed by the structure tag followed by the name of the variable or variables you want to create.

## Accessing Members of a Structure

Individual structure members can be used like other variables of the same type. Structure members are accessed using the structure member operator (.), also called the dot operator, between the structure name and the member name. Thus, to have the structure named first refer to a structure location that has coordinates x=50, y=100, you could write

```
first.x = 50;
first.y = 100;
```

To display the screen locations stored in the structure second, you could write
`printf("%d,%d", second.x, second.y);`

At this point, you might wonder what the advantage is of using structures rather than individual variables. One major advantage is that you can copy information between structures of the same type with a simple equation statement. Continuing with the preceding example, the statement

```
first = second;
```

is equivalent to this statement:

```
first.x = second.x;
first.y = second.y;
```

When your program uses complex structures with many members, this notation can be a great time-saver. Other advantages of structures will become apparent as you learn advanced techniques. In general, you will find structures to be useful whenever information of different variable types is treated as a group. For example, in a mailing list database, each entry could be a structure, and each piece of information (name, address, city, and so on) could be a structure member.

Listing 11.1 pulls together everything that has been covered up to this point. It is not practical; however, it illustrates the point of a simple structure.

## Input

LISTING 11.1 simplestruc.c Declaring and Using a Simple Structure

## Output

The coordinates are: (12, 14).

## Analysis

This listing defines a simple structure for holding the coordinates of a point. This is the same structure you've seen illustrated earlier in the lesson. On line 8, the struct keyword is used followed by the tag, coord. The body of the structure is on lines 9-11, which contains two members, x and y, both of type int. On line 12, myPoint is declared as an instance of coord. This declaration could also have been done on a separate line as follows:

```
struct coord myPoint;
```

## Using Structures That Are More Complex

Now that you have been introduced to simple structures, you can go on to the interesting and complex types of structures. These are structures that contain other structures as members and structures that contain arrays as members.

## Including Structures Within Other Structures

As mentioned earlier, a C structure can contain any of C’s data types. The preceding example can be extended to illustrate this.

Assume that your graphics program has to deal with rectangles. A rectangle can be defined by the coordinates of two diagonally opposite corners. You've already seen how to define a structure that can hold the two coordinates required for a single point. You need two such structures to define a rectangle. You can define a structure as follows (assuming, of course, that you have already defined the coord structure):

```
struct rectangle {
    struct coord corner1;
    struct coord corner2;
};
```
