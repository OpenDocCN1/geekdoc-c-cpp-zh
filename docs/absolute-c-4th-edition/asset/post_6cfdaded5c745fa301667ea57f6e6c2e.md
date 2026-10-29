
# PROGRAMMING PROJECTS

+   1. Reread the code in Display 10.9. Then, write a class TwoD that implements the two-dimensional dynamic array of doubles using ideas from this display in its constructors. You should have a private member of type pointer to double to point to the dynamic array, and two int (or unsigned int) values that are MaxRows and MaxCols.
+   
+   You should supply a default constructor for which you are to choose a default maximum row and column sizes and a parameterized constructor that allows the programmer to set maximum row and column sizes.
+   
+   Further, you should provide a void member function that allows setting a particular row and column entry and a member function that returns a particular row and column entry as a value of type double.
+   
+   Remark: It’s difficult or impossible (depending on the details) to overload [] so it works as you would like for two-dimensional arrays. So simply use accessor and mutator functions using ordinary function notation.
+   
+   Overload the + operator as a friend function to add two two-dimensional arrays. This function should return the TwoD object whose ith row, jth column element is the sum of the ith row, jth column element of the left-hand operand TwoD object and the ith row, jth column element of the right-hand operand TwoD object.
+   
+   Provide a copy constructor, an overloaded operator=, and a destructor.
+   
+   Declare class member functions that do not change the data as const members.

![](img/9505fd46e120aa9c1406715936ff6251_448_0.png)

+   2. Using dynamic arrays, implement a polynomial class with polynomial addition, subtraction, and multiplication.

![](img/9505fd46e120aa9c1406715936ff6251_448_1.png)

Discussion: A variable in a polynomial does nothing but act as a placeholder for the coefficients. Hence, the only interesting thing about polynomials is the array of coefficients and the corresponding exponent. Think about the polynomial

x*x*x*x + x + 1

Where is the term in x*x? One simple way to implement the polynomial class is to use an array of doubles to store the coefficients. The index of the array is the exponent of the corresponding term. If a term is missing, then it simply has a zero coefficient.

There are techniques for representing polynomials of high degree with many missing terms. These use so-called sparse matrix techniques. Unless you already know these techniques, or learn very quickly, don’t use these techniques.

Provide a default constructor, a copy constructor, and a parameterized constructor that enables an arbitrary polynomial to be constructed.

Supply an overloaded operator = and a destructor.
Provide these operations:
polynomial + polynomial, constant + polynomial, polynomial + constant,
polynomial – polynomial, constant – polynomial, polynomial – constant.
polynomial * polynomial, constant * polynomial, polynomial * constant.
Supply functions to assign and extract coefficients, indexed by exponent.
Supply a function to evaluate the polynomial at a value of type double.
You should decide whether to implement these functions as members, friends, or stand-alone functions.

For additional online Programming Projects, click the CodeMate icons below.
1.7

![](img/9505fd46e120aa9c1406715936ff6251_449_0.png)

then you need only recompile the file containing the class implementation. The other files, including the files containing the programs that use the class, need not be changed or even recompiled. This section tells you how to carry out this separate compilation of classes.

# ENCAPSULATION REVIEWED

The principle of encapsulation says that you should separate the specification of how the class is used by a programmer from the details of how the class is implemented. The separation should be so complete that you can change the implementation without needing to change any program that uses the class. The way to ensure this separation can be summarized in three rules:

+   1. Make all the member variables private members of the class.

+   2. Make each of the basic operations for the class either a public member function of the class, a friend function, an ordinary function, or an overloaded operator. Group the class definition and the function and operator declarations (prototypes) together. This group, along with its accompanying comments, is called the interface for the class. Fully specify how to use each such function or operator in a comment given with the class or with the function or operator declaration.

+   3. Make the implementation of the basic operations unavailable to the programmer who uses the class. The implementation consists of the function definitions and overloaded operator definitions (along with any helping functions or other additional items these definitions require).

