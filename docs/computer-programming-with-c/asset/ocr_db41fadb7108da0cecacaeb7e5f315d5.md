![](bbox=[0.22, 0.113, 0.807, 0.388])

# 11.12 Employee Management System: Revisited

Let us develop a C++ program to store the details of n employees in a computer memory. As the value of n is not known at the time of compilation, we will create an array e of size 100, assuming that the maximum number of employees will always be ≤100. The below statement will create an array e of type Employee with a size as 100:

```
```cpp
Employee e[100];
```
```

As seen later in the code, the program also takes the value of variable n as input from the user to determine the actual number of employees to be stored in the computer memory. Recall from Section 11.11 that each element e[i] of the array e is actually the object of class Employee, hence we can invoke the function input() over each of the object e[i] to accept members id, name, and salary of e[i] as input from the user. Similarly, we can invoke the function output() over each of the object e[i] to print the members id, name, and salary of e[i]. In the program, we have used a simple for loop to iterate over the array e. As there are a total of n objects in the array, the value index i will range from 0 to n−1 as seen in the code.

In the following code, we first accept the data about all the employees as input from the user by invoking the input() function for each of the Employee objects in the for loop and then print the members of each of the Employee objects using another for loop as shown.

```
```cpp
#include <iostream.h>
class Employee
{
private:
        int id;
        char name[100];
```
```