
![](img/d68f6199646ca63591a6d8419e0ed4ba_400_0.png)

We discuss more about the constness in reference relationships later in this chapter.

> **After the reference relationship is established, it cannot be changed.**

### EXAMPLE 9.1

We will get a compilation error if we first bind *rScore* to *score* and then try to break this relationship and bind *rScore* to *num*, as shown below:

```cpp
int score = 92;
int& rScore = score;
int num = 80;
int& rScore = num;    // Compilation error, breaking the reference relationship
```

### EXAMPLE 9.2

Sometimes we see statements that should not be confused with breaking the reference relationship. For example, consider the following:

```cpp
int score = 92;
int& rScore = score;
int num = 80;
rScore = num;
```

In this code segment, we are not breaking the relationship. We are storing a copy of value in *num* to the common memory location established by the reference relationship. In other words, the last statement is not binding; it is an assignment to the common variable. We could have used the statement score = num with the same effect.

## Multiplicity

We can have multiple reference variables bound to the same variable, but the reverse is not possible. We cannot have a reference variable bound to more than one variable.

### EXAMPLE 9.3

The following shows how to bind three reference variables (*rNum1*, *rNum2*, and *rNum3*) to a single variable *num*.

```cpp
int num = 100;
int& rNum1 = num;       // rNum1 is bound to num
int& rNum2 = num;       // rNum2 is bound to num
int& rNum3 = num;       // rNum3 is bound to num
```

This means that a memory location can be called using four names: *num*, *rNum1*, *rNum2*, and *rNum3*, as shown in Figure 9.3.

![](img/d68f6199646ca63591a6d8419e0ed4ba_401_0.png)

**Figure 9.3** Multiple references to the same variable are allowed.

![](img/d68f6199646ca63591a6d8419e0ed4ba_401_1.png)

**Figure 9.4** A reference to multiple variables is not allowed.

### EXAMPLE 9.4

We get a compilation error if we try to bind one reference variable to more than one variable because doing so means breaking the constant reference relation and creating a new one, which is not allowed.

```cpp
int num1 = 100;
int num2 = 200;
int& rNum = num1;        // rNum is bound to num1
int& rNum = num2;        // Compilation error. rNum cannot be bound to num2
```

Figure 9.4 shows this unacceptable relationship.

## No Binding to Values

Note that a reference variable cannot be bound to a value. For example, we get a compilation error in the following statement.

```cpp
int& x = 92;            // Compilation error: no binding to values
```

## 9.1.2 Retrieving Value

When the reference relationship is established, the value stored in the common memory locations can be retrieved either through the original variable or reference variable.

### EXAMPLE 9.5

Program 9.1 shows the use of an original variable and its reference. However, this application is only for demonstration; the actual relationship between a variable and its reference is beneficial when we use them in two different functions, as we will see later in the chapter.

### Program 9.1 Accessing value

```cpp
/************************************************************
 * The program shows how to declare and initialize the original    *
 * and reference variables and then access the common value       *
 * through either of them.
 *******************************************************************/
#include <iostream>
using namespace std;

int main ( )
{
    // Creation of reference relations
    int score = 92;
    int& rScore = score;
    // Using data variable
    cout << "Accessing value through data variable." << endl;
    cout << "score: " << score << endl;
    // Using reference variable
    cout << "Accessing value through reference variable." << endl;
    cout << "rScore: " << rScore << endl;
    return 0;
}
```

Run:

```text
Accessing value through data variable.
score: 92
Accessing value through reference variable.
rScore: 92
```

## 9.1.3 Changing Value

There is only one value in a reference relationship, but the value can be changed either through the original variable or through any of the reference variables, unless we use *const* modifiers (Figure 9.5).

![](img/d68f6199646ca63591a6d8419e0ed4ba_402_0.png)

**Figure 9.5** Preventing change in a reference relation

**Table 9.1 — Four possible combinations**

| **Case** | **Data variable** | **Reference variable** | **Status** |
|---|---|---|---|
| 1 | `int name = value;` | `int& rName = name;` | OK |
| 2 | `const int name = value;` | `int& rName = name;` | Error |
| 3 | `int name = value;` | `const int& rName = name;` | OK |
| 4 | `const int name = value;` | `const int& rName = name;` | OK |

The constant modifier can be put in front of the original variable or in front of the reference variable. The relationship (binding) is by nature constant and cannot be broken. Figure 9.5 shows the use of a const modifier for both the original and the reference variables.

Table 9.1 shows the four possible combinations, but the second one creates a compilation error, as we describe shortly.

### First Case

In the first case, there is no restriction to changing the value either through the original variable or through the reference variable.

### Second Case

The second case creates a compilation error because we try to bind a nonconstant reference variable to a constant variable. Since the original variable is already constant, there is no way that we can change its value through the reference variable.

### Third Case

In the third case, the data can be changed through the data variable, but we want to restrict it from being changed through the reference variable.

### Fourth Case

In the fourth case, we want to create an original variable and a reference variable in a way that neither the original variable nor the reference variable can change the common value. This case has little application because the data variable and the reference variable can only be used to retrieve data, not to change them.

## 9.1.4 Applications

Using references in the same namespace, such as in the same function, is unnecessary because we can always use the original variable instead of the reference variable. Both variables use the same memory location. The idea of references is beneficial when the two variables are in different scopes, like in a calling function and the called function. We can save memory by using one memory location and accessing it in two functions using the original variable and the reference variable.

In this section we discuss the use of references in the communication between two functions. We discuss using references in passing data to a function and in returning data from a function. The first application is called pass-by-reference; the second is called return-by-reference.

We need the copy constructor to create a copy constructor (vicious circle). The C++ standard says we must use pass-by-constant reference as shown below:

```cpp
// Pass-by-reference in copy constructor
Circle::Circle(const Circle& circle)
: radius (circle.radius)
{
}
```

### EXAMPLE 9.8

Assume we want to write a function to swap two data items. This is the second case in our recommendation. We need change, so we use pass-by-reference as shown in Program 9.2.

### Program 9.2 Using a swap function with pass-by-reference

```cpp
/************************************************************
 * The program shows how to use pass-by-reference to allow a
 * called function to swap two values in the calling function.
 ************************************************************/
#include <iostream>
using namespace std;

void swap (int& first, int& second);  // Prototype

int main ( )
{
    // Definition of two variables
    int x = 10;
    int y = 20;
    // Printing the value of x and y before swapping
    cout << "Values of x and y before swapping." << endl;
    cout << "x: " << x << " " << "y: " << y << endl;
    // Calling swap function to exchange the values of x and y
    swap (x, y);
    // Printing the value of x and y after swapping
    cout << "Values of x and y after swapping." << endl;
    cout << "x: " << x << " " << "y: " << y;
    return 0;
}
/************************************************************
 * The swap function swaps the values of the parameters and
 * pass-by-reference allows the corresponding arguments in main
 * to be swapped accordingly.
 ************************************************************/
void swap (int& x, int& y)
{
```
