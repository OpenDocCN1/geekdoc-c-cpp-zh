```
```c
Circle c2;
c2 = c1;
```
```

This causes every member of c1 to be copied to the corresponding member of c2. In a similar manner we could also write:

```
```c
Point p = c1.center;
c2.center = p;
```
```

The first statement copies every member of c1.center to the corresponding members of p. The second copies every member of p to the corresponding members of c2.center.

We finally note that variables can be defined in the same statement as the definition of the structure. For example, we could have written

```
```c
struct Circle{
    Point center;
    double radius;
} c1;
```
```

which would define the struct Circle as well as an instance c1.

# 15.1.1  Visibility of structure types and structure variables

If a structure type is going to be used in more than one function, it must be defined outside both the functions. The definition must actually appear before the functions in the file.

The rules for accessing structure variables are the same as the rules for variables of the fundamental data types (Section 3.6). Thus in the block in which a variable is defined, it can be used anywhere following its definition. Also, a name name defined in block B might shadow names defined in blocks that contain B, or the name name might in turn be shadowed by names defined in blocks contained in block B.

# 15.1.2  Arrays of structures

Note that we can make arrays of any data type. For example, we could make an array of circles or books if we wished.

```
```c
Circle c[10];
Book library[100];
```
```

We can refer to members of the elements of the arrays in the natural manner. For example, c[5].center.x refers to the x coordinate of the center of the fifth circle in c. Similarly library[96].title[0] would refer to the starting letter in the title of the 96th book in library.