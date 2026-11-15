
- 26. Modify program chapter 9_13 to insert all words into the list, then call the member function unique() to remove duplicate words.
- 27. Modify program chapter 9_13 to keep a count of how many times each unique word appears in the text file.
- 28. Write a function that assigns the value v to the first n elements of the array x. Use the prototype:

```
void assignV(double *x, int n, double v);
```

- 29. Write a function that assigns a random value to the first n elements of the array x. Use the prototype:

```
void assignRandom(double *x, int n);
```

![](img/f2bfa570e453b020c16e048c79a3ea0e_504_0.png)

## ENGINEERING CHALLENGE:
Artificial Intelligence

Artificial Intelligence (AI) is an intriguing area of science that focuses on creating intelligent machines that have the ability to “think.” Research in the areas of robotics, cognitive science, language, computing, and sensory perception have advanced the creation of intelligent machines. Today, software exists that can conduct a dialog with human client, beat a world-class chess player, and aid in the diagnosis of disease. Virtual pets are available that “learn” about their environment and respond to their owners. The intelligent software that exists today is only a hint of what is to come.

## ADVANCED TOPICS

## CHAPTER OUTLINE

- Objectives
- 10.1 Generic Programming
- 10.2 Data Abstraction
- 10.3 Problem Solving Applied: Color Image Processing
- 10.4 Recursion
- 10.5 Class Templates
- 10.6 Inheritance
- 10.7 virtual Methods
- 10.8 Problem Solving Applied: Iterated Prisoner's Dilemma
- Summary, Key Terms, C++ Statement Summary, Style Notes, Debugging Notes, and Problems

## OBJECTIVES

In this chapter, we develop problem solutions containing:

- function templates
- overloaded operators
- image processing examples
- recursive member functions
- class templates
- class hierarchies
- an implementation of the iterated prisoner's dilemma game

## 10.1 Generic Programming

Generic programming is a form of programming that supports the implementation of an algorithm, or a type, using a set of parameters rather than a specific type. The C++ programming language supports generic programming through the use of templates. A template is a formal definition of a generic algorithm, or generic type, and can be implemented, or instantiated, by the compiler when referenced with a specific type. The ability to define a concept once, and have the concept implemented automatically for many different types, saves time in the development and testing of problem solutions.

In previous chapters we developed problem solutions that used pre-defined templates from the C++ Standard Library, including vector <type> and random_shuffle(). In this chapter we will illustrate the use of programmer defined templates by writing a set of function templates to perform statistical measures on various sets of data, and a class template to implement the concept of a binary tree.

![](img/f2bfa570e453b020c16e048c79a3ea0e_506_0.png)

The ability to define algorithms and types using templates is a powerful feature of the C++ programming language, but there are some limitations. Templates are not well supported by all compilers, linkers and debuggers. Thus, using templates can result in code that is harder to compile and debug, and code that is less portable.

![](img/f2bfa570e453b020c16e048c79a3ea0e_506_1.png)

To minimize the time spent debugging a template, it is a good idea to first develop a working version of a function, or class, for a specific type. Once a working version has been thoroughly tested and debugged, a template can be defined and the template can be tested against the working version to compare results and performance. For portability, and to eliminate some of the potential linker errors, we will use #include statements in our problem solutions to include the source files that define our templates, thus eliminating the need to link to the object files.

## Function Templates

A function template uses a parameter in the function definition rather than a data type. When a function template is referenced with an argument of a specific type, the compiler generates an instance of the template, replacing the parameter with the specific type of the function argument. Thus, a function template is written once, and multiple versions of the template are instantiated, as needed, by the compiler.

In Chapter 7, we wrote a set of functions to perform statistical measures on a set of data. Each function assumed that the data was in an array of type double. In this section, we will develop a set of function templates to perform statistical measures, then test these templates against the functions developed in Chapter 7. We will begin with the function minval(). The definition of minval(), taken from Chapter 7, is repeated below:

