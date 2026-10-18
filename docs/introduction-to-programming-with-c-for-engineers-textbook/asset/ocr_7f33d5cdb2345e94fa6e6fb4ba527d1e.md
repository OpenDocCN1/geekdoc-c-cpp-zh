The definition of the overloaded operator << starts on line [2]. Remember that this is a separate function, declared in `EMatrix` as a friend. It always takes two parameters; the first is the out reference to `std::ostream`, which in C++ represents a broad group of output streaming objects, such as the familiar `std::cout`; the second parameter is always an object to be streamed out, `matrix` in our case, passed by a constant reference. Since we have a matrix to be streamed out, two loops are started on lines [4, 6]. The first one traverses rows of the input matrix parameter using the `const auto &` construction (Section 3.7). Such a convenient version of the `for` loop is possible thanks to the begin and end functions defined in EMatrix. Otherwise, we’d be left with the older version of `for`, operating with an iterator and calling the `EMatrix::GetRow` function. The second internal loop on line [6] traverses the data in each row, which is then output on line [7] to the out stream, separated by a tabulator (`\t`). After writing the entire row, a newline symbol is output on line [9], and so on, until all the rows are saved. Finally, on line [12], the stream object `out` is returned, so the << operations can be chained in one line, as we have done before.

```
```cpp
// Stream out a matrix to the stream out. Assume text mode.
std::ostream & operator << ( std::ostream & out, const EMatrix & matrix )
{
    for( const auto & row : matrix )      // go row-by-row
    {
        for( const auto & data : row )    // data in a single row
            out << data << "\\t";

        out << std::endl;
    }

    return out;        // return the stream, so they can be chained
}
```
```

The implementation of operator >>, starting on line [15], is a little bit more complicated, mostly because we need to interpret what is read in. First, let’s analyze the two parameters of this function: `in`, which is a reference to the `std::istream`-derived object; and a matrix, which is a reference to an `EMatrix` object. That is, the EMatrix object must already have been created, so it can then be passed for input. But it can be empty, since on line [22], its current contents are cleared.

```
```cpp
// Stream in a matrix from the stream in. Assume text mode.
std::istream & operator >> ( std::istream & in, EMatrix & matrix )
{
    // Dimensions have to be determined from the data layout.
    // Each new line constitutes a new row of a matrix.
    // So, we have to read strings line by line, and
    // from each string read data by data.

    matrix.fData.clear();        // get rid of whatever was there

    std::string str;              // an empty string
    while( getline( in, str ) )   // read the entire line into the string
    {
        // create a string-stream from a string
```
```