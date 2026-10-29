
## Templates 16

16.1 FUNCTION TEMPLATES 730
Syntax for Function Templates 731
Pitfall: Compiler Complications 734
Tip: How to Define Templates 736
Example: A Generic Sorting Function 737
Pitfall: Using a Template with an Inappropriate Type 741

16.2 CLASS TEMPLATES 743
Syntax for Class Templates 744
Example: An Array Template Class 748
The vector and basic_string Templates 754

16.3 TEMPLATES AND INHERITANCE 754
Example: Template Class for a Partially Filled Array with Backup 755

Notice that the function swapValues applies only to variables of type int. Yet the algorithm given in the function body could just as well be used to swap the values in two variables of type char. If we want to also use the function swapValues with variables of type char, we can overload the function name swapValues by adding the following definition:

```
void swapValues(char& variable1, char& variable2)
{
    char temp;
    
    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

But there is something inefficient and unsatisfying about these two definitions of the swapValues function: they are almost identical. The only difference is that one definition uses the type int in three places and the other uses the type char in the same three places. Proceeding in this way, if we wanted to have the function swapValues apply to pairs of variables of type double, we would have to write a third, almost identical function definition. If we wanted to apply swapValues to still more types, the number of almost identical function definitions would be even larger. This would require a good deal of typing and would clutter up our code with lots of definitions that look identical. We should be able to say that the following function definition applies to variables of any type:

```
void swapValues(Type_Of_The_Variables& variable1,
                Type_Of_The_Variables& variable2)
{
    Type_Of_The_Variables temp;
    
    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

As we will see, something like this is possible. We can define one function that applies to all types of variables, although the syntax is a bit more complicated than what we have just shown. The proper syntax is described in the next subsection.

## Syntax for Function Templates

Display 16.1 shows a C++ template for the function swapValues. This function template allows you to swap the values of any two variables, of any type, as long as the two variables have the same type. The definition and the function declaration begin with the line

```
template<class T>
```

template prefix

type parameter

A template overloads the function name

This is often called the template prefix. It tells the compiler that the definition or function declaration that follows is a template and that T is a type parameter. In this context, the word class actually means type.¹ As we will see, the type parameter T can be replaced by any type, whether the type is a class or not. Within the body of the function definition, the type parameter T is used just like any other type.

The function template definition is, in effect, a large collection of function definitions. For the function template for swapValues shown in Display 16.1, there is, in effect, one function definition for each possible type name. Each of these definitions is obtained by replacing the type parameter T with a type name. For example, the function definition shown next is obtained by replacing T with the type name double:

```
void swapValues(double& variable1, double& variable2)
{
    double temp;

    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

Another definition for swapValues is obtained by replacing the type parameter T in the function template with the type name int. Yet another definition is obtained by replacing the type parameter T with char. The one function template shown in Display 16.1 overloads the function name swapValues so that there is a slightly different function definition for every possible type.

The compiler will not literally produce definitions for every possible type for the function name swapValues, but it will behave exactly as if it had produced all those function definitions. A separate definition will be produced for each different type for which you use the template, but not for any types you do not use. Only one definition is generated for a single type regardless of the number of times you use the template for that type. Notice that the function swapValues is called twice in Display 16.1: One time the arguments are of type int, and the other time the arguments are of type char. Consider the following function call from Display 16.1:

```
swapValues(integer1, integer2);
```

¹In fact, the ANSI/ISO standard provides that the keyword typename may be used instead of class in the template prefix. It would make more sense to use the keyword typename rather than class, but everybody uses class, so we will do the same. (It is often true that consistency in coding is more important than optimality.)

## Display 16.1 A Function Template

```
1 //Program to demonstrate a function template.
2 #include <iostream>
3 using std::cout;
4 using std::endl;
5 
6 //Interchanges the values of variable1 and variable2.
7 //The assignment operator must work for the type T.
8 template<class T>
9 void swapValues(T& variable1, T& variable2)
10 {
11     T temp;
12     temp = variable1;
13     variable1 = variable2;
14     variable2 = temp;
15 }
16 int main()
17 {
18     int integer1 = 1, integer2 = 2;
19     cout << "Original integer values are "
20         << integer1 << " " << integer2 << endl;
21     swapValues(integer1, integer2);
22     cout << "Swapped integer values are "
23         << integer1 << " " << integer2 << endl;
24     char symbol1 = 'A', symbol2 = 'B';
25     cout << "Original character values are: "
26         << symbol1 << " " << symbol2 << endl;
27     swapValues(symbol1, symbol2);
28     cout << "Swapped character values are: "
29         << symbol1 << " " << symbol2 << endl;
30     return 0;
}
```

Many compilers still have problems with templates. To be certain that your templates work on the widest selection of compilers, place the template definition in the same file in which it is used and have the template definition precede all uses of the template.

## Sample Dialogue

```
Original integer values are: 1 2
Swapped integer values are: 2 1
Original character values are: A B
Swapped character values are: B A
```

When the C++ compiler gets to this function call, it notices the types of the arguments—in this case, int—and then it uses the template to produce a function definition with the type parameter T replaced with the type name int. Similarly, when the compiler sees the function call

```
swapValues(symbol1, symbol2);
```

it notices the types of the arguments—in this case, char—and then it uses the template to produce a function definition with the type parameter T replaced with the type name char.

calling a function template

Notice that you need not do anything special when you call a function that is defined with a function template; call it just as you would any other function. The compiler does all the work of producing the function definition from the function template.

A function template may have a function declaration and a definition, just like an ordinary function. You may be able to place the function declaration and definition for a function template in the same locations that you place function declarations and definitions for ordinary functions. However, separate compilation of template definitions and template function declarations is not yet implemented on most compilers, so it is safest to place your template function definition in the file where you invoke the template function, as we did in Display 16.1. In fact, most compilers require that the template function definition appear before the first invocation of the template. You may simply #include the file containing your template function definitions prior to calling the template function. Your particular compiler may behave differently; you should ask a local expert about the details.

In the function template in Display 16.1, we used the letter T as the parameter for the type. This is traditional but is not required by the C++ language. The type parameter can be any identifier (other than a keyword). T is a good name for the type parameter, but other names can be used.

more than one type parameter

It is possible to have function templates that have more than one type parameter. For example, a function template with two type parameters named T1 and T2 would begin as follows:

```
template<class T1, class T2>
```

However, most function templates require only one type parameter. You cannot have unused template parameters; that is, each template parameter must be used in your template function.

## PITFALL: Compiler Complications

Many compilers do not allow separate compilation of templates, so you may need to include your template definition with your code that uses it. As usual, at least the function declaration must precede any use of the function template.

Some C++ compilers have additional special requirements for using templates. If you have trouble compiling your templates, check your manuals or check with a local expert. You may need to set special options or rearrange the way you order the template definitions and the other items in your files.
