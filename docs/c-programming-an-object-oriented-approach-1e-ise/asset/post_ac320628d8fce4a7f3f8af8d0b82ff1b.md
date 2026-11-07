
## Program 7.8 The implementation file (Continued)

```cpp
13  Circle :: Circle (double rds)
14  : radius (rds)
15  {
16      if (radius < 0.0)
17      {
18          assert (false);
19      }
20  }
21  /****************************************************
22   * The default constructor that initializes a circle to 0.0.
23   * It does not need an assertion.
24   ****************************************************/
25  Circle :: Circle ()
26  : radius (0.0)
27  {
28  }
29  /****************************************************
30   * The copy constructor that copies the radius of another circle
31   * to create a new one. The source circle is already validated,
32   * which means that we do not need validation.
33   ****************************************************/
34  Circle :: Circle (const Circle& circle)
35  : radius (circle.radius)
36  {
37  }
38  /****************************************************
39   * A destructor that cleans up an object when the application is
40   * terminated.
41   ****************************************************/
42  Circle :: ~Circle ()
43  {
44  }
45  /****************************************************
46   * The setRadius function is defined to change the circle
47   * by decreasing or increasing the size of the radius. It needs
48   * validation because the new size must be a positive value.
49   ****************************************************/
50  void Circle :: setRadius (double value)
51  {
52      radius = value;
53      if (radius < 0.0)
54      {
55          assert (false);
56      }
57  }
58  /**********************************************************************
59   * The getRadius is a function that returns the radius                 *
60   * of an object. It needs the const modifier to prevent the            *
61   * accidental change of the host object.                                *
62   **********************************************************************/
63  double Circle :: getRadius () const
64  {
65      return radius;
66  }
67  /**********************************************************************
68   * The getArea accessor function returns the area of the host           *
69   * object. It needs the const modifier to prevent the accidental       *
70   * change of the host object.                                           *
71   **********************************************************************/
72  double Circle :: getArea() const
73  {
74      const double PI = 3.14;
75      return (PI * radius * radius);
76  }
77  /**********************************************************************
78   * The getPerimeter accessor function returns the perimeter of          *
79   * the host object. It needs the const modifier to prevent the          *
80   * accidental change of the host object.                                *
81   **********************************************************************/
82  double Circle :: getPerimeter () const
83  {
84      const double PI = 3.14;
85      return (2 * PI * radius);
86  }
```

**Creating the Application File** Program 7.9 is the same as we have seen before with one exception: The contents of the interface file is added at the beginning using the include macro.

## Program 7.9 The application file

```cpp
1  /**********************************************************************
2   * This is the application file that instantiates objects and         *
3   * lets the object operate on themselves using member functions.      *
4   * To be compiled, it needs a copy of the interface file.             *
5   **********************************************************************/
6  #include "circle.h"

int main ( )
{
    // Instantiation of first object and applying operations
    Circle circle1 (5.2);
    cout << "Radius: " << circle1.getRadius() << endl;
    cout << "Area: " << circle1.getArea() << endl;
    cout << "Perimeter: " << circle1.getPerimeter() << endl;
    cout << endl;
    // Instantiation of second object and applying operations
    Circle circle2 (circle1);
    cout << "Radius: " << circle2.getRadius() << endl;
    cout << "Area: " << circle2.getArea() << endl;
    cout << "Perimeter: " << circle2.getPerimeter() << endl;
    cout << endl;
    // Instantiation of third object and applying operations
    Circle circle3;
    cout << "Radius: " << circle3.getRadius() << endl;
    cout << "Area: " << circle3.getArea() << endl;
    cout << "Perimeter: " << circle3.getPerimeter() << endl;
    cout << endl;
    return 0;
}
```

**Compiling, Linking, and Running** The following shows the compiling, the linking, and the running processes. Note that these processes are separate from the creation of other files.

| Command | Description |
|---|---|
| `c++ -c circle.cpp` | Compilation of implementation file |
| `c++ -c app.cpp` | Compilation of application file |
| `c++ -o application circle.o app.o` | Linking of two compiled object files |
| `application` | Running the executable file |

