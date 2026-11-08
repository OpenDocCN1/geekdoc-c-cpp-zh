different names. A reference variable must be initialized at the time of declaration. This establishes a relation between the reference and the data object, which it refers to. It is important to note that the initialization of a reference variable is completely different from its assignment.

Let's now learn how to declare variables in the next section.

# ## Declaration of Variables

We know that in C language, all the variables must be declared before they are used in executable statements of a program. This is true for the C++ language as well. However, there is a significant difference between C and C++ with regard to the place of their declaration. C language requires that all the variables should be defined at the beginning of the scope. In a typical C program, variable declarations are done at the top followed by executable instructions in the main() function body. At times, their actual usage is done far away from the place where it is declared, which leads to several problems in keeping track of the variables in C. Therefore, while constructing the C++ language, the designers of the language addressed this issue.

C++ allows the declaration of a variable anywhere within the scope. We only need to ensure that a variable is declared in C++, before it is used. In other words, there is no restriction regarding the place of declaration of C++ variables. This helps in making the program more realistic and readable, as a variable is declared just above where it is going to be used. In addition, every time we need to declare a variable, we need not go at the beginning of the scope to declare the variable. This approach also reduces the chances of errors that were present during the earlier days of C, which caused us to scan the program back and forth. Listing 12.2 shows the declaration of variables in C++.

Listing 12.2: Demonstrating the Declaration of Variables in C++

```
```
//A sample program demonstrating declaration of variables in C++ #include <iostream>
using namespace std;
int main()
{
    float sum = 0;            //declaration of a variable
    for (int i=0;i<5; i++)    //declaration of a variable
    {
        sum = sum + i;
    }
    float average;
    average = sum / 5;
    cout <<" The average value is "<<average<<endl;
    return 0;
}
```
```

However, one disadvantage of this approach is that we cannot see all the variables used in a scope at the same time. To solve this problem, we can write our own source code as in C language, where all the variables are defined at the beginning of the program.

Let's now learn about the expressions, operators, and operator precedence in C++.

# ## Expressions, Operators, and Operator Precedence

As we are new to C++, let's cover a little bit on expressions, operators, and operator precedence. Although, all these topics had already been covered in the section of C programming, and there is not much difference between the operators in C and C++, we will try to only focus on operators that are specific to C++. Expressions are sequence of operators and operands that are used for computing a value from the operands and designating objects or functions. In C++, operators can be overloaded and their meaning can be user-defined, however, operator precedence and the number of operands they take cannot be modified. This section describes the syntax and semantics of operators as they are supplied with the language. These three forms the basic skeleton of any language and gives a major part of understanding about the language. Therefore, it is very essential to start discussing about them before we start writing programs in C++.