
However, the start of the file is not always the best location for the line

    using namespace std;

We will eventually be using more namespaces than just std. In fact, we may be using different namespaces in different function definitions. If you place the directive

    using namespace std;

inside the brace { that starts the body of a function definition, then the using directive applies to only that function definition. This will allow you to use two different namespaces in two different function definitions, even if the two function definitions are in the same file and even if the two namespaces have some name(s) with different meanings in the two different namespaces.

Placing a using directive inside a function definition is analogous to placing a variable declaration inside a function definition. If you place a variable definition inside a function definition, the variable is local to the function; that is, the meaning of the variable declaration is confined to the function definition. If you place a using directive inside a function definition, the using directive is local to the function definition; in other words, the meaning of the using directive is confined to the function definition.

It will be some time before we use any namespace other than std in a using directive, but it will be good practice to start placing these using directives where they should go. In Display 4.15 we have rewritten the program in Display 4.12 with the using directives where they should be placed. The program in Display 4.15 will behave exactly the same as the one in Display 4.12. In this particular case, the difference is only one of style, but when you start to use more namespaces, the difference will affect how your programs perform.

## DISPLAY 4.15 Using Namespaces (part 1 of 2)

```
//Computes the area of a circle and the volume of a sphere.
//Uses the same radius for both calculations.
#include <iostream>
#include <cmath>

const double PI = 3.14159;

double area(double radius);
//Returns the area of a circle with the specified radius.

double volume(double radius);
//Returns the volume of a sphere with the specified radius.
```

(continued)

## DISPLAY 4.15 Using Namespaces (part 2 of 2)

```
13
14 int main( )
15 {
16     using namespace std;
17
18     double radiusOfBoth, areaOfCircle, volumeOfSphere;
19
20     cout << "Enter a radius to use for both a circle\n"
21         << "and a sphere (in inches): ";
22     cin >> radiusOfBoth;
23
24     areaOfCircle = area(radiusOfBoth);
25     volumeOfSphere = volume(radiusOfBoth);
26
27     cout << "Radius = " << radiusOfBoth << " inches\n"
28         << "Area of circle = " << areaOfCircle
29         << " square inches\n"
30         << "Volume of sphere = " << volumeOfSphere
31         << " cubic inches\n";
32
33     return 0;
34 }
35
36
37 double area(double radius)
38 {
39     using namespace std;
40
41     return (PI * pow(radius, 2));
42 }
43
44 double volume(double radius)
45 {
46     using namespace std;
47
48     return ((4.0/3.0) * PI * pow(radius, 3));
49 }
```

The sample dialogue for this program would be the same as the one for the program in Display 4.12.

## SELF-TEST EXERCISES

20. If you use a variable in a function definition, where should you declare the variable? In the function definition? In the main part of the program? Any place that is convenient?

## DISPLAY 4.16 Factorial Function

### Function Declaration

```
1    int factorial(int n);
2    //Returns factorial of n.
3    //The argument n should be nonnegative.
```

### Function Definition

```
1    int factorial(int n)
2    {
3        int product = 1;
4        while (n > 0)
5        {
6            product = n * product;
7            n--;
8        }
9
10       return product;
11   }
```

formal parameter n used as a local variable

The function definition for factorial uses two local variables: product, which is declared at the start of the function body, and the formal parameter n. Since a formal parameter is a local variable, we can change its value. In this case we change the value of the formal parameter n with the decrement operator n--. (The decrement operator was discussed in Chapter 2.)

Each time the body of the loop is executed, the value of the variable product is multiplied by the value of n, and then the value of n is decreased by one using n--. If the function factorial is called with 3 as its argument, then the first time the loop body is executed the value of product is 3, the next time the loop body is executed the value of product is 3 * 2, the next time the value of product is 3 * 2 * 1, and then the while loop ends. Thus, the following will set the variable x equal to 6 which is 3 * 2 * 1:

```
x = factorial(3);
```

Notice that the local variable product is initialized to the value 1 when the variable is declared. (This way of initializing a variable when it is declared was introduced in Chapter 2.) It is easy to see that 1 is the correct initial value for the variable product. To see that this is the correct initial value for product, note that after executing the body of the while loop the first time, we want the value of product to be equal to the (original) value of the formal parameter n; if product is initialized to 1, then this will be what happens.

Formal parameter used as a local variable

This will work, and in many programming languages you have no choice but to do something like this. Fortunately, C++ allows for a more elegant solution. In C++ you can simply use the same function name ave for both functions; you can use the following function definition in place of the function definition ave3:

```
double ave(double n1, double n2, double n3)
{
    return ((n1 + n2 + n3)/3.0);
}
```

## DISPLAY 4.17 Overloading a Function Name

```
//Illustrates overloading the function name ave.
#include <iostream>

double ave(double n1, double n2);
//Returns the average of the two numbers n1 and n2.

double ave(double n1, double n2, double n3);
//Returns the average of the three numbers n1, n2, and n3.

int main()
{
    using namespace std;
    cout << "The average of 2.0, 2.5, and 3.0 is "
         << ave(2.0, 2.5, 3.0) << endl;

    cout << "The average of 4.5 and 5.5 is "
         << ave(4.5, 5.5) << endl;

    return 0;
}

double ave(double n1, double n2)
{
    return ((n1 + n2)/2.0);
}

double ave(double n1, double n2, double n3)
{
    return ((n1 + n2 + n3)/3.0);
}
```

### Output

```
The average of 2.0, 2.5, and 3.0 is 2.50000
The average of 4.5 and 5.5 is 5.00000
```

The function name ave now has two definitions. This is an example of overloading. In this case we have overloaded the function name ave. In Display 4.17 we have embedded these two function definitions for ave into a complete sample program. Be sure to notice that each function definition has its own function declaration.

Overloading is a great idea. It makes a program easier to read, and it saves you from going crazy trying to think up a new name for a function just because you already used the most natural name in some other function definition. But how does the compiler know which function definition to use when it encounters a call to a function name that has two or more definitions? The compiler cannot read a programmer’s mind. In order to tell which function definition to use, the compiler checks the number of arguments and the types of the arguments in the function call. In the program in Display 4.17, one of the functions called ave has two arguments and the other has three arguments. To tell which definition to use, the compiler simply counts the number of arguments in the function call. If there are two arguments, it uses the first definition. If there are three arguments, it uses the second definition.

Determining which definition applies

Whenever you give two or more definitions to the same function name, the various function definitions must have different specifications for their arguments; that is, any two function definitions that have the same function name must use different numbers of formal parameters or use formal parameters of different types (or both). Notice that when you overload a function name, the function declarations for the two different definitions must differ in their formal parameters. You cannot overload a function name by giving two definitions that differ only in the type of the value returned.

### Overloading a Function Name

If you have two or more function definitions for the same function name, that is called overloading. When you overload a function name, the function definitions must have different numbers of formal parameters or some formal parameters of different types. When there is a function call, the compiler uses the function definition whose number of formal parameters and types of formal parameters match the arguments in the function call.

Overloading is not really new to you. You saw a kind of overloading in Chapter 2 with the division operator /. If both operands are of type int, as in 13/2, then the value returned is the result of integer division, in this case 6. On the other hand, if one or both operands are of type double, then the value returned is the result of regular division; for example, 13/2.0 returned the value 6.5. There are two definitions for the division operator /, and the two definitions are distinguished not by having different numbers of operands,
