tors. As you'll learn in Chapter 8, pointer variables (known more commonly as pointers) contain memory addresses as their values. Array names are simply pointers to where the arrays begin in memory, and, of course, two arrays will always be at different memory locations. When an array is passed to a general-purpose function designed to handle arrays of any size, the size of the array must be passed as an additional argument. Furthermore, one array cannot be assigned to another with the assignment operator(s)—array names are constant pointers, and as you'll learn in Chapter 8, a constant pointer cannot be used on the left side of an assignment operator. These and other capabilities certainly seem like "naturals" for dealing with arrays, but C++ does not provide such capabilities. However, the C++ Standard Library provides class template vector to allow you to create a more powerful and less error-prone alternative to arrays. In Chapter 11, we present the means to implement such array capabilities as those provided by vector. You'll learn how to customize operators for use with your own classes (a technique known as operator overloading).

The vector class template is available to anyone building applications with C++. The notations that the vector example uses might be unfamiliar to you, because vectors use template notation. Recall that Section 6.18 discussed function templates. In Chapter 14, we discuss class templates. For now, you should feel comfortable using class template vector by mimicking the syntax in the example we show in this section. You'll deepen your understanding as we study class templates in Chapter 14. Chapter 22 presents class template vector (and several other standard C++ container classes) in detail.

The program of Fig. 7.25 demonstrates capabilities provided by C++ Standard Library class template vector that are not available for C-style pointer-based arrays. Standard class template vector provides many of the same features as the Array class that we construct in Chapter 11. Standard class template vector is defined in header <vector> (line 5) and belongs to namespace std. Chapter 22 discusses the full functionality of standard class template vector.

```
```cpp
 1  // Fig. 7.25: fig07_25.cpp
 2  // Demonstrating C++ Standard Library class template vector.
 3  #include <iostream>
 4  #include <iomanip>
 5  #include <vector>
 6  using namespace std;
 7
 8  void outputVector( const vector< int > & ); // display the vector
 9  void inputVector( vector< int > & ); // input values into the vector
10
11  int main()
12  {
13     vector< int > integers1( 7 ); // 7-element vector< int >
14     vector< int > integers2( 10 ); // 10-element vector< int >
15
16     // print integers1 size and contents
17     cout << "Size of vector integers1 is " << integers1.size()
18        << "\nVector after initialization:" << endl;
19     outputVector( integers1 );
20
```
```

Fig. 7.25 | C++ Standard Library class template vector. (Part 1 of 4.)