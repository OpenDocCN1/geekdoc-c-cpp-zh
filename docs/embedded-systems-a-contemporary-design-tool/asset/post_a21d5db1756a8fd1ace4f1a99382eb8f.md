
## 7.6.4 Operations

The only legal operations on a struct are:

- Copying.
- Assignment as a unit.
- Taking address, using the address of the operator, &.

Structs cannot be compared. Operations such as:

```
Point (...) ;
Point pt1, pt2 ;
if (pt1 == pt2)
{
}
```

are illegal.

## 7.6.5 Structs as Data Members

### 7.6.5.1 Accessing Members

Since a struct is a user-defined type and since one can declare instances of that type, there should be no reason that a data member of a struct could not be an instance of another struct. Such is, in fact, the case. Continuing with the Point example, a rectangle is fully specified by naming its opposite vertices. Expressing this concept graphically gives the diagram in Figure 7.37.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_377_0.png)

Figure 7.37 A Rectangle is Specified by two Points

We start with the UML object diagram for the rectangle. One can also say that the Rectangle is composed of two points. Such a relationship can be expressed in the composition diagram shown in Figure 7.38.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_377_1.png)

Figure 7.38 Expressing the Rectangle as a Composition of Points

The Point and the Rectangle can be defined as C structs shown in Figure 7.39. Once again, we will use the typedef in the declaration to simplify matters.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_378_0.png)

Figure 7.39 Using a Typedef to Simplify the Type Specification of a Point and a Rectangle

The order in which the two structs are declared is significant. Recall what we learned about function prototypes earlier. Since the declaration of a struct defines a new data type, one must make certain that it has been declared before it is used in a subsequent declaration. If the Rectangle was declared prior to the declaration of the Point, any attempt to compile the code fragment would have resulted in an error.

Accessing a data member of struct type within a struct is a simple extension of what we have done so far.

Given the declaration:

```
Rectangle r1;
r1.pt1.x
```

Refers to the x coordinate of pt1

```
r1.pt1.y
```

Refers to y coordinate of pt1

### 7.6.5.2 Initialization and Assignment

The initialization of a data member of struct type within a struct is a bit trickier. One cannot initialize an instance of a Rectangle with a bracketed list of points:

```
Rectangle r1 = {pt1, pt2};
```

Values for the data members can be assigned, however. The following code fragment provides values for the two data members.

```
Point p1 = {10, 20};
Point p2 = {20, 30};
Rectangle r1;
r1.pt1 = p1;
r1.pt2 = p2;
```

### 7.6.5.3 Functions

Let's now see how to put the struct to work. Some of the things that one might like to know about a Rectangle are its area and its perimeter. Since the C struct does not support functions, we will use pointers to functions. First the UML diagram and then the C definition are presented in Figure 7.40.

| Rectangle |
|---|
| +pt1 : Point |
| +pt2 : Point |
| +(area)(in pt0 : Point, in pt1 : Point) : int |
| +(perimeter)(in pt0 : Point, in pt1 : Point) : int |

```
typedef struct
{
 Point pt1;
 Point pt2;
 int (*area)(Point pt0, Point pt1);
 int (*perimeter) (Point pt0, Point pt1);
} Rectangle;
```

Figure 7.40 Adding Function Capability to a Struct

The object diagram shows that the Rectangle has two data members of type Point and two members that are pointers to functions. Each function takes two parameters of type Point and returns an int.

The design can now be turned into C code.

For this example, we will build the project from three separate files:

- A header file containing the struct definitions and the function prototypes – rect.h as identified in Figure 7.41. The header will be included in the two other files because they must know about Points and Rectangles.

```
typedef struct
{
 int x;
 int y;
} Point;

typedef struct
{
 Point pt1;
 Point pt2;
 int (*area)(Point pt0, Point pt1);
 int (*perimeter) (Point pt0, Point pt1);
} Rectangle;
int computeArea(Point pt0, Point pt1);
int computePerimeter(Point pt0, Point pt1);
```

Figure 7.41 Writing a Header File for the Struct Declarations

- An implementation file containing the definitions of the functions used to compute the rectangle’s area and perimeter is given in Figure 7.42. This is a C source file and will be linked into the project.

```
#include "rect.h"
// Rectangle area function
int computeArea(Point p0, Point pt1)
{
    int area = (pt1.x - p0.x) * (pt1.y - p0.y);
    return area;
}

// Rectangle perimeter function
int computePerimeter(Point p0, Point pt1)
{
    int perimeter = 2*(pt1.x - p0.x) + 2*(pt1.y - p0.y);
    return perimeter;
}
```

Figure 7.42 Writing the Implementation File for the Struct Definitions

- The main implementation file appears in Figure 7.43. This is a .c source file and the place where the work gets done.

