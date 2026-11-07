![](bbox=[0.23, 0.085, 0.84, 0.19])

Figure 15.1 A function template is instantiated into several functions

# Nontype Template Parameter

Sometimes we need to define a value instead of a type in our function template. In other words, the type of a parameter may be the same for all template functions that we want to use. In this case, we can define a template, but the type cannot be specifically defined.

Assume we want a function that prints the elements of any array regardless of the type of the element and the size of the array. We know that the type of each element can vary from one array to another, but the size of an array is always an integer (or unsigned integer). We do so using Program 15.4. We have two template parameters, T and N. The parameter T can be any type; the parameter N is a nontype (the type is predefined as integer).

# Program 15.4 Printing an array

```
~~~cpp
/********************************************************
 * A program that uses a template function to print elements of
 * any array of any type
 ********************************************************/

#include <iostream>
using namespace std;

// Definition of the print template function
template <typename T, int N>
void print (T (&array) [N])
{
   for (int i = 0; i < N ; i++)
   {
      cout << array [i] << " ";
   }
   cout << endl;
}

int main ()
{
   // Creation of two arrays
   int arr1 [4] = {7, 3, 5, 1};
   double arr2 [3] = {7.5, 6.1, 4.6};
   // Calling template function
   print (arr1);
~~~
```

(continued)