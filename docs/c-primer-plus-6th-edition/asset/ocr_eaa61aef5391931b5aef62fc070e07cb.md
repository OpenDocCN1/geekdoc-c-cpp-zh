The Standard Template Library 979

There's too much information about the STL to present in a single chapter, so we'll look at some representative examples and examine the spirit of the generic programming approach. We'll begin looking at a few specific examples. Then, when you have hands-on appreciation for comparators, iterators, and algorithms, we'll look at the underlying design philosophy and then take an overview of the whole STL. Appendix G," STL Methods and Functions," summarizes the various STL methods and functions.

# The vector Template Class

Chapter 4 touched briefly on the vector class. We'll look more closely at it now. In computing, the term vector corresponds to an array rather than the mathematical vector discussed in Chapter 11, "Working with Classes." (Mathematically, an N-dimensional mathematical vector can be represented by a set of N components, in that aspect, a mathematical vector has additional properties, such as inner and outer products, that a computer vector doesn't necessarily have.) A computing-style vector holds a set of values that can be accessed randomly. That is, you can use an index to access the 10th element of a vector without having to access the preceding 9 elements of the varlay and ArrayFP classes introduced in Chapter 14 and to those of the array class introduced in Chapter 4. That is, you could create a vector object, use one vector to another, and use the [] operator to access vector elements. To make the class generic, you make it a template. That's what the STL does, defining a template in the vector (formerly vector.h) header file.

To create a vector template object, you use the usual <type> notation to indicate the type to be used. Also the vector template uses dynamic memory allocation, and you can use an initialization argument to indicate how many vector elements you want:

```
#include vector
using namespace std;
vector<int> ratings(5); // a vector of 5 ints
int n;
cin >> n;
vector<double> scores(n); // a vector of n doubles
```

After you create a vector object, operator overloading for [] makes it possible to use the usual array notation for individual elements: ratings[0] = 9; for (int i = 0; i < n; i++) cout << scores[i] << endl;

# Allocators Again

Like the string class, the various STL container templates take an optional template argument that specifies which allocator object to use to manage memory. For example, the vector template begins like this: