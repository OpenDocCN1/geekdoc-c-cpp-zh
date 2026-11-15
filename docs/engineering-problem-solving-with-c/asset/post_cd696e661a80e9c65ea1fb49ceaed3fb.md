
| Step | main() | swapIntegers(int a, int b) |
| :--- | :--- | :--- |
| Step 1: | integer a ?<br>integer b ? | |
| Step 2: | integer a 5<br>integer b 10 | |
| Step 3: | integer a 5<br>integer b 10 | integer a [ ]<br>integer b [ ] |
| Step 4: | integer a 5<br>integer b 10 | integer hold [ 5 ] |
| Step 5: | integer a 10<br>integer b 10 | integer a [ ]<br>integer b [ ] |
| Step 6: | integer a 10<br>integer b 5 | integer a [ ]<br>integer b [ ] |
| Step 7: | integer a 10<br>integer b 5 | Function variables are released. |
| Step 8: | All memory is released. | |

Recall that function arguments and formal parameters must agree in order, type and number, but the names do not have to be the same. In the above example we chose to use the same identifiers for the function arguments and the formal parameters. This is allowable because the identifiers are defined within different statement blocks. However, it is important to realize that a and b defined in the main function occupy different memory locations than a and b defined in the function header. Function arguments that correspond to pass-by-reference parameters must be variables, since their values can be modified. Constants and expressions cannot be passed as arguments to pass-by-reference parameters.

## Modify 6.2

- 1. Modify the driver program developed in the previous section by adding the following function call:
  - swapIntegers(10, 5);
  - What results do you see when you attempt to compile and execute the program?
  - Explain.

- 2. Modify the driver program developed in the previous section by adding the following function call:
  - swapIntegers(a, a * b);
  - What results do you see when you attempt to compile and execute this program?
  - Explain.

## Practice 6.2

In Problems 1–4, consider the references to the swapIntegers function. For invalid reference, explain why the reference is invalid. For valid references, give a memory snapshot before and after the reference.

- 1. int x=1, y=3;
  - ...
  - swapIntegers(x,y);

- 2. ...
  - swapIntegers(10, 5);

- 3. int x=1, y=3;
  - ...
  - swapIntegers(x, y+5);

- 4. double x=1.5, y=3.2;
  - ...
  - swapIntegers(x, y);

- 5. What is output by the following program?

```
#include<iostream>
using namespace std;

void fun_ch6(int first, int& second);

int main()
{
    int n1(0), n2(0);
    fun_ch6(n1,n2);
    cout << n1 << endl << n2 << endl;
    return 0;
}
```

## Practice 6.2 continued

```
void fun_ch6(int first, int second)
{
    first++;
    second += 2;
    return;
}
```

## Storage Class and Scope

In the sample programs presented thus far, we have declared objects within a main function and within programmer-defined functions, and we have placed our function prototypes before the main function. It is also possible to define an object before the main function. This affects the scope of the object, where scope refers to the portion of the program in which it is valid to reference the object. Scope is also sometimes defined in terms of the portion of the program in which the object is visible or accessible. It is important to be able to determine the scope of a function or object. Because the scope of an object is directly related to its storage class, we also discuss the four storage classes: automatic, external, static, and register.

- scope
- storage class
- local global
- automatic storage class
- external storage class

First, we define the difference between local and global or file scope. Local objects are defined within a function and thus include the formal parameters and any other objects declared in the function. A local object can be accessed only in the function that defines it. A local object has a value when its function is being executed, but its value is not retained when the function is completed. Global objects are defined outside the main function or other programmer-defined functions. The definition of a global object is outside of all functions, so it can be accessed by any function within the program file. The automatic storage class is used to represent local objects; this is the default storage class, but it can also be specified with the keyword auto before the type definition. The external storage class is used to represent global objects.

Consider a program that contains the following statements:

```
#include <iostream>
using namespace std;

int count(0);
...
int main()
{
    int x, y, z;
    ...
}

int calc(int a, int b)
{
    int x;
    count += x;
    ...
}

void check(int sum)
{
    count += sum;
    ...
}
```

The object count is global and thus can be referenced by the functions calc() and check(). The objects x, y, and z are local objects that can be referenced only in the main function, similarly, the objects a, b, and x are local objects that can be referenced only in the function calc(), and sum is a local object that can be referenced only in the function check(). Note that there are two local objects named x—these are two different objects with different scopes.

The memory assigned to a global object is retained for the duration of the program. Although a global object can be referenced from a function, using global objects is generally discouraged. In general, parameters are preferred for transferring information to a function because the parameter is evident in the function prototype, whereas the global object is not visible in the function prototype. The use of nonconstant global objects should be avoided.

![](img/0235a4ea835dc4575bd036e024a533b3_297_0.png)

Function names also have external storage class, and thus can be referenced from other functions. Function prototypes, and #include directives included outside of any function are also global, and thus are available to all other functions in the program; this explains why we do not need to include the header file cmath in every function that references a mathematical function.

The static storage class is used to specify that the memory for a local object should be retained during the entire program execution. Therefore, if a local object in a function is given a static storage class assignment by using the keyword static before its type specification, the object will not lose its value when the program exits the function in which it is defined. A static object could be used to count the number of times that a function was invoked, because the value of the count would be preserved from one function call to another. The following program illustrates the use of the static storage class:

```
#include<iostream>
using namespace std;

void ch6_static();

int main()
{
    ch6_static();
    ch6_static();
    ch6_static();
}

void ch6_static()
{
    int x(0);
    static int count(0);
    x++;
    count++;
    cout << x << ' ' << count;
    return;
}
```

The first time the function ch6_static() is called the objects x and count are defined and initialized. Since count is static and retains its value, the initialization is ignored on all subsequent calls to the function. The output from this program is as follows:

```
1 1
1 2
1 3
```

The keyword register is used before the type designation of an object to specify that it should be placed in a register or high speed memory location. Accessing registers is faster than accessing memory, so this class of storage is used for frequently accessed values. Because the availability of high speed memory is limited, it may not be possible to honor the request and the object will be placed in a regular memory location.

## 6.4 Problem Solving Applied: Calculating a Center of Gravity

### 1. PROBLEM STATEMENT

Determine the total weight and center of gravity of an aircraft, based on the number of crew members (a maximum of two is allowed) and the weight of the cargo (a maximum of 5,000 pounds is allowed). To compute the center of gravity, the program will take each weight and multiply it by its distance from the nose of the airplane. These products, called moments, are added together, and the sum is divided by the total weight to give us its center of gravity. The empty weight of the aircraft is known to be 9,021 pounds, and its empty center of gravity is 305 inches from the nose of the aircraft. Thus, the empty moment is 2,751,405 inch-pounds. The aircraft can hold a maximum of 540 gallons of fuel. For simplicity, we will assume that the tank is full at the time of takeoff and, with a fuel weight of 6.7 pounds per gallon, the fuel moment is known to be 1,169,167.3 inch-pounds.

### 2. INPUT/OUTPUT DESCRIPTION

The I/O diagram illustrates that the inputs to this program are the number of crew members (one to two) and the weight of the cargo. The output is a report of the total weight of the aircraft and the center of gravity. Built in data types int and double will be used for all data objects.

![](img/0235a4ea835dc4575bd036e024a533b3_298_0.png)
