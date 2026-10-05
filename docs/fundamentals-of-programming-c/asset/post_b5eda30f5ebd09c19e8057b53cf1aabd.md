
# 17.8. EXERCISES

context that expects an ostream object reference or pointer, and ifstream objects can be used when an istream object is required.

- The specifier is protected as far as most code outside the class is concerned, but it works "public" to code within derived classes. Subclass methods can see and manipulate inherited protected methods, but subclasses cannot directly see inherited private data and cannot call inherited protected methods.

- Polymorphism in object-oriented languages is a process by which the code executed during invocation is determined at runtime, not compile time.

- Polymorphism in C++ requires three key ingredients:
  - inheritance—a class overrides a method in its base class
  - virtual methods—an overridden virtual method can use dynamic binding (code to execute is determined at runtime) rather than static binding (compiler determines the code to execute)
  - method calls through pointers or references—a pointer's declared type is of the base class, but the actual type of the object to which it points may be a derived class. The relationship enables the process to work correctly.

- A derived class may override a public method that is declared virtual in the base class. Such virtual methods enable polymorphism.

- A pure virtual method (or pure function) has no defined body and is indicated by the "= 0" syntax.

- A class that contains at least one pure virtual function is known as an abstract class. It is illegal to attempt to create an instance of an abstract class. Abstract classes serve to organize hierarchies of classes related through inheritance. Classes that are not abstract are concrete classes.

# 17.8 Exercises

- 1. Overload the operator<< so it accepts an ostream reference and a two-dimensional vector of Boolean values. The function should print the contents of the 2D vector in a table; for example, a four-row, five column print might look like:

```
true  false  true   true   true
false  true   false  false  false
false  false  false  false  false
true   false  true   true   true
```

Note that the words true and false, not simply 0 or 1. Once you have the function using the count object, demonstrate that you can save the contents of any 2D Boolean vector to a text file.

- 2. Consider the following C++ code:
```cpp
class Widget {
public:
  virtual int f() { return 1; };
};

class Gadget: public Widget {
public:
    virtual int f() { return 2; }
};

class Gizmo: public Widget {
public:
    virtual int f() { return 3; }
};

void do_it(Widget *w) {
    cout << w->f() << " ";
}

int main() {
    vector<Widget *> widgets;
    Widget wid;
    Gadget gad;
    Gizmo giz;
    widgets.push_back(&wid);
    widgets.push_back(&gad);
    widgets.push_back(&giz);
    for (size_t i = 0; i < widgets.size(); i++)
        do_it(widgets[i]);
}
```

- (a) What does the program print?
(b) Would the program still compile and run if the f method within the Widget class were a pure virtual function?
(c) How would the program run differently if the virtual keyword were removed from all the code?
(d) Would the program behave the same if the virtual keyword were removed from all the classes except for Widget?

# Chapter 18

# Generic Programming

The flexible sorting examples in Listing 12.2 (flexibleint.cpp), Listing 16.5 (loggingflexiblesort.cpp), and Listing 17.20 (polymorphsort.cpp) allow us to arrange the elements in integers in creative ways and perform other interesting activities such as logging. These examples demonstrate the power of function pointers, inheritance, and polymorphism. As flexible and powerful as these techniques, they all contain one major limitation: they deal with vectors of integers only. Consider the Compar class from Listing 17.23 (compar.h) and Listing 17.19 (compar.cpp), and the "flexible" selection_sort function from Listing 17.23 (loggingsort.cpp). The selection_sort function accepts a vector of integers and a Compar reference. What if we need to sort a vector of double-precision floating-numbers or a vector of string objects? Unfortunately, all of this "flexible" code cannot handle this seemingly minor variation.

In this chapter we show how C++ template mechanism enables programmers to develop truly generic algorithms and data structures. We will see how the standard C++ library has embraced the template technology to provide a wealth of generic algorithms and data structures that greatly assist developers in the construction of quality software.

# 18.1 Function Templates

Consider the following comparison function found in Listings 12.2, 16.5, and 17.23:

```cpp
/*
* less_than(a, b)
* Returns true if a < b; otherwise, returns
* false.
 */
bool less_than(int a, int b) {
    return a < b;
}
```

Listing 18.1 (testlessthan.cpp) tests the less_than function with various arguments.

# 18.1 FUNCTION TEMPLATES

# Listing 18.1: testlessthan.cpp

```cpp
#include <iostream>

using namespace std;

/*
 * less_than(a, b)
 * Returns true if a < b; otherwise, returns
 * false.
 */
bool less_than(int a, int b) {
    return a < b;
}

int main() {
    cout << less_than(2, 3) << endl;
    cout << less_than(2.2, 2.7) << endl;
    cout << less_than(2.7, 2.2) << endl;
}
```

The compiler generates warnings for the last two sentences. The **less_than** function expects two integer arguments, but the calling code sends double-precision floating-point values. The automatic conversion from **double** to **int** can lose information, hence the warnings. The output of Listing 18.1 (testlessthan.cpp) shows that we should take these warnings seriously:

| 1 |
| :--- |
| 0 |
| 0 |

Obviously 2 < 3 and 2.7 > 2.2. The automatic conversion from **double** to **int** truncates. The situation is even worse for the following code:
```cpp
string word1 = "ABC", word2 = "XYZ";
cout << (word1 < word2) << endl; // This will not compile
cout (word2 < word1) << endl; // This produced the expected output
```

The C++ standard library provides a operator< function that compares two **string** objects lexicographically.

# 18.1 Function Templates

As another example, consider the following function that computes the sum of the elements in a vector:

```cpp
int sum(const vector<int>& v) {
    int result = 0;
    for (int elem : v) {
        result += elem;
    }
    return result;
}
```

The following client code works:
```cpp
vector<int> v {10, 20, 30};
cout << sum(v) << endl;
```

The following code does not compile:
```cpp
vector<double> v {10, 20, 30};
cout << sum(v) << endl;
```

This duplicated effort is unsatisfactory. These two overloaded functions are identical except for the types. The actions of the two functions—initialization, vector traversal and arithmetic—are essentially the same. In general, code duplication is undesirable. A programmer who discovers an error in one of the functions must remember to apply the corresponding correction to the function's overloaded counterpart.

Both the less_than functions share a common shortcut: they are tied to a particular type. It would be convenient to specify the type and let the compiler fill in the fields. In the case of less_than we would be able to write a function that uses the < operator for parameters of any type which is compatible. For sum, we would like to create a generic function that works for any numeric type.

C++ enables us to write generic functions via templates. A template function specifies a pattern of code, and either the programmer or the compiler supplies the exact type as needed. Listing 18.2 (templatesleshan.cpp) uses C++s template mechanism to create a generic less_than function.

# Listing 18.2: templatesleshan.cpp

```cpp
#include <iostream>
#include <string>

using namespace std;
```
