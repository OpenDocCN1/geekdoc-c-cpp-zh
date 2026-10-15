for errors. For example, as mentioned earlier, a program can easily “walk off” either end of an array, because C++ does not check whether subscripts fall outside the range of an array. Two arrays cannot be meaningfully compared with equality operators or relational operators. As you’ll see in Chapter 8, pointer variables (known more commonly as pointers) contain memory addresses as their values. Array names are simply pointers to where the arrays begin in memory, and, of course, two arrays will always be at different memory locations. When an array is passed to a general-purpose function designed to handle arrays of any size, the size of the array must be passed as an additional argument. Furthermore, one array cannot be assigned to another with the assignment operator(s)—array names are const pointers, and, as you’ll see in Chapter 8, a constant pointer cannot be used on the left side of an assignment operator. These and other capabilities certainly seem like “naturals” for dealing with arrays, but C++ does not provide such capabilities. However, the C++ Standard Library provides class template vector to allow programmers to create a more powerful and less error-prone alternative to arrays. In Chapter 11, Operator Overloading; String and Array Objects, we present the means to implement such array capabilities as those provided by vector. You’ll see how to customize operators for use with your own classes (a technique known as operator overloading).

The vector class template is available to anyone building applications with C++. The notations that the vector example uses might be unfamiliar to you, because vectors use template notation. Recall that Section 6.18 discussed function templates. In Chapter 14, we discuss class templates. For now, you should feel comfortable using class template vector by mimicking the syntax in the example we show in this section. You’ll deepen your understanding as we study class templates in Chapter 14. Chapter 20 presents class template vector (and several other standard C++ container classes) in detail.

The program of Fig. 7.26 demonstrates capabilities provided by C++ Standard Library class template vector that are not available for C-style pointer-based arrays. Standard class template vector provides many of the same features as the Array class that we construct in Chapter 11, Operator Overloading; String and Array Objects. Standard class template vector is defined in header <vector> (line 11) and belongs to namespace std (line 12). Chapter 20 discusses the full functionality of standard class template vector.

Lines 19–20 create two vector objects that store values of type int—integers1 contains seven elements, and integers2 contains 10 elements. By default, all the elements of each vector object are set to 0. Note that vectors can be defined to store any data type, by replacing int in vector<int> with the appropriate data type. This notation, which specifies the type stored in the vector, is similar to the template notation that Section 6.18 introduced with function templates. Again, Chapter 14 discusses this syntax in detail.

```
1 // Fig. 7.26: fig07_26.cpp
2 // Demonstrating C++ Standard Library class template vector.
3 #include <iostream>
4 using std::cout;
5 using std::cin;
6 using std::endl;
7 
8 #include <iomanip>
9 using std::setw;
```

Fig. 7.26 | C++ Standard Library class template vector. (Part 1 of 4.)