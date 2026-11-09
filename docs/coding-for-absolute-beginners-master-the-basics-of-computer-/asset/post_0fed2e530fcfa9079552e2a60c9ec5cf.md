
```c
#include <stdio.h>
struct Distance
{
    int feet;
    float inch;
} dist1, dist2, sum;
int main()
{
    printf("1st distance\n");
    printf("Enter feet: ");
    scanf("%d", &dist1.feet);
    printf("Enter inch: ");
    scanf("%f", &dist1.inch);
    printf("2nd distance\n");
    printf("Enter feet: ");
    scanf("%d", &dist2.feet);
    printf("Enter inch: ");
    scanf("%f", &dist2.inch);

    sum.feet = dist1.feet + dist2.feet;

    sum.inch = dist1.inch + dist2.inch;

    while (sum.inch >= 12)
    {
        ++sum.feet;
        sum.inch = sum.inch - 12;
    }
    printf("Sum of distances = %d' - %.1f\"", sum.feet, sum.inch);
    return 0;
}
```

```
1st distance
Enter feet: 5
Enter inch: 9
2nd distance
Enter feet: 6
Enter inch: 3
Sum of distances = 12'-0.0"

...Program finished with exit code 0
Press ENTER to exit console.
```

### Passing Pointers to Structures

We can also define a pointer to a structure in the C programming language, which is done in the same manner as defining a pointer to another variable. In order to access the members of a structure through a pointer, the following syntax can be considered:

```c
Struct_pointer->title;
```

### C Programming files

Programming requires developers to handle different requirements and scenarios by using the most effective approaches. To perform file handling operations in C language, we can use the operations as follows:

- `fprintf()`
- `fscanf()`
- `fread()`
- `fwrite()`
- `fseek()`

Generally, the entire data is lost when a program is terminated, for which we have to create a specific file containing all of the data. It also saves time and lets the programmer access data from the file by entering a few commands and transferring the data from one computer to another through C language operators.

There are two types of files known as Text files and Binary files. Text files are `.txt` files that can be created by using Notepad and require minimum effort to write, maintain, and update the record. Binary files are `.bin` files and they store the data in the binary form of 0s and 1s. Furthermore, binary files can store a bigger amount of data compared to text files.

In the C programming language, we can create a new file, open an existing file, read from and write information to a file, and close a file through simple commands mentioned in the following table:

| Operation | Syntax |
|---|---|
| Opening a file | `ptr = fopen("fileopen", "mode")` |
| Closing a file | `fclose(fptr);` |
| Write to binary file | `fwrite(address_data, size_data, numbers_data, pointer_to_file);` |
| Read from binary file | `fread(address_data, size_data, numbers_data, pointer_to_file);` |
| Write to text file | `FILE *fptr; fptr = fopen("File address", "w");` |
| Read from text file | `FILE *fptr; fptr = fopen("File address", "r");` |
| File Seek | `fseek(FILE *stream, long int offset, int whence)` |

### Essential Tips to Make C Programming Easy

For beginners, it is advised that they always comment their code by writing vital code information between `/*` and `*/`. Commenting on the major part of your code can also make it easier to make future changes and improve the functionality of the program. Furthermore, always use variables to store data such as `int`, `char`, and `float` because it will make it simpler for you to perform different operations and calculations.

C language is simple and fast. With the availability of pointers, keywords, and bitwise operators, writing efficient code will surely not be a problem for beginners.

![](img/9d932bec53e523b8d8b7b8134cf77ca7_63_0.png)

## CHAPTER FIVE

## C++

C++ is a free-form and intermediate-level programming language that was developed by Bjarne Stroustrup in 1979. Being an enhanced version of the C programming language, C++ has now become the most used and best-suited language for beginners. The language delivers about 7 different styles of programming and you can choose the most suitable style as per your requirements. Being a statically typed programming language, C++ allows the compiler to outline errors or bugs before executing the program. Moreover, Object-Oriented Programming with C++ makes it convenient to solve complex problems and extends the usage of standard libraries as well. C++ is the world's most popular programming language and is widely used with Graphical User Interfaces, Operating Systems and Embedded Systems as well.

### Basic Syntax

The basic syntax for C++ programming language is the same as other languages such as C. Including various words, symbols, characters, operations, and expressions, the programmer must follow a predefined set of rules to execute the program properly.

Here is the first program we can write to get started with C++:

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"My First Program in C++";
    return 0;
}
```

Program Output: My First Program in C++.

![](img/9d932bec53e523b8d8b7b8134cf77ca7_64_0.png)

The details of the program are as follows:

- **`#include<iostream>`** = The statement contains predefined input and output functions and informs the compiler to include the iostream file as well.
- **`using namespace std;`** = A statement used to store the functions, variables, and operations within the program whereas std is considered as a namespace name.
- **`int main()`** = This is the main function of the program from where the execution begins. `int` is a return type and indicates to the compiler to return an integer value for which we also have to include a `return 0` statement at the end.
- **`cout << "My First Program in C++"`** = `cout` is an object that belongs to the iostream file and is used to display the content.
- **`return 0;`** = The statement returns value 0 from main() function and is responsible for the execution of the main function as well.

### Variables and Data Types

#### Variables

There are different types of variables in C++ programming language. As they are defined with a specific keyword, we must create a variable, specify the type, and assign the value by following the syntax as given below:

```cpp
Type variable = value;
```

##### Types of variables

- `int` = Used to store integers and whole numbers. For example, 1, 45, 6346.
- `char` = Used to store single characters. For example, `'a'` or `'Z'`.
- `double` = Used to store floating point numbers. For example, 50.2, 100.2342.
- `bool` = Used to store a value with two states: `true` or `false`.
- `string` = Used to store text. For example, `"C++ programming language"`.

To declare and assign a value to a variable, we can follow the syntax as mentioned below:

```cpp
int newNum;
newNum = 50;
cout << newNum;
```

Every variable that is being used in C++ should be identified with unique names which are known as identifiers. To construct identifiers, names must contain letters, digits, or underscores and are case-sensitive as well.

#### Data Types

Data types in the C++ programming language define the type of data that can be stored in a variable. Generally, the data types in C++ are classified into three groups: built-in, derived, and user-defined. The user-defined data type includes structures, union, and enum whereas the derived data type is based on array, function, and pointer.

Built-in data types for C++:

- `int`
- `char`
- `float`
- `double`
- `bool`

User-defined data types:

- `union`
- `enum`
- `struct`

Derived data types:

- function
- array
- pointer

### Modifier Types and Storage Classes

Modifiers in C++ programming language are used with `char`, `double`, and `int` data types to change the meaning of base type in order to meet certain programming conditions. These modifiers include `signed`, `unsigned`, `long`, and `short`.

To define the scope of variables and functions within a C++ program, we can use storage classes such as `auto`, `register`, `extern`, `mutable`, and `static`. The `auto` storage class is default for all local variables whereas the `static` storage class allows the compiler to store a local variable during the lifetime of the program and destroy it whenever it goes out of scope.

The external storage class gives a reference to a global variable and is used when there are two or more files using the same global functions or variables. For the `mutable` storage class, only class objects are considered and they can also be modified by a constant member function as well.

### Flow Control

In C++ programming, control flow is referred to as the order in which instructions, functions, and statements are being evaluated and executed.
