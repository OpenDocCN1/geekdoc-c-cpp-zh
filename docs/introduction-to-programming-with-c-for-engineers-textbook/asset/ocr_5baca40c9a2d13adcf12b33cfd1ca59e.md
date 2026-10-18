On line [91], the input integer `val` is checked to see if it is greater than 1. If so, `ToBinConvert` is called recursively on line [92], but its argument is divided by 2. To avoid costly divisions, a much faster right shift operator `>>`, shifting by one place, is applied (GROUP 7, Table 3.15). But when recursion ends due to `val` being equal to 1, all the recursive calls return, launching `printf` on line [94]. This, in turn, outputs “0” or “1” depending on the last bit of `val` from its call time.

When we call this simple example, the following appears in the terminal window:

```
D:\BC++\Projects\CPro\build_win\Debug>CPro 2019 bin
Value converter. Calling format:
CPro.exe dec_val [bin,oct,hex]
2019 [dec] = 11111100011 [bin]
Press any key to continue . . .
```

# A.2.3  C Structures

The main difference when using C, as opposed to C++, is that functions are totally separate from structures, which contain only publicly accessible data. The second difference is that there is no automatic mechanism for initializing that data in structures: i.e. there are no constructors, since there are no functions inside the C structures. Finally, in C, structures cannot inherit since there is no inheritance mechanism. On the other hand, C structures can contain other C structures, so a composite relation can exist.

To understand the differences, let’s analyze the following example. It implements a representation of the quadratic equation and a few associated functions for its initialization and basic computations.

```
Listing A.2  Definitions of the QE structure to hold coefficients of a quadratic equation in the C language (in CPro, struct_test.c).

1   /* Simple struct to store coeffs of the quadratic equation */
2   struct QE
3   {
4       float a, b, c;
5   };
6
7   /* struct QE is a tag, and we need to introduce the type QE */
8   /* The name of a struct is a tag, rather than the type. */
9   typedef     struct QE       QE;
```

A structure QE is defined on lines [2–5]. It contains three variables a, b, and c. However, unless this is a static or global object, there is no way to impose an automatic initialization of data members when an instance of QE is created. Also, there is no mechanism for disposing or deallocating memory when QE is destroyed. In addition, it is not possible to define a function inside a `struct`, although function pointers are accepted. Moreover, `struct QE` in C is only a tag. To introduce a full type QE, the typedef construction is needed, as shown on line [9].

Finally, there is no way to inherit from a `struct`, although `struct`s can be nested. Compared with C++, these are the fundamental differences that greatly affect the way software is designed, as discussed in Section A.4.