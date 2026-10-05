
## 2 Variables, Constants, and Arithmetic Conversions

TABLE 2.1 Data types
| DATA TYPE | USUAL SIZE (BYTES) | RANGE OF VALUES (MIN-MAX) |
| --- | --- | --- |
| bool | 1 | false/true |
| char | 1 | -128 ... 127 |
| wchar_t | 2 | -32.768 ... 32.767 |
| short int | 2 | -32.768 ... 32.767 |
| int | 4 | -2,147,483,648...2,147,483,647 |
| long int | 4 | -2,147,483,648...2,147,483,647 |
| float | 4 | Lowest positive: 1.17*10^-38 Highest positive: 3.2*10^38 |
| double | 8 | Lowest positive: 1.22*10^-308 Highest positive: 1.8*10^308 |
| long double | 12, 16 | 0 ... 255 |
| unsigned char | 1 | 0 ... 65535 |
| unsigned short int | 2 | 0 ... 4,294,967 |
| unsigned long int | 4 | 0 ... 4,294,967 |

The char, short, int, and long types are used to store integer values, which can be either signed or unsigned. If we use unsigned the variable has no sign bit and it may store only positive values or zero. The word int can be omitted. For example, long instead of long int. Also the words can be mixed in any order. For example, the declaration unsigned long int a; is the same as int unsigned a.

With the exception of the char type, all other types are signed by default. In signed types, the most bit is reserved for the sign. If the value is negative it is 1, otherwise. The advantage of using unsigned types is that they have a upper limit than their signed counterparts, since they don't need to account for negative values.

Characters are represented by specific numeric codes. The char type is typically used to store the numeric codes of the characters of the basic character set, such as the ASCII set (e.g., it includes characters that appear on the keyboard such as digits, letters, punctuation marks, ...). The wchar_t type is used to store the numeric codes of the characters of a larger character set, such as the Unicode.

The char type may be signed or unsigned, it is implementation dependent. Therefore, if it is important for your program, you should explicitly write signed char or unsigned char instead of char.

```
char a = 255;
int b = a;
```

the value of b is unsigned. In one system the char type is signed b becomes -1, while in another where the char type is unsigned b converts to value and false converts to 0. Conversely, non-zero values convert to true, whereas a zero value converts to false. For example:

```
bool b = 2; // b becomes true.
int i = false; // i becomes 0.
```

Typically, a bool variable is used to store the result of an action, such as whether a value is found in an array or not.

## 14 Introduction to C++

The float, double, and long double types are used to store values with a fractional part, that is, floating-point numbers; floating-point types are always signed. Although the long double normally provides the highest precision, it is rarely used because the precision of the float and double types is usually sufficient.

Although C++ each implementation sets its own sizes for the data types, it places restrictions on their memory. The size of the char must be at least 8 bits, the size of the short is at least 16 bits, and the size of the int at equal to that of the short. The size of the long must be at least 32 bits and at least equal to that of int. The following order applies: sizeof(char) <= sizeof(short) <= sizeof(int) <= sizeof(long). The size of the wchar depends on the implementation; however, it applies: sizeof(wchar_t) <= sizeof(long). If it is important to save many values the fit, use short instead of int, because its size is usually smaller.

For floating-point types, C++ specifies that the size of the long double must be at least that of the double, and the size of the double type must be at least that of the float. If want to learn the sizes of the int and floating-point types that your system uses the sizeof operator. If you want to find out more about the type limits, read the limits and cfloat header files. Also, you can use the limit file and get type information. For the next statement displays the maximum value of the int type:

```
std::cout << "Max value of type int is " << std::numeric_limits<int>::max();
```

To get the minimum value we replace max() with min(). If you want to get the maximum values for other data types, replace the int in the angle brackets with the desired.

> If you don't care about precision use the float type, because it reserves less bytes and calculations with float numbers tend to be executed faster.

Let's run the following program. The == operator in the if statement compares the value of a against 3.1. What do you think the program will display, Yes or No?

```
#include <iostream> // Example 2.1.
int main() {
    float a = 3.1;
    if(a == 3.1)
        std::cout << "Yes\n";
    else
        std::cout << "No\n";
}
```

Although the obvious answer is Yes, did the program output NO? Surprise! And the reason is due to the limited capacity of the float type to represent precisely the number 3.1. As'll see later, by default, the type of a float constant (e.g., 3.1) is double.

When using floating-point variables in comparisons, it is safer to declare them as double or long double rather than float. If you use these types, the program would probably display Yes. But in general, when you test the value of a floating-point variable for equality, you never be sure about the comparison, as there is a possibility that the number cannot be represented with the accuracy of the type. If it can be represented, the result of the comparison is valid. For example,

## 2 • Variables, Constants, and Arithmetic Conversions 15

## Variables, Constants, and Arithmetic Conversions

For simplicity, I've made some assumptions throughout this book. I assume that the type supported by the compiler are shown in Table 2.1, that one byte contains eight bits (yes, it can have more), and the system uses the most common method to represent signed numbers, which is two's complement. Also, I assume that the underlying character set is the ASCII set. When using floating-point values in our program, we'll use float and double types, in order to get familiar with both types.

Before ending this section, I want to point out that C++ static type control in the sense that the validity of you types is done during compilation and. Later in this book we will see that we use the basic types to create other types (e.g., pointers) over operators. We'll also learn to create our types, such as structures and classes.

## Declaring Variables

Variables must be declared before used in the program. The declaration informs the compiler about the name of the variable and its type. We've already seen some examples of declarations in the previous section. To declare a variable we:

```
data_type variable_name;
```

The variable_name is the name of the variable and the data_type its type. As we said, C++ is a statically typed language, in the sense that the compiler must know the type of every entity (e.g., variable) at the point of its use. The type of entity determines the operations we can perform on it. For example, to declare an integer variable named i and a floating-point variable named j, we:

```
int i;
float j;
```

Variables of the same type can be declared in the same line, separated by a comma. For example, instead of declaring the variables i, j, and k in three different lines:

```
int i;
int j;
int k;
```

we can declare them in the same line and save space: int i, j, k;