In C++, the best way to ensure that you follow these rules is to place the interface and the implementation of the class in separate files. As you might guess, the file that contains the interface is often called the interface file, and the file that contains the implementation is called the implementation file. The exact details of how to set up, compile, and use these files will vary slightly from one version of C++ to another, but the basic scheme is the same in all versions of C++. In particular, the details of what goes into the files is the same in all systems. The only things that vary are the commands used to compile and link these files. The details about what goes into these files are illustrated in the next subsection.

A typical class has private member variables. Private member variables (and private member functions) present a problem to our basic philosophy of placing the interface and the implementation of a class in separate files. The public part of the definition for a class is part of the interface for the class, but the private part of the implementation. This is a problem because C++ will not allow you to split the class definition across two files. Thus, some sort of compromise is needed. The only sensible compromise is to place the entire class definition in the interface file. Since a programmer who is using the class cannot use any of the private members of the class, the private members will, in effect, still be hidden from the programmer.

# ### 1.2 矩阵的运算

矩阵的运算包括矩阵的加法、数乘、乘法、转置、共轭转置、逆矩阵等。本节主要介绍矩阵的加法、数乘、乘法、转置和共轭转置等基本运算，逆矩阵将在1.4节中介绍。

# #### 1.2.1 矩阵的加法与数乘

定义1.2.1 设A=(a_ij)和B=(b_ij)都是m×n矩阵，则矩阵A与B的和定义为

A+B=(a_ij+b_ij)

即两个同型矩阵的和等于对应元素相加所组成的矩阵。

设k为一个数，则数k与矩阵A的乘积定义为

kA=(ka_ij)

即数乘矩阵等于用该数乘以矩阵的每一个元素。

矩阵的加法与数乘统称为矩阵的线性运算。

设A、B、C都是m×n矩阵，k、l为数，则矩阵的线性运算满足以下运算规律：

+   1. 交换律：A+B=B+A
+   2. 结合律：(A+B)+C=A+(B+C)
+   3. 零矩阵：A+O=A
+   4. 负矩阵：A+(-A)=O
+   5. 数乘结合律：k(lA)=(kl)A
+   6. 分配律：k(A+B)=kA+kB
+   7. 分配律：(k+l)A=kA+lA
+   8. 数乘单位元：1A=A

# Display 11.1  Interface File for the DigitalTime Class

```
//This is the header file dtime.h. This is the interface for the class DigitalTime.
//Values of this type are times of day. The values are input and output in 24-hour
//notation, as in 9:30 for 9:30 AM and 14:45 for 2:45 PM.
#include <iostream>
using namespace std;

class DigitalTime
{
public:
    DigitalTime(int theHour, int theMinute);
    DigitalTime();
    //Initializes the time value to 0:00 (which is midnight).

    int getHour( ) const;
    int getMinute( ) const;
    void advance(int minutesAdded);
    //Changes the time to minutesAdded minutes later.

    void advance(int hoursAdded, int minutesAdded);
    //Changes the time to hoursAdded hours plus minutesAdded minutes later.

    friend bool operator ==(const DigitalTime& time1,
                            const DigitalTime& time2);

    friend istream& operator >>(istream& ins, DigitalTime& theObject);

    friend ostream& operator <<(ostream& outs, const DigitalTime& theObject);
private:
    int hour;
    int minute;

    static void readHour(int& theHour);
    //Precondition: Next input to be read from the keyboard is
    //a time in notation, like 9:45 or 14:45.
    //Postcondition: theHour has been set to the hour part of the time.
    //The colon has been discarded and the next input to be read is the minute.

    static void readMinute(int& theMinute);
    //Reads the minute of the keyboard after readHour has read the hour.

    static int digitToInt(char c);
    //Precondition: c is one of the digits '0' through '9'.
    //Returns the integer for the digit; for example, digitToInt('3') returns 3.
};
```

![](img/9505fd46e120aa9c1406715936ff6251_454_0.png)
