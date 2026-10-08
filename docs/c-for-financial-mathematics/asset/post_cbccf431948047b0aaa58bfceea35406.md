
cout << c;

The compiler does perform some automatic casting, but in the wrong place! It guesses that you want the data to be cast as shown:

```cpp
int a = 3;
int b = 5;
double c = (double)(a / b);
cout << c;
```

To understand this, it is best to break it down into two parts: the calculation and then the cast. The code above is equivalent to:

```cpp
int a = 3;
int b = 5;
int divisionResult = 3 / 5;
double c = (double)divisionResult;
cout << c;
```

It should now be clear why the code fails. Two ways you can write the code so that it does what you want are:

```cpp
int a = 3;
int b = 5;
double c = ((double)a) / b;
cout << c;
```

and

```cpp
int a = 3;
int b = 5;
double aAsDouble = (double)a;
double c = aAsDouble / b;
cout << c;
```

The syntax we have used here for casting comes from C and so is called a C-style cast or an old-style cast. In C++ you can use an alternative notation for casting, which is called a C++-style cast or a new-style cast. Here is an example of a C-style cast to an integer:

```cpp
double pi = 3.141;
int piRoundedDown = (int)pi;
cout << piRoundedDown;
```

Here is an example of a C++-style cast:

```cpp
double pi = 3.141;
int piRoundedDown = static_cast<int>(pi);
cout << piRoundedDown;
```

In my view, the C++-style syntax is bulky to type and hard to read. However, many authors recommend using C++-style casts. In this book we will use C-style casts, if only to save space in printouts.

## 2.4 Memory addresses

Another data type which is important in the C language is a memory address, more commonly known as a pointer. Manipulating memory directly is just the kind of thing that CPUs are good at. The aim of the C language was to make it possible to write code that is similar to machine code in terms of performance but is easier for humans to read and write. For this reason, pointers are one of the basic data types in C. Since C++ contains C, pointers are a basic data type in C++ too.

However, our aim is to do mathematics and not to manipulate computer memory directly. For this reason we will try to avoid pointers wherever possible. We will only discuss them seriously in Chapter 11. Most C++ courses introduce pointers very early. As a result new programmers get the idea that they should use pointers a lot in their code too. However, an experienced C++ programmer knows that pointers are only an appropriate tool for solving problems involving direct memory access. We will rarely use them.

Nevertheless, for the sake of completeness we will give a brief outline of the concept now.

If you have a 32-bit computer, you can think of your memory as consisting of up to $2^{32}$ bytes of data. For 64-bit computers, simply replace the 32 with 64. We'll assume a 32-bit computer for the remainder of the discussion.

Each of these $2^{32}$ bytes is stored in a memory location. Each possible location is itself labelled with a number. This number is called the memory address and it takes a value between 0 and $2^{32} - 1$. Usually human beings aren't very interested in the precise value of a memory address, so they aren't often written down. But when one does write one out, it's normal to write them in hexadecimal. In hexadecimal we can say that a memory location is a number between 00000000 and FFFFFFFF. This helps to clearly distinguish memory locations from "normal" numbers.

A memory address is stored in C or C++ using a pointer data type. So you know what type of data is stored at that memory address, the pointer data type consists of two parts: the name of a data type that is pointed to and a * character. For example, if we write:

```cpp
double* dPointer = 0x00000000;
```

then we have just declared a variable of type **double\*** which means “a pointer to a double” or equivalently “a memory location containing a double”. We have specified the precise location that it points to, though it is extremely unusual to do this directly.

The one place where beginners are most likely to encounter a pointer is in so-called C-strings. Look at the following code:

```cpp
const char* speech = "To be or not to be?";
```

This creates a variable called **speech** which is of type **const char\***. The **char\*** means it is a pointer to a memory location containing a character. The **const** in front means that you can’t use the variable **speech** to change the text, only to read it.

