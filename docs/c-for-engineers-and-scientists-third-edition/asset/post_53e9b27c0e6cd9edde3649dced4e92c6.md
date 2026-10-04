
## Chapter 6 325

One of the first requirements in writing newval() is to declare two reference parameters for accepting passed addresses. In C++, a reference parameter is declared with this syntax:

```
dataType& referenceName
```

For example, the reference declaration

```
double num1;
```

declares that num1 is a reference parameter used to store the address of a double. Similarly, int& secnum; declares secnum is a reference to an integer, and char& key; declares that key is a reference to a character.

Because you need to accept two addresses in the parameter list for newval(), the declarations double& num1 and double& num2 can be used. Including these declarations in the parameter list for newval(), and assuming the function returns no value (void), the function header for newval() becomes the following:

```
void newval(double& num1, double& num2);
```

For this function header, the following is an appropriate prototype:

```
void newval(double& num1, double& secnum);
```

This prototype and function header are included in Program 6.8, which uses a newval() function body that displays the values stored in these reference variables from within the function body.

In calling the newval() function in Program 6.8, you need to understand the connection between the arguments, firstname, and secnum, used in the function call and the parameters, xnum and ynum, used in the function header. Both refer to the same data items. The significance is that the values in the arguments (firstname and secnum) can now be altered from within newval() by using the parameter names (xnum and ynum). Therefore, the parameters xnum and ynum do not store copies of the values in firstname and secnum; instead, they access the locations in memory set aside for these two arguments.

## 326 Modularity Using Functions

### Program 6.8

```cpp
#include <iostream>
using namespace std;

void newval(double&, double&); // prototype with two reference parameters

int main() {
    double firstname, secnum;

    cout << "Enter two numbers: *";
    cin >> firstname >> secnum;
    cout << "\nThe value in firstname is: " << firstname << endl;
    cout << "The value in secnum is: " << secnum << "\n\n";
    newval(firstname, secnum); // call the function
    cout << "The value in firstname is now: " << firstname << endl;
    cout << "The value in secnum is now: " << secnum << endl;
    return 0;
}

void newval(double& xnum, double& ynum) {
    cout << "The value in xnum is: " << xnum << endl;
    cout << "The value in ynum is: " << ynum << "\n\n";
    xnum = 89.5;
    ynum = 99.5;
}
```

The equivalence of argument names in Program 6.8, which is the essence of a pass by reference, is illustrated in Figure 6.7. As shown in this figure, the argument names and their matching parameter names are simply different names referring to the same memory storage areas. In main(), these memory locations are referenced by the argument names firstname and secnum, and in newval(), the same locations are referenced by the parameter names xnum and ynum.

## Chapter 6 327

In main() the values are referenced as

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_346_0.png)

In newval() the same values are referenced as

Figure 6.7 The equivalence of arguments and parameters in Program 6.8

The following is a sample run of Program 6.8:

```
Enter two numbers: 22.5 33.0
The value in firstname: 22.5
The value in secnum is: 33
The value in xnum: 22.5
The value in ynum is: 33
The value in firstname is now: 89.5
The value in secnum is now: 99.5
```

In reviewing this output, notice that the values initially displayed for the parameters xnum and ynum are the same as those displayed for the arguments firstname and secnum. Because xnum and ynum are reference parameters, however, newval() has direct access to the arguments firstname and secnum. Therefore, any change to xnum in newval() alters the value of firstname in main(), and any change to ynum changes secnum's value. As the final displayed values show, the assignment of values to xnum and ynum in newval() is reflected in main() as the altering of firstname's and secnum's values.

The equivalence between actual calling arguments and function parameters shown in Program 6.8 provides the basis for returning multiple values from a function. For example, say you want to write a function that's required to accept three values, compute these values' sum and product, and return these computed results to the calling routine. By

## 328 Modularity Using Functions

naming the function calc() and providing five parameters (three for input data and two referenced for values), the following function can be used:

```cpp
void calc(double num1, double num2, double num3, double& total, double& product) {
    total = num1 + num2 + num3;
    product = num1 * num2 * num3;
}
```

This function has five parameters, num1, num2, num3, total, and product. Only the last two are referenced, so the first three are passed by value and the last two are passed by reference. The value of total is calculated as the sum of num1, num2, and num3. The value of product is computed as the product of num1, num2, and num3. Program 6.9 includes this function.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_347_0.png)

### Program 6.9

```cpp
#include <iostream>
using namespace std;

void calc(double, double, double, double&, double&); // prototype with three value parameters and two reference parameters

int main() {
    double firstname, secnum, third, sum, product;

    cout << "Enter three numbers: ";
    cin >> firstname >> secnum >> third;
    cout << "\nThe value in firstname is: " << firstname << endl;
    cout << "The value in secnum is: " << secnum << endl;
    cout << "The value in third is: " << third << endl;
    calc(firstname, secnum, third, sum, product); // call the function
    cout << "The sum is: " << sum << endl;
    cout << "The product is: " << product << endl;
    return 0;
}

void calc(double num1, double num2, double num3, double& total, double& product) {
    total = num1 + num2 + num3;
    product = num1 * num2 * num3;
}
```

## Chapter 6 Returning Multiple Values 329

In main(), the function calc() is called with the five arguments firstname, secnum, third, sum, and product. As required, these arguments agree in number and data type with the parameters declared by calc(). The five arguments passed, firstname, secnum, and third have been assigned values when the call to calc() is made. The remaining two arguments have not been initialized and are used to receive values from calc(). Depending on the compiler used, these arguments initially contain zeros or "garbage" values. Figure 6.8 shows the relationship between actual and parameter names and the values they contain after the return from calc().

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_348_0.png)

Figure 6.8 The relationship between argument and parameter names

As a final example of the usefulness of passing references to a called function, take a look at constructing a function named swap() that exchanges the values of two main()'s double-precision variables. This type of function is useful when sorting a list of numbers. Because the value of more than one variable is affected, swap() cannot be written as a pass by value function that returns a single value. The exchange of main()'s variables by swap() can be accomplished only by giving swap() access to main()'s variables. One way of doing this is using reference parameters.

You have already seen how to pass references to two variables in Program 6.8. Now see how to exchange the values in the passed parameters.