```text
Radius: 5.2
Area: 84.9056
Perimeter: 32.656

Radius: 5.2
Area: 84.9056
Perimeter: 32.656

Radius: 0
Area: 0
Perimeter: 0
```

## 7.6.3 Preventing Multiple Inclusion

If we include the contents of the same header file more than once in a compilation file, the compiler issues an error and the compilation is aborted. To prevent this, we use the following preprocessor directives: *define*, *ifndef* (if not defined), and *endif*. In this section we learn how to use these three preprocessor directives to ignore a duplicate inclusion of a header file. In the file that will be included in another file, such as the interface file, we add these three directives as shown in Figure 7.16.

```c
#ifndef CIRCLE_H
#define CIRCLE_H

   // contents of the circle.h file

#endif
```

circle.h

**Figure 7.16** The contents of the header file after adding three directives

These three directives work with a flag (a constant). The flag we have used in the figure is the name of the file with an underscore followed by the letter H, all in uppercase. This is a convention; any name can be used if consistent. The directive *ifndef* follows the rule of the *if* statement. If the directive constant has not been defined, the body of *ifndef* is included. In other words, the code in `CIRCLE_H` is included in the file. If the flag is already defined, the preprocessor ignores the rest of the text and jumps to the *endif* directive.

Now let us see what happens when we include the file `circle.h` more than once in our program or include another file that also has the include directive. What we get is two copies of the `circle.h` contents in our file as shown in Figure 7.17.

When the preprocessor encounters the first *ifndef* directive, since the flag is not defined yet, it defines it (next line) and adds the rest of code until it encounters the *endif* directive, which means that the contents of the header file are added to the source file. When the preprocessor encounters the second *ifndef* directive, since the flag is already defined, it immediately jumps to the *endif* directive and does not include the contents of the header file again. That is what we need to accomplish. You may be wondering how a file gets included twice. Generally this happens when two different files, each with the same include file, are added to a third file.

![](img/d68f6199646ca63591a6d8419e0ed4ba_336_0.png)

**Figure 7.17** How conditional directives ignore duplicate inclusion

## 7.6.4 Encapsulation

You may wonder why we need separate compilations. Separate compilations allow us to achieve one of the goals of object-oriented programming, encapsulation. **Encapsulation** in object-oriented programming allows us to distinguish between the design of a class and the use of the class.

### Design of the Class

The designer creates the interface file and the implementation file. The designer makes the interface file public. The implementation file is compiled, but only the compiled version is made public; the source code remains private. The designer can change the implementation file at any time, re-compile it, and re-announce it.

### Use of the Class

The user receives a copy of the interface file and the compiled version of the implementation file. The user adds the interface to her application file and compiles it. He then links his own compiled file and the compiled file received from the designer to create an executable file.

### Effect

The effective result is that the designer protects both the interface file and the implementation file from any changes by the user as follows:

- The interface file is protected from change because there are two copies of it used in the process. The designer uses one copy and the user uses another copy. If the user changes the copy he received publicly, the separate-compilation process does not work.
- The implementation file is protected from change because the designer sends the compiled version of the file to the user. Compilation is a one-way process. The user cannot get the original file from the compiled file to change it.

This means the whole design is encapsulated in a box and cannot be changed by the user; the user can only create instances and let the instances operate on themselves.

### Public Interface

There is one more step before users can effectively instantiate objects and use them. Although users can print and look at the interface created by the designer, the designer normally creates what is called a **public interface**, which is the declaration of the member functions with some explanation so users will understand how to call the member functions in their applications.

> The public interface is a text file based on the function declaration that tells the user of the class how to use it.

Compared with a real-life object such as a product, the *public interface* is the manual we receive from the manufacturer that states how to use the product.

### EXAMPLE 7.6

Table 7.5 shows an example of the public interface for our *Circle* class (as developed so far). We can always add more explanation if needed to make the user comfortable.
