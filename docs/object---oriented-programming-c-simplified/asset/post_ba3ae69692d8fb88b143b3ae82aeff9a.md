
## 1. Built-in Type
- (a) Integral Type
    - (i) int
    - (ii) char
- (b) Floating Types
    - (i) float
    - (ii) double
- (c) void
- (d) bool
- (e) wchar_t

## 2. User Defined Data Type
- (a) class
- (b) struct
- (c) union
- (d) enumeration

## 3. Derived Data Types
- (a) array
- (b) function
- (c) pointer
- (d) reference

wchar_t is a new data type which supports long characters. The wchar_t keyword designates a wide-character type. The wchar_t type is defined as an unsigned short (16-bit) data object.
A wchar_t constant can be declared by preceding L before it as L"abc", L'a'. To use this data type you must include header file wchar.h.

## 2.7 QUALIFIERS

Qualifiers qualify the meaning of data types. Unsigned, signed, short and long are the 4 qualifiers available in C++. The manner in which they are used as follows :

```
signed int x, y, b;
unsigned int p,q;
long int num;
short int n;
```

long int is a data type as mentioned earlier and short int is same as signed int or simply int on most of the C++ compilers. Signed qualifier is used where we want to work with both positive and negative values. Unsigned qualifier can be used where we want with only positive values. They can be used only with char and integer data types. The available range increases in positive when we use unsigned say for example, range of signed char or simply char −128

to 127 where as for unsigned char it is 0 to 255. Same holds for int/ or long int. Apart from these two important keywords are also used as qualifiers const and volatile. The const qualifier is used to declare a variable as a constant for example, const int x=10; declare a constant x of type int with constant value. For more about constant see in the next chapter.

## 2.8 RANGE OF DATA TYPES

Table 2.5 : Data Type and Their Range

| S.No. | Data Type | Size(in byte) | Range |
|---|---|---|---|
| 1 | int or short | 2 | −32768 to 32767 |
| 2 | Unsigned int | 2 | 0 to 65535 |
| 3 | Long int | 4 | −2147483648 to 2147483647 |
| 4 | Float | 4 | 3.4e-38 to 3.4e+38 |
| 5 | Char | 1 | −128 to 127 |
| 6 | Unsigned char | 1 | 0 to 255 |
| 7 | Unsigned long | 4 | 0 to 4294967295 |
| 8 | Double | 8 | 1.7e-308 to 1.7e+308 |
| 9 | Long double | 10 | 3.4e-4932 to 3.4e+4932 |

For the calculation of range of data types we have a fixed formula :

- 1. For a signed data types if it takes n bits in memory then the range of values a particular variable of this data type can take is
    - −2^(n-1) to 2^(n-1) − 1
    - Example : for n=16(int) the range is
    - −2^15 to 2^15 −1
    - And for char data type n=8 the range is
    - −2^7 to 2^7−1

- 2. For an unsigned data types if it takes n bits in memory then the range of values a particular variables of this data type can take is
    - 0 to 2^n−1
    - For example, for n=16 (unsigned short int) the range is 0 to 2^16−1 and for unsigned char data type n=8 the range is 0 to 2^8−1.

## 2.9 YOUR FIRST C++ PROGRAM

