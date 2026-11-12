

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_731_0.png)

Clearly, before you access an element of an array, you must assign it a value. You must assign values to array elements one at a time by using the previously described index notation. Note that, if a and b are arrays of the same type, the assignment a = b is illegal.

The data type of maxTemps is a derived type, which is a type that you derive from the fundamental types by using a declaration operator such as []. Naming a derived type by using a typedef is often useful. Thus, you can write

```
const int DAYS_PER_WEEK = 7;
typedef double ArrayType[DAYS_PER_WEEK];
ArrayType maxTemps;
```

and make ArrayType available for use throughout your program.

**Initialization.** You can initialize the elements of an array when you declare it for the first time. For example,

```
double maxTemps[DAYS_PER_WEEK] = {82.0, 71.5, 61.1, 75.0, 88.3};
```

initializes the first five elements of maxTemps to the values listed and the last two elements to zero.

**Passing an array to a function.** If you wanted a function that computed the average of the first n elements in a one-dimensional array, you could declare the function as

```
double getAverageTemp(double temperatures[], int n);
```

Because the compiler does not know the number of items that the array can hold, you must also pass the function either the size of the array or the number of array items to process. Traditionally, the array is listed as the first parameter and the number of items as the second. You can invoke the function by writing, for example,

```
double avg = getAverageTemp(maxTemps, 5);
```

where maxTemps is the previously defined array.

An array is never passed to a function by value, regardless of how you write its parameter. An array is always passed by reference. This restriction avoids copying of perhaps many array entries. Thus, the function getAverageTemp could modify the elements of maxTemps, even though the array is an input to the function. To prevent such alteration, you can specify the array parameter as a constant reference parameter by preceding its type with const, as follows:

```
double getAverageTemp(const double temperatures[], int n);
```

> You can initialize an array when you declare it

> Arrays are always passed by reference to a function

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_732_0.png)

FIGURE A-7 A two-dimensional array

## A.6.2 Multidimensional Arrays

You can use a one-dimensional array, which has one index, for a simple collection of data. For example, you can organize 52 temperatures linearly, one after another. A one-dimensional array of these temperatures can represent this organization.

An array can have more than one dimension

You can also declare multidimensional arrays. You use more than one index to designate an element in a multidimensional array. Suppose that you wanted to represent the minimum temperature for each day during 52 weeks. The following statements declare a two-dimensional array, minTemps:

```
const int DAYS_PER_WEEK = 7;
const int WEEKS_PER_YEAR = 52;
double minTemps[DAYS_PER_WEEK][WEEKS_PER_YEAR];
```

These statements specify the ranges for two indices: The first index can range from 0 to 6, while the second index can range from 0 to 51. Most people picture a two-dimensional array as a rectangular arrangement, or matrix, of elements that forms rows and columns, as Figure A-7 indicates. The first dimension given in the definition of ArrayType is the number of rows. Thus, minTemps has 7 rows and 52 columns. Each column in this matrix represents the seven daily minimum temperatures for a particular week.

In a two-dimensional array, the first index represents the row, the second index represents the column

To reference an element in a two-dimensional array, you must indicate both the row and the column that contain the element. You make these indications of row and column by writing two indices, each enclosed in brackets. For example, minTemps[1][51] is the element in the 2nd row and the 52nd column. In the context of the temperature example, this element contains the minimum temperature recorded for the 2nd day (Monday) of the 52nd week. The rules for the indices of a one-dimensional array also apply to the indices of multidimensional arrays.

As an example of how to use a two-dimensional array in a program, consider the following program segment, which determines the smallest value in the previously described array minTemps. We use enumerators to reference the days of the week.

```
enum Day {SUN, MON, TUES, WED, THURS, FRI, SAT};

// Initially, assume the lowest temperature is first in the array
double LowestTemp = minTemps[0][0];
Day dayOfWeek = SUN;
int weekOfYear = 1;

// Search array for lowest temperature
for (int weekIndex = 0; weekIndex < WEEKS_PER_YEAR; weekIndex++)
{
    for (Day dayIndex = SUN; dayIndex <= SAT; dayIndex++)
    {
        if (LowestTemp > minTemps[dayIndex][weekIndex])
        {
            LowestTemp = minTemps[dayIndex][weekIndex];
            dayOfWeek = dayIndex;
            weekOfYear = weekIndex + 1;
        } // end if
    } // end for
} // end for

// At this point, lowestTemp is the smallest value in minTemps and
// occurs on the day and week given by dayOfWeek and weekOfYear,
// that is, lowestTemp == minTemps[dayOfWeek][weekOfYear - 1].
```

