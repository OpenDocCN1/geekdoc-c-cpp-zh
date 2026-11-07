```
14.4000:  21.9895
21.6000:  30.8952
26.9000:  37.2730
done
```

The valarray class has many features besides the ones discussed so far. For example, if numbers is a valarray<double> object, the following statement creates an array of bool values, with vbool[i] set to the value of numbers[i] > 9—that is, to true or false:

```
valarray<bool> vbool = numbers > 9;
```

There are extended versions of subscripting. Let's look at one—the slice class. A slice class object can be used as an array index, in which case it represents, in general, not just one value but a subset of values. A slice object is initialized to three integer values: the start, the number, and the stride. The start indicates the index of the first element to be selected, the number indicates the number of elements to be selected, and the stride represents the spacing between elements. For example, the object constructed by slice(1,4,3) means select the four elements whose indexes are 1,4,7, and 10. That is, start with the start element, add the stride to get the next element, and so on until four elements are selected. If, say, varint is a vararray<int> object, then the following statement would set elements 1,4,7, and 10 to the value 10:

```
varint[slice(1,4,3)] = 10;    // set selected elements to 10
```

This special subscripting facility allows you to use a one-dimensional valarray object to represent two-dimensional data. For example, suppose you want to represent an array with 4 rows and 3 columns. You can store the information in a 12-element valarray object. Then a slice(0,3,1) object used as a subscript would represent elements 0, 1, and 2—that is, the first row. Similarly, a slice(0,4,3) subscript would represent elements 0,3,6, and 9—that is, the first column. Listing 16.21 illustrates some features of slice.

# Listing 16.21  valice.cpp

```
// valice.cpp -- using valarray slices
#include <iostream>
#include <valarray>
#include <cstdlib>

const int SIZE = 12;
typedef std::valarray<int> vint;    // simplify declarations
void show(const vint & v, int cols);
int main()
{
    using std::slice;                  // from <valarray>
    using std::cout;
    vint valint(SIZE);                 // think of as 4 rows of 3

    int i;
```