```
/*PROG 2.1 PRINTS HELLO C++ ON THE SCREEN */

#include <iostream.h>
int main()
{
    cout << " Hello C++";
    return 0;
}

OUTPUT :
Hello C++
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_48_0.png)

Figure 2.3. Output screen of program 2.1.

EXPLANATION: In the first line #include is a preprocessor directive, iostream.h is a header file which is written enclosed in < and > or in "". "io" in iostream stands for input output, .h stands for header file. The file iostream.h has to be included in every C++ program. There may be space between #include and <iostream.h>. Next line is the function main () due to symbol () which is known as function symbol. This function must be present in every C++ file you make because execution of your C++ program starts from this main (). {is the opening braces for main function and } is the closing brace. All the statements, instructions are written inside the main function. The int before main is treated as its return type. cout is the predefined object of class iostream_withassign which is defined in iostream.h. The symbol << is an operator known as put to or insertion operator. The combined effect of cout << is that whatever is written after it is in double quotes is printed onto the screen, so the output. Every statement in a C++ program has to end with; (semicolon). C++ is case sensitive programming language, so whatever you use that is in-built in C++ has to be in lower case. The line return 0; is simply for the omission of warning. If you do not write return 0; you will not get any error but a warning. The above program can be modified as (with a little change in return type of function main).

```
void main()
{
    cout << "Hello C++";
}
```

### 2.9.1 Compilation and Execution Process

To run your first program in Windows environment follow the following steps.

- 1. In the Visual Studio 6.0 open Microsoft Visual C++ 6.0.
- 2. In the IDE select new from file.
- 3. Under Project tab select option win 32 Console Application and give project name say “CPP”. Choose location where you want to put your project say D:\. In the project all your files will be saved.

![](img/ad5299318df8d4d7c6df5eaa86590ea3_49_0.png)

Figure 2.4

4. Click Finish. A new dialog box will appear, simply press OK. At this step you have successfully made a new project CPP under D:\.

![](img/ad5299318df8d4d7c6df5eaa86590ea3_49_1.png)

Figure 2.5

5. Now select new from file. Select Files tab and option C++ source file. Give a suitable file name say first. Press OK.

![](img/ad5299318df8d4d7c6df5eaa86590ea3_50_0.png)

Figure 2.6

6. A new window will appear. Type the above program in the window as it.

7. From the build menu select build CPP.exe option. Assuming no error in the program a new window will appear at the bottom showing 0 error 0 warnings.

![](img/ad5299318df8d4d7c6df5eaa86590ea3_50_1.png)

Figure 2.7

After a day’s work when you want to open your same project simply looks for file with .dsp extension which stands for **data source project**. After wards you can continue making C++ programs.

## 2.10 STRUCTURE OF A C++ PROGRAM

The general structure of any C++ program is given below. It simply states that a standard C++ program may look like according to various sections presents in the structure.

|  |
|---|---|
| Documentation |
| Header file |
| Symbolic Constants |
| Global variables, functions |
| Class declaration |
| Member function definition |
| main()
{
  ....................;
  ....................;
} |
| Global function definition |

Figure 2.10. General structure of a C++ program.

- - The first section Documentation is optional and is used to put comments for the program usually the program heading as we have given.
- - In second section we include various header files required by our C++ program.
- - Symbolic constants and global variable, functions are defined after that if required.
- - The class, main building block of C++ programming is declared which consists of declaration of data members and functions. The member function may be declared and defined in the class or they are declared in the class but defined outside the class which is done outside the class declaration.
- - The **main()** function must be present in every C++ program. It contains all the statements which are to be executed. Inside this main function we create objects of class created earlier. All statements are put inside the braces and terminate with semicolon.

A full fledge C++ program is given below. Don't worry if you do not understand extra stuff at this point. This is just to give you idea of structure of a C++ program.

```
/*Documentation*/
/* DEMO PROGRAM FOR C++ STRUCTURE, DOES NOT SERVE ANY PURPOSE EXCEPT DEMONSTRATION */

#include <iostream.h> /*header file inclusion */
#include <iomanip.h>
```

```
int x;float y; char z; /* global variables */
void disp(); /* global function */
/*class declaration starts here */
class demo
{
private :
    int x, y;
public :
    void input(int a, int b);
    void show();
};
/*class declaration ends here */
/*class function definition */
void demo ::input(int a, int b)
{
    x = a;
    y = b;
}
/*class function definition */
void demo ::show()
{
    cout << "x=" << x << endl;
    cout << "y=" << y << endl;
}
void main() /*main function definiton */
{
    demo d1,d2; //creating objects
    d1.input(10,20);
    ..............;
    ..............;
    d1.show();
    int num;
    show(); //local function call
}
/*global function definitions */
void show()
{
    cout << "in show" << endl;
}
```