```
```cpp
/*
* This function returns the minimum
* value in an array x with n elements.
*/
double minval(const double x[], int n)
{
// Declare objects.
double min_x;

// Determine minimum value in the array.
min_x = x[0];
for (int k=1; k<n; ++k)
{
if (x[k] < min_x)
min_x = x[k];
}

// Return minimum value.
return min_x;
}
/*---------------------------*/
```
```

The function minval() returns the smallest value found in an array of type double. The algorithm for finding the smallest value in an array is independent of the data type of the array, thus minval() is a good candidate for a function template.

The definition of a function template begins with an expression of the form: template<typename identifier>.

The identifier in this expression provides a name for a parameterized type, and this identifier is used in the function definition in place of a specific type. The definition of a function template named minVal() is provided below:

```
/*
 ************************************************************/
/* Function returns the minimum value in an */
/* array of type Dtype and size n. */
/*
************************************************************/
template <typename Dtype>
Dtype minVal(const Dtype x[], int n)
{
// Declare objects.
Dtype minX;
// Determine minimum value in the array.
minX = x[0];
for (int k=1; k<n; ++k)
{
if (x[k] < minX)
minX = x[k];
}
// Return minimum value.
return minX;
}
/*
************************************************************/
```

Note that the only difference between the statement block that defines minVal() and the statement block that defines the function template minVal() is that the data type double in minVal() has been replaced with the parameter Dtype. The prototype for this function template is:

```
template <typename Dtype>
Dtype minVal(const Dtype x[], int n);
```

### Function Templates: A function template is a parameterized function definition.

```
Syntax:
template<typename identifier1 [,typename identifier2,...] >
return-type function name(parameter list)
{
//Statement block
}
```

```
Example:
template<typename Dtype>
void swapTwo(Dtype& a, Dtype& b)
{
Dtype temp = a;
a = b;
b = temp;
}
```

```
Prototype:
template<typename Dtype>
void swapTwo(Dtype& a, Dtype& b);
```

![](img/f2bfa570e453b020c16e048c79a3ea0e_508_0.png)
![](img/f2bfa570e453b020c16e048c79a3ea0e_508_1.png)

The keyword `template`, followed by a parameter list enclosed within <> symbols, must precede a function template definition and a function template prototype. Within the parameter list the keyword `typename` precedes each identifier in the list, indicating that the identifier represents a data type. The template parameter list must include at least one parameter. If multiple parameters are used, they are separated with commas, as in:

```
template <typename T1, typename T2, typename T3>
```

The following program calls the function template `minVal()` four times to find the smallest value in arrays of type `int`, `char`, `double`, and `string`.

```
/*--------------------------------------------------------------*
| Program chapter10_1                                          |
|                                                              |
| This program demonstrates the use of the function            |
| template minVal.                                             |
*--------------------------------------------------------------*/
#include<iostream> //Required for cout.
#include<string> //Required for string.
using namespace std;
//Function Prototype
template <typename Dtype>
Dtype minVal(const Dtype x[], int n);
int main()
{
 //Declare objects.
 const int SIZE = 10;
 char ch[SIZE] = {'h','e','l','l','o',' ','w','o','r','l','d'};
 int idat[SIZE] = {5,2,7,8,2,5,9,8,1,9};
 double ddat[SIZE] = { -2.1,4.3,0.0,9.3,0.4,-4.2};
 string sdat[SIZE] = {"this","short","the","list","of","strings"};
 //Print smallest value in each array.
 cout << "\nSmallest value in ch array."
 << "\n" << minVal(ch,SIZE) << endl; // Char
 cout << "\nSmallest integer in idat is "
 << minVal(idat,SIZE) << endl; // int
 cout << "\nSmallest double in ddat is "
 << minVal(ddat,6) << endl; // double
 cout << "\nSmallest string in sdat is "
 << minVal(sdat,6) << endl; // string
 return 0;
}
/*--------------------------------------------------------------*/
```
