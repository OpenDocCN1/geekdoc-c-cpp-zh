
```cpp
cout << data.size() << "\n";      // Output: 0
data.resize(100);                            // enlarged
cout << data.size() << "\n";              // Output: 100
valarray<int> data2(200);                       // space for 200 values
cout << data2.size() << "\n";              // Output: 200
valarray<int> dataC(5, 20);                   // twenty ss, different from vector
cout << dataC[6] << "\n"; // Output: 20:
data[6]=5;
valarray data(2, 3, 5, 7, 11); // valarray<int>, initialization list
cout << data.size() << ":" << data[3] << "\n"; // Output: 5:
data[3]=7;
```

As you can see, you can also redefine a number of values with initial values. But beware: the two valarray(value, size) parameters are in the opposite order compared to vector! It is better to get used to defining valarray only with a number for the size or initialization list.

Copying and moving are also allowed.

Each of the slice_array, gslice_array, mask_array, and indirect_array helper classes can also be specified as a source for initialization. Note that these constructors are not marked with explicit, allowing implicit conversion for parameters and returns.

## 24.12.3 Assignment
The assignment operator operator= supports the same parameters as the constructor.

There is no assign like in any other (real) containers, but at least there is a swap.

## 24.12.4 Insert and Delete
You cannot really insert like with insert. However, you can access the elements for reading and writing with operator[]. Access is not checked; you must take care of the range boundaries yourself. There is no at() method for this.

However, you can still change the size of a valarray afterward. For this, there is the resize method:

- * resize(size_t size, T value)—enlarges or reduces, truncates or initializes with value

It is possible that all data will be copied during this operation. Pointers and iterators into the valarray therefore become invalid.

> The operator[] is almost magical in valarray. It can not only handle an integer index to address a single element, but it can also use slices, masks, and indirections as an index.

In fact, the aforementioned helper classes are used as an index, but in practice, many type conversions occur here, so you work with the following types as an index:

- * Slice
You either slice or gslice.

- * Mask
You take a valarray<bool> of the same size as the data valarray<T>.

- * Indirection
You take a valarray<size_t> of the same size as the data valarray<T>.

## Consider the following example:

```cpp
// https://godbolt.org/z/PeG4K7Edc
vararray v {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12};
vararray<int> r1(v(slice(0, 4, 3))); // Start at 0, 4 elements, step size 3
cout << r1; // Output: 1 4 7
vararray<int> r2(v > 6); // addressed by vararray<bool>
cout << r2; // Output: 7 8 9 10 11 12
const vararray<size_t> indirect{2, 3, 6}; // duplicates allowed
vararray<int> r5(v(indirect)); // addressed by vararray<size_t>
cout << r5; // Output: 3 4 7
```

## 24.12.6 Specialty: Manipulate All
There are a handful of useful methods for information or manipulation over all data in the vararray:

- sum, min, and max
Calculate the sum, the minimum, and the maximum over all values. With a normal container, you would instead use, for example, accumulate or max_element from <algorithm>.

- shift and cshift
Shift and rotate the values around the entire vararray. shift rotates; cshift fills with zeros.

- apply
This calls a function for each element in the vararray. The function must take a T as an argument and return a T. You cannot modify the element. Overall, you get a new valarray back from apply. With normal containers, you would probably use for_each.

- * Integer, floating point, boolean, and bitwise arithmetic
You can modify all values of a valarray simultaneously using all built-in operators: +, *, =, &&, <<, and so on.
You can specify either a single value (scalar) or, if appropriate, another valarray as the other operand.
Writing va * vb is identical to va[0]*vb[1]; va[1]*vb[1]; ...
This applies to all binary operators.

- * Mathematical functions
For valarray, a multitude of mathematical functions are overloaded, which then apply element-wise to all contained values. Examples include abs, exp, sqrt, log10, sin, cos, asin, and cos. You receive a new valarray each time, as if apply(func) had been called.

- * Comparison operations
You can use operator> and like to compare all elements of valarray against either a single value or another valarray. You get back a valarray<bool>

## 24.12.7 Specialty: Slicing and Masking
The specialty compared to normal containers is that you can slice a valarray with helper classes to select only parts of it. These slices can be complicated and, for example include a step size, thus simulating multidimensionality. With masking, you can exclude parts of valarray from operations. A slice helper object represents a complicated index, similar to how a[12] would work in normal array. You create a slice helper object with one constructors:

