
# Templates 16

- 16.1 FUNCTION TEMPLATES 694
- Syntax for Function Templates 695
- Pitfall: Compiler Complications 698
- Tip: How to Define Templates 700
- Example: A Generic Sorting Function 701
- Pitfall: Using a Template with an Inappropriate Type 705

- 16.2 CLASS TEMPLATES 707
- Syntax for Class Templates 708
- Example: An Array Template Class 712
- The vector and basic_string Templates 718

- 16.3 TEMPLATES AND INHERITANCE 718
- Example: Template Class for a Partially Filled Array with Backup 719

# 16 Templates

All men are mortal.
Aristotle is a man.
Therefore, Aristotle is a man.

All X's are Y.
Z is an X.
Therefore, Z is Y.

All cats are mischievous.
Garfield is a cat.
Therefore, Garfield is mischievous.

A Short Lesson on Syllogisms

# Introduction

This chapter discusses C++ templates, which allow you to define functions and classes that have parameters for type names. This enables you to design functions that can be used with arguments of different types and to define classes that are much more general than those you have seen before this chapter.

Section 16.1 requires only material from Chapters 1 through 5. Section 16.2 uses material from Section 16.1 as well as Chapters 1 through 11 but does not require the material from Chapters 12 through 15. Section 16.3 requires the previous sections as well as Chapter 14 on inheritance and all the chapters needed for Section 16.2. Section 16.3 does mark some member functions as virtual. Virtual functions are covered in Chapter 15. However, this use of virtual functions is not essential to the material presented. It is possible to read Section 16.3 ignoring (or even omitting) all the occurrences of the keyword virtual.

# 16.1 Function Templates

Many of our previously discussed C++ function definitions have an underlying algorithm that is much more general than the algorithm we gave in the function definition. For example, consider the function swapValues, which we first discussed in Chapter 4. For reference, we repeat the function definition:

```
void swapValues(int& variable1, int& variable2)
{
    int temp;
    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

# Function Templates

Notice that the function swapValues applies only to variables of type int. The algorithm given in the function body could as well be used to swap the variables in two variables of type char. If we want to also use the function swapValues with variables of type char, we can overload the name swapValues by adding the following definition:

```
void swapValues(char& variable1, char& variable2)
{
    char temp;

    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

But there is something inefficient and unsatisfying about these definitions of the swapValues function: They are almost identical. The only difference is that one definition uses the type int in three places and the other uses the type char in the same places. Proceeding in this way, if we wanted to have the function swapValues applies to pairs of variables of type double, we would have to write a third, almost identical definition. If we wanted to apply swapValues to still more types, the number of almost identical definitions would be even larger. This would require a good deal of tying and would clutter our code with lots of definitions that look identical. We should be able to say that the following function definition applies to any of type:

```
void swapValues(Type_Of_The_Variables& variable1, Type_Of_The_Variables& variable2)
{
    Type_Of_The_Variables temp;
    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

As we see, this is possible. We can define one function that applies to all types of variables, although the syntax is a bit more complicated than what we have just shown. The proper syntax is described in the next subsection.

# Syntax for Function Templates

16.1 shows a C++ template for the function swapValues. This function template allows you to swap the values of any two variables, of any type, as long as the two variables have the same type. The definition and the function declaration begin with the line

```
template<class T>
```

template prefix type parameter

This is often called the template prefix. It tells the compiler that the definition or function declaration that follows a template and T is a type parameter. In this context, the word class makes type type. As we see, the type parameter T can be replaced by any type, whether that is a class or not. Within the body of the function definition, the type parameter T is used just like any other.

A template overloads the function name

The template definition is, in effect, a large collection of definitions. For the function swapValues shown in Display 16.1, there is, one effect function definition for each possible type. Each of these definitions is obtained by replacing the type parameter T with a name. For example, the function definition shown next is obtained by replacing T with the type name double:

```
void swapValues(double& variable1, double& variable2){
    double temp;
    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

Another definition for swapValues is obtained by replacing the type parameter T in the function template with the type name int. Another definition is obtained by replacing the type parameter T with char. The one function template shown in Display 16.1 overlaps the function swapValues so that there is a slightly different function definition for possible type.

The compiler will not literally produce definitions for every possible type for the function name swapValues, but it will behave exactly as if it had produced all those definitions. A separate definition will be produced for each different type for which you use the template, but not for types you do not use. Only one definition is generated for a single type regardless of the number of times you use the template for that type. Notice that the function swapValues is called twice in Display 16.1: One time the arguments are of type int, and the other time the arguments are of type char. Consider the following function call from Display 16.1:

```
swapValues(integer1, integer2);
```

> In fact, the ANSI/ISO standard provides that the keyword typename may be used of class in the template prefix. It would make more sense to use the keyword typename rather than class, but everyone uses class, so we do the same. (It is true that consistency in coding is more important than optimality.)

# Function Templates

Display 16.1 A Function Template

```
// //Program to demonstrate a function template.
#include <iostream>
using std::cout;
using std::endl;
```

//Interchanges the values of variable and variable2.
//Theassignment operator must work for the type T.
template<class T>:
void swapValues(T& variable1, T& variable2)
{
temp = variable1;
variable1 = variable2;
variable2 = temp;
}
```

Many compilers still have templates. To be certain that your templates work on the widest selection of compilers, place the template definition in the same file where it is used and have the template definition precede all uses of the template.

```
int main() {
int integer1 = 1, integer2 = 2;
cout << "Original integer values are: "
cout << integer1 << " " << integer2 << endl;
swapValues(integer1, integer2);
cout << "Swapped integer values are: "
cout << integer1 << " " << integer2 << endl;
}
```

```
char symbol1 = 'A', symbol2 = 'B';
cout << "Original character values are: "
cout << symbol1 << " " << symbol2 << endl;
swapValues(symbol1, symbol2);
cout << "Swapped character values are: "
cout << symbol1 << " " << symbol2 << endl;
return 0;
}
```

# 16 Templates

When the C++ compiler gets to this call, it notices the types of arguments—in this case—and then it uses the template to produce a function definition with the type parameter replaced by the type name. Similarly, when the compiler sees the function call

```
swapValues(symbol1, symbol2);
```

A function template may have a declaration and definition, just like an ordinary function. You may be able to place the template declaration and definition in the same locations as you ordinary functions. However, separation of templates is not implemented by most compilers, so it is safest to place your template definition in the file where you use it.

In the function template in 16.1, we used the letter T as the parameter for the type. This is traditional but not required by the C++ language. The type parameter can be any identifier (not a keyword). T is a good name for the type parameter, but other names can be used.

It is possible to have function templates with more than one type parameter. For example, a function template with two type parameters T1 and T2 would begin as follows:

```
template<class T1, class T2>
```

However, most function templates require only one type parameter. You cannot have unused template parameters; that is, each template parameter must be used in your template function.

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_727_0.png)

# Pitfall: Compiler complications

Many compilers do not allow separation of templates, so you may need to include your template definition with your code that uses it. As usual, at least the function declaration must precede any use of the template.

Some C++ templates have special requirements for using them. If you have trouble compiling your templates, check your manuals or check with a local expert. You may need to set special options or rearrange the way you order the template definitions and the other items in your files.
