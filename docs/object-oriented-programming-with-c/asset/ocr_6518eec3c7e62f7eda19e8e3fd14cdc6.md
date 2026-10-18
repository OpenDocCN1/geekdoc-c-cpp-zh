```
```cpp
vector <int> v1(10);        // 10 element int vector
vector <float> v2(25);      // 25 element float vector
```
```

> NOTE: *The type T may represent a class name as well.*

*Example:*

```
```cpp
vector <complex> v3(5);    // vector of 5 complex numbers
```
```

A class created from a class template is called a *template class*. The syntax for defining an object of a template class is:

```
```cpp
classname<type> objectname(arglist);
```
```

This process of creating a specific class from a class template is called *instantiation*. The compiler will perform the error analysis only when an instantiation takes place. It is, therefore, advisable to create and debug an ordinary class before converting it into a template.

Programs 12.1 and 12.2 illustrate the use of a **vector** class template for performing the scalar product of **int** type vectors as well as **float** type vectors.

# Program 12.1 — Example of Class Template

```
```cpp
#include <iostream>

using namespace std;

const size = 3;
```
```