- slice()—empty slice
- slice(size_t start, size_t size, size_t stride)—parameters for start, size, and stride
- slice(const slice& other)—for copy

You can then use this helper object as an index in []. You get back a valarray or a proxy object that can be converted into valarray. For example, if you have valarray with values from 1 to 12, slice(0,4,3) addresses the values 1, 4, and 7, which are exactly the values that would occupy the first column of a 3 × 4 matrix. While slice extracts a one-dimensional slice from a two-dimensional matrix, the gslice class is used for multidimensional slices. For example, if you consider values 1 to 12 as a three-dimensional cuboid of size 2 × 3 × 2, then v[gslice({0, 2}, {6,2})] addresses the two-dimensional slice of the front 2 × 3 face with values 1, 3, 5 and 7, 9, 11:

```cpp
// https://godbolt.org/z/ehP47v
valarray<int> v {
1, 2, 3,
4, 5, 6,
7, 8, 9,
10, 11, 12};
v(0, 4, 3) = valarray<int>(v[slice(0, 4, 3)]); // square the first column
cout << v; // Output: 1 2 9 10 5 6 8 10 11 12
v(0, 4, 3) = valarray<int>{1, 7, 10}; // restore
valarray<int> r3(gslice({0, 2}, {6,2})); // 2-D slice from 3-D cube
cout << r3; // Output: 1 3 5 7 9 11
valarray<char> text("now it starts", 20);
valarray<char> caps("NIRS", 4);
valarray<size_t> idx{0, 4, 7, 14}; // Indexes in text
text[idx] = caps; // assign indirectly

cout << text; // Output: Now It Really Starts
```

First, the program interprets the valarray v as a two-dimensional matrix of size 2 × 3. With a simple slice, I address the first column and multiply it by itself using *=. As a result, you see only 1, 4, 7, and 10 were overwritten.

For clarity, I then restore the original state, as the next step interprets the 12 values as a three-dimensional object—that is, a cuboid with edge lengths 2 × 3 × 2. Here, gslice cuts out a two-dimensional piece.

Finally, I use a valarray<size_t> as an argument for operator[] to perform an indirect assignment of data valarray. text[idx] = caps assigns new values to the letters addressed by idx.

In multiplication, you might know that a matrix of size 2 × 4 can be multiplied by another matrix of size 4 × 2; in this product, the rows of one matrix are multiplied by the columns of the other matrix. For this, you can also use valarray with clever slicing:

```cpp
// https://godbolt.org/z/hf8qz5xs
#include <iostream>
#include <iomanip> // setw
#include <valarray>
using namespace std;

/* Print matrix */
template<class T>
void printMatrix(ostream&os, const valarray<T>& a, size_t n) {
  for(size_t i = 0; i < (n*n); ++i) {
    os << setw(3) << a[i];      // Print value
    os << ((i+1)%n ? '' : '\n');   // next line?
  }
}
```

```cpp
/* Matrix cross product */
template<class T>
valarray<T> matult(
    const valarray<T>& a, size_t arows, size_t acols,
    const valarray<T>& b, size_t brows, size_t bcols) {
    /* Condition: acols = brows */
    valarray<T> result(arows * bcols);
    for(size_t i = 0; i < arows; ++i)
        for(size_t j = 0; j < bcols; ++j) {
            auto row = a[slice(acols*i, acols, 1)]; // Row
            auto col = b[slice(j, brows, bcols)]; // Column
            result[i*bcols+j] = (row*col).sum(); // Cross product of rows
        }
    }
    return result;
}

int main() {
    constexpr int n = 3;
    valarray ma{1,0,-1, 2,2,-3, 3,4,0}; // 3 x 3 matrix
    valarray mb{3,4,-1, 1,-3,0, -1,1,2}; // 3 x 3 matrix
    printMatrix(cout, ma, n);
    cout << " -times-\n";
    printMatrix(cout, mb, n);
    cout << " -results in:-\n";
    valarray<int> mc = matult(ma, n, n, mb, n, n);
    printMatrix(cout, mc, n);
}
```