The memory location that **speech** points to contains the first letter of the **speech** "T". The next memory location in sequence contains the letter "o". The text of the **speech** is stored in consecutive memory locations. To mark the end of the **speech**, the character code 0 is used. This is illustrated in Figure 2.1. In this example, the memory location associated with the text is AB102C02 as this is where the text starts.

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_49_0.png)

**FIGURE 2.1**: Text stored in memory and a pointer to the start of the text. The memory addresses are shown in hexadecimal.

Thinking of text in terms of pointers to memory locations is a pretty difficult way to work. It is strongly recommended that you avoid doing this in C++. Instead you should use the data type **string**. To use this you need to have the line

```cpp
#include <string>
```

near the top of the file with the other **#include** statements. You should also have the line

```cpp
using namespace std;
```

as usual. You can then create a variable of type **string** as follows:

```cpp
string speech = "To be or not to be?";
```

If nothing else this is easier to read than the version using `const char*`. Use `string` as your preferred way of storing text.

Technically a `string` is not a basic data type in C++. This is why you have to have write `#include <string>`. By default, only the basic data types are available in C++ unless you have an `#include` statement to indicate that you want to use a more complex data type.

We will talk at length about complex data types in this book. In fact, to some extent this book is about creating your own sophisticated data types in C++. We will create data objects to represent things such as options and market data.

### 2.5 Operators

#### 2.5.1 The `sizeof` operator

You can find the size (in bytes) of a data type using the `sizeof` operator. For example, the code

```cpp
size_t charSize = sizeof(char);
cout << "A char takes up ";
cout << charSize << " byte\n";
```

can be used to confirm that a `char` takes up one byte as claimed.

#### 2.5.2 Mathematical operations

You can perform various operations on numbers. We have already discussed `+`, `*`, `-` and `/`.

One other mathematical operator that you probably wouldn't think of is `%`. This is called the modulus operator. It computes the remainder on division. So, for example, `13 % 5` is 3.

We have also already seen that you can't raise a number to a given power using the `^` operator. Instead you must use the function `pow`.

This function is defined in the library called `cmath`. The statement

```cpp
#include <cmath>
```

at the beginning of all our programs means "we want to be able to use the functions in the cmath" library.

There are plenty of other functions in the `cmath` library, such as `sin`, `cos`, and so forth. The syntax for calling a function in C is the same as in mathematics.

```cpp
double x = 2.345;
```

```cpp
double y = sin(x) + cos(1.234);
cout << "The answer is " << y << "\n";
```

If a function requires two arguments, then, just as in mathematics, you separate the arguments with commas.

```cpp
cout << "The 32nd power of 2 is ";
cout << pow(2, 32);
cout << "\n";
```

The available functions in the cmath library are listed here: http://www.cplusplus.com/reference/cmath/.

#### 2.5.3 Comparison operators

C++ also contains operators for performing comparisons. We have already met `>`, `<`, `>=`, and `<=`. Also available is `==` (two equal signs) which is used to test if two numbers are equal and `!=` which is used to test if two numbers are different.

> **Danger!**
>
> Use two equal signs `==` to compare numbers not one equal sign. One equal sign is for *assignment*

#### 2.5.4 Logical operators

The result of a comparison operation is a `bool` representing either `true` or `false`. You can then combine `bool` values using the operators `&&`, `||`, and `!`, which mean and, or, and not, respectively.

So, for example, `true && false` evaluates to `false`.

#### 2.5.5 Bitwise operators

The operators `&`, `|`, `~`, `<<` and `>>` treat integers as simply binary data and perform manipulations on these bits.

-   `~` is the bit inversion operator. So `~x` contains binary representation of $x$ but with all the 1’s and 0’s switched.
-   `<<` shifts all the bits in a number to the left by a given amount. So `x<<3` shifts all the bits 3 steps to the left.
-   `>>` shifts all the bits in a number to the right by a given amount. So `x>>3` shifts all the bits 3 steps to the right.
