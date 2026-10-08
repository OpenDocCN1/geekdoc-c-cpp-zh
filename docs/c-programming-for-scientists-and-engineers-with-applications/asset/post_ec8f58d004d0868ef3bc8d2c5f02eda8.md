
# 678 Structures

```c
float   unitcost;
float   totcost;
}parts[10];
```

These two declarations are equivalent. In both cases the array variable parts[10] is an array of 10 elements of the same heterogeneous data type. When the structure tag is not specified, the array must be declared with the structure declaration, because no storage template is set up.

When the structure has been given a data type name, the array may be declared in a separate declaration statement after the structure is declared. The following code shows the declaration of structure variables in a separate statement.

```c
struct gadgetpart {
    char    partname[10];
    int     count;
    float   unitcost;
    float   totalcost;
};
```

struct gadgetpart parts[10];

Notice that the structure is declared first, and the array is declared in a separate statement following the structure declaration. To declare structure variables in a separate statement as shown, the structure tag must be included in the structure declaration.

The storage allocated for the structure array parts[10] is as follows:

| | partname | count | unitcost | totalcost |
|---|---|---|---|---|
| parts[0] | 10 bytes | 4 bytes | 4 bytes | 4 bytes |
| parts[1] | | | | |
| parts[3] | | | | |
| parts[4] | | | | |
| parts[9] | | | | |

Once an array is allocated storage, the values for the members may be stored and manipulated just like single variables. The members of the structure variables may be accessed by using either a member operator or by using the structure variable pointer. Arrays of structures are manipulated in the same way.

## 11.1.3 Structure Member and Pointer Operators

The members of a structure variable must be accessed to initialize them before they can be used in other ways. A structure variable member may be initialized when declared, or through an assignment statement, or by data input. The following demonstrates the use of the member operator and structure variable pointer to access the structure members.

### Structure Member Operator The members of a structure variable can be accessed by using a member operator (.). The following code shows the use of the member operator.

```c
struct gadgetpart {
    char pname[10];
    int count;
    float unitcost;
    float totalcost;
};

struct gadgetpart part;
part.partname
part.count
part.unitcost
part.totalcost
```

The storage is allocated as follows:

| | pname | count | unitcost | totalcost |
|---|---|---|---|---|
| part | 10 bytes | 4 bytes | 4 bytes | 4 bytes |

Notice that the variable name is followed by the member operator followed by the name of the structure member. Each one of these part.partname, part.count, part.unitcost, and part.totalcost is used like a single variable. The only difference is that each of the structure members is identified as belonging to structure variable part.

The following example shows the use of a member operator to assign values to the structure variable members.

```c
strcpy(part.partname, "bolt");
part.count = 20;
part.unitcost = 0.25;
part.totalcost = part.count * part.unitcost;
```

Notice that in each of these assignment statements the left-hand side consists of members of the structure variable part with a member operator (.). Since name is a character string array, a string cannot be assigned directly to it; instead the string copy function strcpy is used to copy the string "bolt" to the string member-name. The members count, unitcost, and totalcost are numeric; they are assigned numeric values using assignment statements.

The values are stored as follows:

| part.name | part.count | part.unitcost | part.totalcost |
| --- | --- | --- | --- |
| bolt | 20 | 0.25 | 5.00 |
| 10 bytes | 4 bytes | 4 bytes | 4 bytes |

A structure variable may also be initialized at the time it is declared as follows:
`struct gadgetpart part1 = {"bolt", 20, 0.25, 5.0};`

### Variable Pointer A pointer to a structure variable contains the memory address of the storage allocated to it. The value of the pointer is the address of the first byte of the storage allocated to the structure variable. Structure variables and structure pointers may both be declared following the structure declaration. The following code shows the declaration of structure variables and a structure pointer.

Structure declaration:

```c
struct gadgetpart {
    char partname[10];
    int count;
    float unitcost;
    float totalcost;
};
```

Structure variable declaration:

```c
struct gadgetpart part1, part2, part3, part4[10];
```

Structure pointer declaration:

```c
struct gadgetpart *ptr1, *ptr2, *ptr3, *ptr4;
```

Where ptr1, ptr2, ptr3, and ptr4 are pointers to structure variables of datatype gadgetpart. The addresses of the structure variables part1, part2, and part4[10] may be assigned to the structure pointers ptr1, ptr2, ptr3, and ptr4, respectively. The following code shows the assignment of the structure variable part1 address to ptr1.

```c
ptr1 = &part1;
```

The storage and the pointer access of the storage of the structure variable part1 is as follows:

![](img/8356e6c3bfe3b10354682c60b1e74b1d_700_0.png)

| | 1000 | bolt | 20 | 0.25 | 5.00 |
| ptr1 | 1000 | 10 bytes | 4 bytes | 4 bytes | 4 bytes |

Notice that ptr1 points to the structure, therefore structure members of structure variable part1 may be accessed using ptr1. For example, the address stored in ptr1 is 1000.

To access the members of the structure variable part1 using the pointer ptr, the pointer must be dereferenced first and then the member operator used.

As the member operator (.) has higher precedence than the dereference operator (*), and the structure variable pointer must be dereferenced first and then the member operator must be applied, parentheses must be used to indicate the order of precedence of the dereference operator and the member operator.

The code to implement this is as follows:

```c
(*ptr1).partname
(*ptr1).count
(*ptr1).unitcost
(*ptr1).totalcost
```

This is cumbersome to code and is also error prone. In C a special symbol called a member dereference operator (->), which is a hyphen followed by the greater symbol without any space between them, is provided to simplify the notation. The preceding expressions may be coded using the operator (->) as follows:

```c
ptr -> partname
ptr -> count
ptr -> unitcost
ptr -> totalcost
```

The following example shows the use of the member dereference operator to assign values to the members of the structure variable.

```c
strcpy(ptr1 -> partname, "nut");
ptr1 -> count = 20;
ptr1 -> unitcost = 0.25;
ptr1 -> totalcost = ptr1 -> count * ptr1 -> totalcost;
```

Notice that this is much simpler to code. The (->) symbol is used for structure pointers for the rest of this chapter.

![](img/8356e6c3bfe3b10354682c60b1e74b1d_701_0.png)

Notice that the character string is copied into partname, and values for the numeric variables count, unitcost, and totalcost are assigned using assignment statements.

### Members that Are Pointer Variables Pointers, arrays, and structures may be members of structure variables. The following structures describe the properties of a square and of the circles that can be inscribed within it and circumscribed around it.

```c
struct Circle
{
  float diam;
  float area;
};
```

```c
struct Square
{
  float side;
  float area;
  struct Circle innercircle;
  struct Circle outercircle;
};
```

Given the length of the side of a square, an instance of the structure Square area can be defined. The length of the side of the square can be used to determine the area of the square and the two instances of the structure Circle, one of which describes the circle inscribed in the square and the other of which describes a circle circumscribed around the square. The code would be as follows:

```c
int main()
{
  const float PI = 3.141593;
  struct Square box;
  float x, s;

  scanf("%f", &x);
  box.side = x;
  box.area = x * x;
  box.innercircle.area = PI * x * x / 4.0;
  s = sqrt(2.0 * x * x);
  box.outercircle.diam = s;
  box.outercircle.area = PI * s * s / 4.0;

  return 0;
}
```

If instead of declaring two members of the structure Square as Circle, they were declared as pointers to circles, the declaration of a Square and definition of an instance of square would require the definition of two instances of a Circle as follows:
