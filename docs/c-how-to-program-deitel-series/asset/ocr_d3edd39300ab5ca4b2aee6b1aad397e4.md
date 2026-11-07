# *Nested Range-Based for Statements*

To process the elements of a two-dimensional array, we use a nested loop in which the *outer* loop iterates through the *rows* and the inner loop iterates through the *columns* of a given row. Function printArray’s nested loop is implemented with range-based for statements. Lines 27 and 30 introduce the C++11 `auto` keyword, which tells the compiler to infer (determine) a variable’s data type based on the variable’s initializer value. The outer loop’s range variable `row` is initialized with an element from the parameter `a`. Looking at the array’s declaration, you can see that the array contains elements of type

```
```cpp
array< int, columns >
```
```

so the compiler infers that `row` refers to a three-element array of int values (again, columns is 3). The const & in row’s declaration indicates that the reference cannot be used to modify the rows and prevents each row from being copied into the range variable. The inner loop’s range variable `element` is initialized with one element of the array represented by `row`, so the compiler infers that `element` refers to an int because each row contains three int values. In an IDE, you can typically hover your mouse over a variable declared with auto and the IDE will display the variable’s inferred type. Line 31 displays the value from a given row and column.

# *Nested Counter-Controlled for Statements*

We could have implemented the nested loop with counter-controlled repetition as follows:

```
```cpp
for ( size_t row = 0; row < a.size(); ++row )
{
   for ( size_t column = 0; column < a[ row ].size(); ++column )
      cout << a[ row ][ column ] << ' ';
   cout << endl;
} // end outer for
```
```

# *Other Common array Manipulations*

Many common array manipulations use `for` statements. For example, the following for statement sets all the elements in row 2 of array a in Fig. 7.19 to zero:

```
```cpp
for ( size_t column = 0; column < 4; ++column )
   a[ 2 ][ column ] = 0;
```
```

The `for` statement varies only the second subscript (i.e., the column subscript). The preceding `for` statement is equivalent to the following assignment statements:

```
```cpp
a[ 2 ][ 0 ] = 0;
a[ 2 ][ 1 ] = 0;
a[ 2 ][ 2 ] = 0;
a[ 2 ][ 3 ] = 0;
```
```

The following nested counter-controlled `for` statement determines the total of *all* the elements in an array a in Fig. 7.19:

```
```cpp
total = 0;
for ( size_t row = 0; row < a.size(); ++row )
   for ( size_t column = 0; column < a[ row ].size(); ++column )
      total += a[ row ][ column ];
```
```