Although you can declare arrays with more than two dimensions, generally more than three dimensions is unusual. The techniques for working with such arrays, however, are analogous to those for two-dimensional arrays.

> **Programming Tip:** When referencing an element of a multidimensional array, do not use comma-separated indices. For example, myArray[3,6] does not reference the array element myArray[3][6]. The expression 3,6 is a comma expression whose value is that of the last item listed, namely 6. Thus, although myArray[3,6] is legal, its meaning is myArray[6], which references the element myArray[0][6].

### Initialization.

You can initialize the elements of a two-dimensional array just as you initialize a one-dimensional array. You list the initial values row by row. For example, the statement

```
int x[2][3] = { { 1, 2, 3 },
    { 4, 5, 6 } }; // 2 rows, 3 columns
```

initializes the two-dimensional array x so that it appears as

```
1   2   3
4   5   6
```

That is, the statements initialize the elements x[0][0], x[0][1], x[0][2], x[1][0], x[1][1], and x[1][2] in that order. In general, when you assign initial values to a multidimensional array, it is the last, or rightmost, index that increases the fastest.

## A.6.3 Vectors

Another container that can hold data items of the same type is the vector. A vector is similar to a one-dimensional array, but vectors provide additional features for the programmer not found in a simple array. A vector is an object of a standard C++ class named vector. This class is a part of the Standard Template Library, or STL. The STL is a collection of data types you can use in your programs. These data types are not part of the official C++ language, but they have been added to the built-in data types. Section A.9 discusses libraries such as the STL and their usefulness.

To use a vector in your program, you must begin it with the following statements:

```cpp
#include <vector>
using namespace std;
```

You can declare a vector in one of three ways:

- If you know how many elements you want in the vector, you can place the type of data it will hold in angle brackets and the number of elements in parentheses:

```cpp
vector<double> firstVector(10); // Vector to hold 10 doubles
vector<string> myVector(12); // Vector to hold 12 strings
```

The size you specify when declaring the vector is only its initial size. As you will see, a vector can grow in size when you add entries.

- You can place initial values into a vector when you declare it, by writing a second argument:

```cpp
vector<int> intVector(5, -1); // Vector to hold 5 integers, initialized to -1
```

When the elements in the vector are allocated, they are given the value of the second argument.

- You can also create an empty vector—a vector with no elements—by omitting its size and the parentheses:

```cpp
vector<char> letterVector; // An empty vector of characters
```

You can store or access items in a vector by using the [] operator, just as you would when using an array. As for an array, the subscripts that identify elements in a vector start at 0 and go to s - 1, where s is the current size of the vector. The following statements are examples of accessing an existing value in a vector and changing the value of an existing entry:

Access vector entries using [] just as you would an array

```cpp
double x = firstVector[5]; // Places sixth entry in x
myVector[3] = "This is a sample string."; // Sets fourth entry's value
```

Using [] stores a value in an existing element. If you are not sure how many elements the vector has, you can call the method size, as in the following example:

```cpp
cout << intVector.size() << endl; // Displays the number of elements in intVector
```

size returns the number of elements in the vector

By calling the size method, you can determine whether the vector is full. This is an important advantage that a vector has over an array.

If the vector is either full or has no elements—that is, if it was created without elements, as letterVector was previously—you can still add new values by using the method push_back. The push_back method accepts an argument and adds it after the last element of the vector. In other words, it pushes the value onto the back of the vector.

Earlier, we declared a ten-element vector firstVector that could hold data of type double. If that vector was full, and we needed to add the additional values 2.3 and 3.4, we could use the push_back method:

push_back places its argument into a new element at the back of a vector

```cpp
firstVector.push_back(2.3); // Grow vector and store value
firstVector.push_back(3.4); // Grow vector and store value
```

At this point, calling the size method would return 12, since two additional elements have been added to the vector.

pop_back removes the last element from a vector

You also can reduce the size of a vector by removing either its last element or all of its elements. To remove only the last element, you can use the pop_back method. This method shortens

