
![](img/0235a4ea835dc4575bd036e024a533b3_76_0.png)

## Main Window

There is a lot of information on the main window that we will not discuss at this time. For this example, we will focus our attention on the left side of the main window. Note that a folder named Chapter_3 has been created for us as well as the file main.cpp. We can view and edit the contents of main.cpp by selecting it. The contents of the selected file will be displayed in the window of the text editor provided by Xcode as shown below.

![](img/0235a4ea835dc4575bd036e024a533b3_76_1.png)

## Main Window: main.cpp Selected

We see that `main.cpp` has comments, a compiler directive, and a block of code to define `int main(int argc, const char * argv[])`. The parameters, `argc` and `argv[]` are not used in this example and will be discussed later in the text. Within the body of `main.cpp`, the string "Hello, World!" is printed to standard output and a value of zero is returned.

To compile and run this program, select **Run** from the **Product** menu provided at the top of the Xcode window. The program will first compile, or build, successfully and then execute. The standard output is streamed to the console on the lower right hand corner of the main window as shown below.

![](img/0235a4ea835dc4575bd036e024a533b3_77_0.png)

Main Window: Console Output

We have now successfully compiled and executed our first C++ program using Xcode. Next, we will add our `Point` class to the current project. To add a new file to our project, we select **New > File...** from the **File** menu provided at the top of the Xcode window. This launches a template window as shown below. Select **Source** from the left side of the template window and **C++ File** from the right side of the window and click **Next**.

![](img/0235a4ea835dc4575bd036e024a533b3_78_0.png)

## Template Window

This launches an options window. This options window asks if we would also like to create a header file.

![](img/0235a4ea835dc4575bd036e024a533b3_78_1.png)

## Point Options Window

Recall that our Point class definition has an implementation file, Point.cpp, and a declaration file, Point.h. Point.cpp is the source file and Point.h is the header file so, yes, we want Xcode to create a source file and a header file, both named Point. Click Next, then select a directory from the save window and click Create. Two new files, Point.cpp and Point.h, have now been added to the project as shown below on the left side of the main window.

![](img/0235a4ea835dc4575bd036e024a533b3_79_0.png)

## Main Window: Point.cpp Selected

Add the C++ statements to Point.cpp, as provided in Section 2.3. Then, select Point.h and add the C++ statements for Point.h as provided in Section 2.3. Finally, select main.cpp and add the necessary statements from program chapter_2_3. When finished, our project files should look like the files shown in the next three views of the main window.

![](img/0235a4ea835dc4575bd036e024a533b3_79_1.png)

## Main Window: Modified Point.cpp Selected

![](img/0235a4ea835dc4575bd036e024a533b3_80_0.png)

Main Window: Point.h Selected

Notice that the file Point.h includes 3 new compiler directives: #ifndef, #define, #endif. These compiler directives ensure that the data type Point will be defined only once.

![](img/0235a4ea835dc4575bd036e024a533b3_80_1.png)

Main Window: Modified main.cpp Selected

Select Run from the Product menu provided at the top of the Xcode window. Your output should look like the output in the console window on the lower right hand corner of the main window.

## Modify 2.3

The following problems refer to program chapter_2_3, developed in this section.

- 1. Add a new type declaration statement to declare a new Point, p3, with an initial value of (-1,0). Run your program and explain your results.
- 2. Add a new type declaration statement to define a new Point with an x value of 1.5 and a y value of 3.6. Run your program and explain your results.
- 3. Add the following assignment statement to your program, just above the return statement:
  `p1 = ORIGIN;`
  Run your program and explain your results.
- 4. Add the following assignment statement to your program, just above the return statement:
  `ORIGIN = p1;`
  Run your program and explain your results.

## 2.5 C++ Operators

To perform operations in a program, such as addition, multiplication, and comparison of objects, we use special operators that are defined for the built in data types supported by C++. In this section, we will look at several of these operators.

### Assignment Operator

