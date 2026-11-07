+   1. We must use the template <> before the header to show that this is the specialization of a template function previously defined.
+   2. We must be careful about replacing T with a specialized type. A C-style string is of type *const char**, which means every time we have T, we must replace it with *const char**.

# ### Overloading

We discussed overloading of regular (nontemplate) functions in Chapter 7. We can apply the same concept to function templates. We can overload a function template to have several functions with the same name but different signatures. Normally, the template type is the same, but the number of parameters is different.

As an example, we overload the *smaller* template function to accept two or three parameters (we call it *smallest* because it uses more than two arguments). Program 15.6 shows the interface. Note that we have defined the second function in terms of the first one. This is why the second function is shorter.

**Program 15.6**  The program for overloaded smaller function

```
```cpp
1  /*********************************************************
2   * Overloaded version of the smaller template function
3   *********************************************************/
4  #include <iostream>
5  using namespace std;
6
7  // Template function with two parameters
8  template <typename T>
9  T smallest (const T& first, const T& second)
10 {
11   if (first < second)
12   {
13     return first;
14   }
15   return second;
16 }
17 // Template function with three parameters
18 template <typename T>
19 T smallest (const T& first, const T& second, const T& third)
20 {
21   return smallest (smallest (first, second), third);
22 }
23
24 int main ( )
25 {
26   // Calling the overloaded version with three integers
27   cout << "Smallest of 17, 12, and 27 is ";
28   cout << smallest (17, 12, 27) << endl;
```
```