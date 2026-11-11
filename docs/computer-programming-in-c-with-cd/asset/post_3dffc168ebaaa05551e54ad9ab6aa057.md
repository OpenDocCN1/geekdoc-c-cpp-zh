
## 3.2 Function

A function is a group of statements, which performs a specific task. It is a self-contained block of statements, which performs a specific task when executed. A function is used in C++ when you need to execute a group of statements many times in a program. It also separates a group of statements from rest of the code. Use of function in a program provides flexibility of dividing the large programs into manageable modules. This in turn makes the program less error prone. The following is the syntax to declare a function in a program:

```
return_type function_Name(list of argument)
```

In the preceding syntax, the `return_type` is the data type that the function returns and `function_Name` is the name of the function. A list of arguments is passed within the parenthesis as method parameter. A common example of a function is the `main()` function as shown in the following code snippet:

```cpp
// To display a welcome message.

int main()
{
    cout << "Hello from C++" << endl;
    return 0;
}
```

In the preceding code snippet, the empty parentheses after the name of the `main()` function indicates that this is the function with no arguments and the `int` before the `main()` function indicates that the function returns integer value. In a C++ program, the main() function is mandatory as the C++ program starts its execution from this function. Apart from the main() function, you can also create your own functions in a program to perform a specific task. Listing 6 shows a program with the use of a function in addition to the main() function (you can find the Func1.cpp file on the CD in the code/chapter3 folder):

### Listing 6: Creating a Function

```cpp
#include<iostream.h>
int sum(int x, int y)
{
    return x+y;
}
int main()
{
    int a=5;
    int b=6;
    int result=sum(a,b);
    cout << "The sum of a and b= " << result;
    return(0);
}
```

**Output:**

```text
The sum of a and b= 11
```

In Listing 6, the sum() function is created and used to add two numbers, although the program in Listing 6 also contains the main() function. The sum() function takes two integer values as arguments, adds these values, and returns the sum to the caller function that is the main() function.

You learn the types of functions in C++ in the following sections. The activities related to functions in C++ can be discussed under the following broad level headings:

- Discussing the types of C++ functions
- Declaring a Function Prototype
- Defining a Function
- Calling a Function
- Passing Argument to a Function
- Returning a Value from a Function
- Describing Function returning void
- Specifying Default Argument
- Describing Call by Value and Call by Reference
- Passing Array to a Function
- Passing Function Argument as const
- Passing String to a Function
- Using Recursion
- Creating Inline Function
- Using String Library Functions

Let’s start discussion with the types of functions in C++.

### Discussing the Types of C++ Functions

The C++ programming language compiler is provided with some built-in functions that are commonly used to write a C++ program. On the other hand, you can also create your own functions in a C++ program. Therefore, you can use the following two types of function in the C++ programming language:

- Standard library functions
- User-defined functions

Now, let’s discuss these functions in detail in the following sections.

### Standard Library Functions

In C++ programming language, the commonly used functions are grouped together and provided with its compiler. The functions of related functionalities are grouped together in a single standard library, such as the cin and cout functions, that are grouped together in the iostream library. The functions of these standard libraries are called standard library functions. Once the functions are grouped in the standard library, you are not required to declare and define them again rather you can use them directly in your program. For using them, you have to include the reference of that library in your program. You can add the reference of a library with the help of header file. The header instructs the C++ compiler to include the specific library in the program.

C++ comes with many standard library functions, such as `strlen()` and `strcmp()`, to perform string operation such as finding length of string. Let’s see how to pass an argument to the standard library function (`strlen()`) that returns the length of the string passed as argument. In Listing 7, the `strlen()` function is used to find the length of a string and return the value as the length of the string (string1) (you can find the Func2.cpp file on the CD in the code/chapter3 folder):

### Listing 7: Using Standard Library Function

```cpp
#include <iostream.h>
#include <string.h>
int main()
{
    char string1[] = "Hello";
    cout << "The length of string1 is " << strlen(string1) << " characters." << endl;
    return 0;
}
```

**Output:**

```text
The length of string1 is 5 characters.
```

In Listing 7, the string1 string is passed as an argument to the strlen() function, and the strlen() function returns the length of the string1 string. You can notice that the `string.h` header file is included because the strlen() function is defined in it, if you do not include the `string.h` header file, the program will generate the compilation error.

Now, after discussing the standard library functions, let’s discuss the user-defined functions.

### User-defined Functions

So far, you learned about various standard library functions provided by C++, but these are not sufficient to perform a variety of tasks in a program. To perform your customized tasks in a C++ program, you can create your own functions. For example, Listing 6 contains the sum() function, which is a user-defined function. Similar to this sum() function, you can create as many functions as you need in a program. Listing 8 shows another example of a user-defined function (you can find the Func3.cpp file on the CD in the code/chapter3 folder):

### Listing 8: Creating User-defined Function

```cpp
#include<iostream.h>
int area(int x, int y);
int main()
{
  int l,b;
  int ar=0;
  cout << "Enter Length ";
  cin >> l;
  cout << "\nEnter Breadth ";
  cin >> b;
  ar = area (l,b);
  cout << "Area of rectangle= " << ar;
  return 0;
}

int area(int x, int y)
{
  return x*y;
}
```

**Output:**

```text
Enter Length 5
Enter Breadth 4
Area of rectangle= 20
```

In Listing 8, the area() function is created and used to calculate the area of a rectangle. In this listing, the area() function is not defined at the time of its declaration. This declaration is known as function prototype declaration. It is possible to declare a function without defining it at the same time. The area() function takes two integer arguments and returns the product of these arguments to the caller function. The main() function calls the area() function with two integer values entered by the user and then displays the product as area of rectangle on the screen.

Let’s discuss the function prototype declaration in the following section.

### Declaring a Function Prototype

In a C++ program, you need to declare a function before providing the definition of the function. Declaring the signature of the function is known as declaring function prototype. In C++, a function prototype specifies function name, function parameters, type of parameters, and function return type, but does not have function body. The body of the function is defined elsewhere in the program. The function prototype directs the compiler about the structure of a function. Therefore, the compiler knows about the prerequisites to call and use the function. You can declare the function prototype before calling the main() function or within the main() function. Moreover, you have to put the termination symbol (;) at the end of the statement declaring function prototype. For example, the following code snippet declares the prototype (signature) of the maximum() function:

```
int maximum(int a, int b);
```

In the preceding code snippet, the function prototype of the maximum() function is declared, which takes two integer values as argument and also returns one integer value when it is called or executed.

Function prototype gives the following information to the compiler about a function:

- The data type of the value returned by the function, if it returns a value. Otherwise indicates that the function is not returning any value, when void is returned by the function.
- The number of arguments that a function takes.
- The data type of all the function arguments that a function takes.

Once a function prototype is declared, you need to define the declared function. Now, let’s discuss defining a function in the following section.

### Defining a Function

Providing the block of statements that performs the intended task of a function is called function definition. A function is uniquely defined by a name and a set of operands, which contains codes that are executed when a function is called. Its operands are referred to as parameters or arguments that are specified within parenthesis after the function name. Task performed by a function that is specified in a block is known as the function body. All the functions return some value if it is not declared with the void return type. The void return type declares that the function does not return any value after completing the execution. The following code snippet shows how to define a function:

```cpp
int maximum(int a, int b)
{
    int temp=0;
    if(a > b)
        temp = a;
    else
        temp = b;
    return temp;
}
```

In the preceding code snippet, we have defined the maximum() function that takes two integer values as arguments and returns an integer value too. The return keyword is used to return a value from the function.