An assignment statement uses the assignment operator = to store the result in the memory location named by the identifier. The general form of the assignment statement is
identifier = expression;

where an expression can be a constant, another object, or the result of an operation. Consider the following two sets of statements that declare and give values to the objects sum, x1, p1, and ch:

```cpp
// Set One
double sum;
int x1[3];
Point p1(1.5, -4.7);
char ch('a');
```

```cpp
// Set Two
double sum;
int x1;
Point p1, p2(1.5, -4.7);
char ch;

sum = 10.5;
x1 = 3;
p1 = p2;
ch = 'a';
```

After either set of statements is executed, the value of sum is 10.5, the value of x1 is 3, the value of p1 is (1.5, -4.7) and the value of ch is 'a', as shown in the following memory snapshot:

![](img/0235a4ea835dc4575bd036e024a533b3_82_0.png)

The statements in Set One declare and initialize the objects at the same time in the type declaration statement; the assignment statements in Set Two could be used at any point in the program and thus may be used to change (as opposed to initialize) the values of objects that have already been declared. Note that the compiler provides an assignment operator for the Point class. The assignment operator performs a bit-wise copy of the data members from the object on the right-hand side of the assignment operator to the corresponding data members of the object on the left-hand side of the assignment operator.

Multiple assignments are also allowed in C++, as in the following statement, which assigns a value of zero to each of the objects x, y, and z:

```cpp
x = y = z = 0;
```

Multiple assignments are discussed further at the end of this section.

| Statement Box 2.3 |
|---|
| **Assignment Statements:** An assignment statement uses an assignment operator to store the value of an expression in the memory location named by the identifier. The expression can be a constant, a variable or an expression that evaluates to a type that is compatible with the data type of the identifier. |
| **Syntax** |
| `identifier = expression;` |
| **Examples** |
| `x1 = y1;` |
| `counter = 0;` |
| `counter = counter + 1;` |

The assignment operator should not be confused with equality. Assignment statements should be read as is assigned the value of; thus, the statement rate = stateTax is read; rate is assigned the value of stateTax. If stateTax contains the value 0.06, then rate also contains the value 0.06 after the statement is executed; the value in stateTax is not changed. The memory snapshots before and after this statement is executed are the following:

| Before: | double rate ? | double stateTax 0.06 |
| After: | double rate 0.06 | double stateTax 0.06 |

If we assign a value to an object that has a different data type, then a conversion must occur during the execution of the statement. Sometimes the conversion can result in information being lost. For example, consider the following declaration and assignment statement:

```cpp
int a;
...
a = 12.8;
```

Because a is declared to be an integer, it cannot store a value with a nonzero decimal portion. Therefore, in this case, the memory snapshot after executing the assignment statement is the following:

```
int a [ 12 ]
```

> Note that the value 12.8 is truncated, not rounded.

To determine whether a numeric conversion will work properly, we use the following order, which is from high to low:

- high: long double
- double
- float
- long integer
- integer
- low: short integer

If a value is moved to a data type that is higher in order, no information will be lost; if a value is moved to a data type that is lower in order, information may be lost. Thus, moving an integer to a double will work properly, but moving a float to an integer may result in the loss of some information or in an incorrect result. In general, use only assignments that do not cause potential conversion problems. Unsigned integers were not included in the list because errors can occur in both directions.

> In general, use only assignments that do not cause potential conversion problems. Unsigned integers were not included in the list because errors can occur in both directions.

### Arithmetic Operators

An assignment statement can be used to assign the result of an arithmetic operation to an object, as shown in this statement that computes the area of a square:

```cpp
areaSquare = side*side;
```

Here the operator * is used to indicate multiplication. The operators + and − are used to indicate addition and subtraction, and the operator / is used for division. Thus, each of the following statements is a valid computation for the area of a triangle:

```cpp
areaTriangle = 0.5*base*height;
```

```cpp
areaTriangle = (base*height) / 2.0;
```
