
# Chapter 12
## Addresses and Pointers

These two declarations can be read as "the variable pointed to by tab is a double" and "the variable pointed to by chr is a char." Because all addresses appear the same, the compiler needs this additional information to know how many storage to access when it uses the address stored in the pointer.

Here are other examples of pointer declarations:

```cpp
char *inkey;
int *numPt;
double *nmlPtr;
```

To understand pointer declarations, reading them "backward" is helpful, starting with the indirection operator, and translating it as "the variable whose address is stored" or "the variable pointed by." Applying this method to pointer declarations, the declaration `char *inkey;` can be read as "the whose address is stored in inkey is a char" or "the variable pointed to by inkey is a char." Both statements are often shortened to the simpler "inkey points to a char." All three interpretations of the declaration statement are correct, so you can use the description that makes the most sense to you. Program 12.2 puts this information together to construct a program using pointers.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_688_0.png)

# Program 12.2

```cpp
#include <iostream>
using namespace std;

int main() {
    int *numAddr; // declare a pointer to an int
    int miles, dist; // declare two integer variables

    dist = 158; // store the number 158 in dist
    miles = 22; // store the number 22 in miles
    numAddr = &miles; // store the 'address of miles' in numAddr

    cout << "The address stored in numAddr is " << numAddr << endl;
    cout << "The value pointed to by numAddr is " << *numAddr << "\n\n";

    numAddr = &dist; // store the address of dist in numAddr
    cout << "The address now stored in numAddr is " << *numAddr << endl;
    cout << "The value now pointed to by numAddr is " << *numAddr << endl;

    return 0;
}
```

# 670 Pointers

The output of Program 12.2 is as follows:

```
The address stored in numAddr is 0012FEC8
The value pointed to by numAddr is 22
The address now stored in numAddr is 0012FEBC
The value now pointed to by numAddr is 158
```

The only use for Program 12.2 is to help you understand what gets stored here, so we review the program to see how the output was produced. The declaration statement `*numAddr;` declares `numAddr` as a pointer to store the address of an integer variable. The statement `numAddr = &miles;` stores the address of the variable `miles` in the pointer `numAddr`. The first statement uses the operation to retrieve and display the value pointed to by `numAddr`, which, of course, the value stored in `miles`.

Because `numAddr` has been declared as a pointer to an integer variable, you can use this pointer to store the address of any integer variable. The statement `numAddr = &dist;` illustrates this by storing the address of the variable `dist` in `numAddr`. The last two statements verify the change in `numAddr`'s value and confirm the new stored address points to the variable `dist`. As shown in Program 12.2, only addresses should be stored in pointers.

It would have been much simpler if the pointer used in Program 12.2 could have been declared as variable `numAddr`. This declaration conveys no information about the storage the variable whose address is stored in `numAddr`. This information is essential when the pointer is used with the indirection operator, as in the second statement in Program 12.2. For example, if an integer's address is stored in `numAddr`, typically only 4 bytes are retrieved when the address is used. If a character's address is stored in `numAddr`, only 1 byte of storage is retrieved, and a double typically retrieves 8 bytes of storage. The declaration of a pointer must, therefore, include the type of variable being pointed to, as illustrated in Figure 12.5.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_689_0.png)

**Figure 12.5** Addressing different data types using pointers

# Chapter 12
Addresses and Pointers

## References and Pointers

At this point, you might be asking what the difference is between a pointer and a reference. Essentially, a reference is a named constant for an address; therefore, the address named as a reference can't be altered. Because a pointer is a variable, the address in a pointer can be changed. For many applications, using references rather than pointers as functions is easier and preferred. The reason is the simpler notation for locating a reference parameter, which eliminates the address operator (&) and induction operator (*) that are required for pointers. Technically, references are said to be automatically dereferenced or implicitly dereferenced (the terms are used synchronously), and pointers must be dereferenced explicitly to be accessed.

For example, passing a variable's address as a function argument, references provide a simpler notation and are usually preferred. For other situations, such as dynamically allocating memory for additional variables as a program is running or using alternatives to array notation (both are discussed later in this chapter), pointers are required.

### Reference Variables³
References are used almost exclusively as function parameters and return types. Nevertheless, reference variables are also available in C++. For completeness, see how to use these variables.

After a variable has been declared, it can be given additional names by using a reference declaration, which has this form:

```cpp
dataType& name = existingName;
```

For example, the reference declaration

```cpp
double& sum = total;
```

equates the name `sum` to the name `total`. Both now refer to the variable as, as illustrated in Figure 12.6.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_690_0.png)

**Figure 12.6** sum is an alternative name for

After establishing another name for variable using a reference declaration, the name, as alias, can be used in place of the original. For example, look at 12.3.

# 672 Pointers
# Program 12.3

```cpp
#include <iostream>
using namespace std;

int main() {
    double total = 20.0;
    double& sum = total;

    cout << "The address of total is " << &total << endl;
    cout << "The value of sum is " << sum << endl;

    sum = 25.5;
    cout << "The new value of total is " << total << endl;

    return 0;
}
```

The following output is produced by Program 12.3:

```
The address of total is 0012FEB8
The value of sum is 20
The new value of total is 25.5
```

Because `sum` is a reference to `total`, the address of `total` is the same as the address of `sum`. The statement `sum = 25.5` changes the value of `total` because `sum` is an alias for `total`. Note that a reference variable cannot be reassigned to point to another variable. For example, the following causes a compiler error:

```cpp
int num = 5;
int val = 10;
int& ref = num;
ref = val; // This changes num, not ref.
```

When a reference is initialized, it is bound to the variable. This cannot be changed later. For example, the following is invalid:

```cpp
int num = 5;
int val = 10;
int& ref; // Error: reference must be initialized
```

If a reference is used in an expression, it behaves like the variable it refers to. For example:

```cpp
void swap(int& a, int b) {
    int temp = a;
    a = b;
    b = temp;
}
```

Using this function, you can swap the values of two variables without using the address operator or induction operator.

# Chapter 12
Addresses and Pointers
## 73

Another way of looking at references is to consider them as pointers with restricted capabilities. For example, look at these statements:

```cpp
int b;
int&a = b;
a = 10;
```

Here, `a` is declared as a reference variable that stores the address of `b`. Because `a` is declared as a reference, the compiler automatically assigns the address of `b`. Finally, in the statement `a = 10`, the compiler changes the value stored in `b`.

 pointers pointers, you must use the induction operator. For example:

```cpp
int b;
int *a = b;
*a = 10;
```

Here, `a` is defined as a pointer to store the address of `b`. Therefore, `*a` (which can be read as "the address is a" or "the variable pointed by b") is `b`, and the expression `*a = 10` changes the value stored in `b`. Notice that with pointers, the stored address can be altered to point to any other variable except the one it's initialized to. Also, notice that a reference variable cannot be reassigned to point to another variable. To dereference a, you must use the induction operator, *. As you might expect, the * is also called the dereferencing operator.

# EXERCISES 12.1

+   1. (For) If average is a variable, what does &average mean?
2. (Practice) For the variables and addresses shown in Figure 12.7, determine the addresses corresponding to the expressions &temp, &dist, &date, and &miles.
3. (Practice) Write a C++ program that includes the following declaration statements. Have the program use the address operator and a cout statement to display the addresses corresponding to each variable.

```cpp
int num, count;
long date;
float slope;
double power;
```

+   b. After running the program for Exercise 3a, draw a diagram of how your computer has set aside storage for the variables in the program. On your diagram, fill in the addresses the program displays.