```
#include <stdio.h>
// bring in struct definitions and function prototypes
#include "rect.h"

void main (void)
{
    // declare an instance of Rectangle
    Rectangle myRectangle;
    // declare some working variables
    int myArea = 0;
    int myPerimeter = 0;

    // assign values to instance data members
    myRectangle.pt1.x = 5;
    myRectangle.pt1.y = 10;
    myRectangle.pt2.x = 10;
    myRectangle.pt2.y = 20;

    // assign values to instance function pointers
    myRectangle.area = computeArea;
    myRectangle.perimeter = computePerimeter;

    // compute the area and perimeter
    myArea = myRectangle.area(myRectangle.pt1, myRectangle.pt2);
    myPerimeter = myRectangle.perimeter(myRectangle.pt1, myRectangle.pt2);

    printf("the area and perimeter are: %i, %i\n", myArea, myPerimeter);
    return;
}
```

Figure 7.43 Writing the Main Implementation File

Observe how the area and perimeter functions are invoked and in particular, how the parameters were passed in.

## 7.6.6 Pointers to Structs

A struct has an address in memory; therefore, one can use a pointer variable to refer to it exactly, as was done with pointers to any of the other variables we have studied. One can write:

```
typedef struct
{
    int pt1;
    int pt2;
} Rectangle;
Rectangle myRect;
Rectangle *rectPtr;
rectPtr = &myRect;
```

This code fragment declares an instance of a Rectangle and an instance of a pointer to a Rectangle; then it assigns the address of the instance to the pointer variable. Now let's look at accessing members of the rectangle.

### 7.6.6.1 Accessing Members

Since

```
*rectPtr
```

identifies the struct, the code fragment

```
(*rectPtr).pt1
```

refers to the member pt1. The parentheses around the pointer must be included because the . has higher precedence than * . Without the parentheses,

```
*rectPtr.pt1
```

is interpreted as

```
*(rectPtr.pt1)
```

which is illegal, as pt1 is not a pointer.

Because such pointer operations are so common, the C language defines a special short-hand symbol, ->. That notation allows one to replace the construct

```
(*ptr).member
```

with

```
structPtr -> member
```

The -> symbol is typed as the two characters: - followed by >. Using the shorthand notation, one may write:

```
rectPtr -> pt1;
```

The notation says that:

- rectPtr is pointer to a struct
- pt1 is a member

Thus, if one has:

Rectangle r1;
Rectangle *r1Ptr = &r1;

the following are equivalent:

r1.pt1;
r1Ptr -> pt1;

## 7.6.7 Passing Structs and Pointers to Structs

Passing an instance of a struct or a pointer to such an instance to a function is the same as any of the simpler intrinsic types. Let's look at an example.

### EXAMPLE 7.24

In this example, we will declare two functions, as given in Figure 7.44. One will accept an argument of type struct by value and the other by reference using a pointer. We access the data members exactly as was done outside of the function.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_382_0.png)

Figure 7.44 Passing Structs to Functions

Unlike arrays, the struct is passed by value in C by default. In an embedded application, passing a large struct by value can potentially cause the stack to overflow, thereby leading to unexpected system crashes. The problem is made significantly worse if one or more of the data members is an array.

> Coding Style
> Passing a struct to a function by value is generally not efficient.
> Passing by reference is the preferred way.

> Coding Style
> It is not considered good practice to declare an array as a struct data member and then to pass that struct into a function.

## 7.7 THE INTERRUPT

An interrupt is very similar to a function call. The major difference between the two is that the function invocation is synchronous to the normal program flow of control; the interrupt invocation originates with some event either inside or outside of the system and is asynchronous to the normal program flow of control. Among the minor differences, we find that variables can be passed into and returned from a function; one can neither pass a variable into nor return a variable from an interrupt. The reason will become clear shortly. First let's look at the structure of the interrupt control flow.

synchronous
asynchronous

### 7.7.1 The Interrupt Control Flow

An interrupt scheme is used so that one can be working on one job and then, when an important issue arises, immediately be notified. It is not necessary to continually check to see if the event has happened. A good simple model for an interrupt is the telephone. It is not necessary to sit by the telephone all day waiting for a call to come in – although, perhaps some people do. The ring provides notification that new information is arriving.

There are three major pieces to the interrupt structure:

- The interrupt event and source.
- The interrupt service routine (ISR).
- The interrupt vector table.

### 7.7.2 The Interrupt Event

An interrupt event can originate from a variety of sources. These sources may be in one of the many pieces of hardware in the system or in some piece of software. The interrupt is used to signify that some event of interest has occurred and that it must be dealt with. Potential events can include a timer expiring, an external signal changing state, or the result of a calculation or measurement exceeding a prespecified value.

Different microprocessors and microcomputers permit different numbers and kinds of interrupts. Some may be designated as software interrupts, whereas others are relegated to signaling hardware events. The number of interrupts may range from as few as one to as many as 12–16. One typically does not have the luxury of assigning any interrupt to
