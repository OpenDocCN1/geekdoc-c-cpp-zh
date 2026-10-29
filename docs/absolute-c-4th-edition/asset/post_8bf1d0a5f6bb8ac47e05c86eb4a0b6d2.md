
## 1. 引言

本文档旨在介绍一种基于深度学习的图像识别方法，该方法在多个标准数据集上取得了优异的性能表现。

## 2. 相关工作

近年来，卷积神经网络（CNN）在计算机视觉领域取得了显著进展。本文方法基于ResNet架构，并引入了注意力机制。

- 方法一：基于区域的目标检测
- 方法二：基于回归的目标检测
- 方法三：基于Transformer的目标检测

## 3. 方法

我们提出了一种端到端的训练框架，整体流程如下图所示。

![](img/9505fd46e120aa9c1406715936ff6251_461_0.png)

| 数据集 | 准确率 | 参数量 |
|--------|--------|--------|
| CIFAR-10 | 97.2% | 1.2M |
| ImageNet | 91.5% | 25.6M |

> 实验结果表明，该方法在准确率和效率之间取得了良好的平衡。

These helping functions readHour and readMinute use another helping function named digitToInt. The function digitToInt converts a digit, such as '3', to a number, such as 3. This function was given previously in this book as the answer to Self-Test Exercise 3 in Chapter 7.

### Tip: REUSABLE COMPONENTS

A class developed and coded into separate files is a software component that can be used again and again in a number of different programs. A reusable component saves effort because it does not need to be redesigned, recoded, and retested for every application. A reusable component is also likely to be more reliable than a component that is used only once. It is likely to be more reliable for two reasons. First, you can afford to spend more time and effort on a component if it will be used many times. Second, if the component is used again and again, it is tested again and again. Every use of a software component is a test of that component. Using a software component in many times in a variety of contexts is one of the best ways to discover any remaining bugs in the software.

### USING #ifndef

We have given you a method for placing a program in three (or more) files: two for the interface and implementation of each class and one for the application part of the program. A program can be kept in more than three files. For example, a program might use several classes, and each class might be kept in a separate pair of files. Suppose you have a program spread across a number of files and that more than one file has an include directive for a class interface file such as the following:

```
#include "dtime.h"
```

Under these circumstances you can have files that include other files, and these other files may in turn include yet other files. This can easily lead to a situation in which a file, in effect, contains the definitions in dtime.h more than once. C++ does not allow you to define a class more than once, even if the repeated definitions are identical. Moreover, if you are using the same header file in many different projects, it becomes close to impossible to keep track of whether you included the class definition more than once. To avoid this problem, C++ provides a way of marking a section of code to say "if you have already included this stuff once before, do not include it again." The way this is done is quite intuitive, although the notation may look a bit weird until you get used to it. We will go through an example, explaining the details as we go.

The following directive defines DTIME_H:

```
#define DTIME_H
```

DTIME_H is not defined to mean anything but merely put on a list. The important point is that you can use another directive to test whether DTIME_H has been defined and so test whether a section of code has already been processed. You can use any (nonkeyword) identifier in place of DTIME_H, but you will see that there are standard conventions for which identifier you should use.

The following directive tests to see whether DTIME_H has been defined:

```
#ifndef DTIME_H
```

If DTIME_H has already been defined, then everything between this directive and the first occurrence of the following directive is skipped:

```
#endif
```

An equivalent way to state this, which may clarify the way the directives are spelled, is the following: If DTIME_H is not defined, then the compiler processes everything up to the next #endif. The not is why there is an n in #ifndef. (This may lead you to wonder whether there is a #ifdef directive as well as a #ifndef directive. There is, and it has the obvious meaning, but we will have no occasion to use #ifdef.)

Now consider the following code:

```
#ifndef DTIME_H
#define DTIME_H
< a class definition >
#endif
```

If this code is in a file named dtime.h, then no matter how many times your program contains

```
#include "dtime.h"
```

In Display 11.4 we have rewritten the header file dtime.h shown in Display 11.1, but this time we used these directives to prevent multiple definitions. With the version of dtime.h shown in Display 11.4, if a file contains the following #include directive more than once, the class DigitalTime will still be defined only once:

```
#include "dtime.h"
```

You may use some other identifier in place of DTIME_H, but the normal convention is to use the name of the file written in all uppercase letters with the underscore used in place of the period. You should follow this convention so that others can more easily read your code and so that you do not have to remember the flag name. This way the flag name is determined automatically and there is nothing arbitrary to remember.

These same directives can be used to skip over code in files other than header files, but we will not have occasion to use these directives except in header files.

### #ifndef

You can avoid multiple definitions of a class (or anything else) by using #ifndef in the header file (interface file), as illustrated in Display 11.4. If the file is included more than once, only one of the definitions included will be used.

**Display 11.4 Avoiding Multiple Definitions of a Class**

```
1 //This is the header file dtime.h. This is the interface for the class DigitalTime.
2 //Values of this type are times of day. The values are input and output in
3 //24-hour notation, as in 9:30 for 9:30 AM and 14:45 for 2:45 PM.
4
5 #ifndef DTIME_H
6 #define DTIME_H
7
8 #include <iostream>
9 using namespace std;
10
11 class DigitalTime
12 {
13     <The definition of the class DigitalTime is the same as in Display 11.1.>
14
15 };
16
17 #endif //DTIME_H
```

### Tip: DEFINING OTHER LIBRARIES

You need not define a class in order to use separate compilation. If you have a collection of related functions that you want to make into a library of your own design, you can place the function declarations (prototypes) and accompanying comments in a header file and the function definitions in an implementation file, just as we outlined for classes. After that, you can use this library in your programs the same way you would use a class that you placed in separate files.

### Self-Test Exercises

- 1. Suppose that you are defining a class and that you then want to use this class in a program. You want to separate the class and program parts into separate files as described in this chapter. State whether each of the following should be placed in the interface file, implementation file, or application file.

  - a. The class definition
  - b. The declaration for a function that is to serve as a class operation but that is neither a member nor a friend of the class
  - c. The declaration for an overloaded operator that is to serve as a class operation but that is neither a member nor a friend of the class
  - d. The definition for a function that is to serve as a class operation but that is neither a member nor a friend of the class
  - e. The definition for a friend function that is to serve as a class operation
  - f. The definition for a member function
  - g. The definition for an overloaded operator that is to serve as a class operation but that is neither a member nor a friend of the class
  - h. The definition for an overloaded operator that is to serve as a class operation and that is a friend of the class
  - i. The main function of your program

- 2. Which of the following files has a name that ends in .h: the interface file for a class, the implementation file for the class, or the application file that uses the class?

- 3. When you define a class in separate files, there is an interface file and an implementation file. Which of these files needs to be compiled? (Both? Neither? Only one? If so, which one?)

- 4. Suppose you define a class in separate files and use the class in a program. Now suppose you change the class implementation file. Which of the following files, if any, needs to be recompiled: the interface file, the implementation file, and/or the application file?
