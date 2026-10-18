theDbArray, which is the same size as theArray, is created on line [24]. This time, it holds elements of double type. We already know that it will not be initialized automatically. Therefore, on line [27], elements of theArray are copied to theDbArray object with the std::copy function. Note that the elements are converted from unsigned int to double on the fly.

```
```cpp
// Make the same size as theArray
array< double, theArray.size() > theDbArray;

// Copy and convert int to double
copy( theArray.begin(), theArray.end(), theDbArray.begin() );

copy(    theDbArray.begin(), theDbArray.end(),
         ostream_iterator< double >( cout, " " ) );
```
```

Finally, std::copy is used again on lines [29–30] to display all the elements of theDbArray array. More precisely, the output is performed by the ostream_iterator for double, attached to the std::cout stream.

It is worth noting that std::array is a wrapper class around the built-in fixed-size arrays, discussed in Appendix A.2.1. A wrapper class will be presented in Section 3.15.

# 3.10.1  Multidimensional Fixed-Size Arrays

In a straightforward way, we can create arrays that contain other arrays and thus obtain multidimensional fixed-size arrays. Let’s consider Listing 3.8, which shows how to create a simple 2D structure with two rows and three columns (i.e. a matrix), holding floating-point objects.

# Listing 3.8  Examples of using std::array to define multidimensional fixed-size arrays (in CppBookCode, VectorsStringsArrays.cpp).

```
```cpp
enum ArrayDims { kCols = 3, kRows = 2 };   // Define two constants

using ArrayElem = double;

// Declare a single array of kCols elems
using _1D_Array = std::array< ArrayElem, ArrayDims::kCols >;

// Declare a matrix with kRows
using _2D_Array = std::array< _1D_Array, ArrayDims::kRows >;

_2D_Array matrix { 0.0 };   // Create a matrix and init with zeros
```
```

The dimensions of a fixed-size array need to be known at compile time. For this purpose, we can define a const int object; but in this example, we use the other option, which is the enumerated type ArrayDims and its constant values kCols and kRows, as defined on line [1]. This is an