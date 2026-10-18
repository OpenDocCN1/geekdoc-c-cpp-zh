This matrix is ready for use, as shown in the _Easy_Matrix_First_Test_ function in Listing 3.5.

```
```
Listing 3.5 Definition of the Easy_Matrix_First_Test function using RealMatrix for matrix operations (part of EMTest.cpp).
void Easy_Matrix_First_Test( void )
{
// Using RealMatrix as it is
RealMatrix m = {
{ 2, 2, 0, 11 },
{ 3, 4, 5, 0 },
{ -1, 2, -1, 7 }
};
// Add next row
m.push_back( { 5, 3, 5, -3 } );
// Accumulate elements except the diagonal
double non_diagonal_sum {};
for( int r = 0; r < m.size(); ++ r )
for( int c = 0; c < m[ 0 ].size(); ++ c )
if( c != r )
non_diagonal_sum += m [ r ] [ c ];
std::cout << "Sum of m except the diagonal " << non_diagonal_sum << std::endl;
}
```
```

A matrix m of type RealMatrix is defined and initialized on lines [20-24]. As we already know, RealMatrix is a vector of vectors. Therefore, it is initialized exactly the same way. More precisely, the initializer lists, each encompassed in { } brackets, are used to set up values for each row. Then the rows are set in order, one after the other, to constitute a matrix. This matrix’s dimensions are three rows by four columns. However, we would like to have a square matrix, so on line [27], another is pushed back. After that, m represents a 4×4 matrix.

Then, on lines [32-35], the sum of only the diagonal elements of m is computed. To do this, two for loops are used (Section 3.13.2.2). The first, from line [32], advances its iterator r from 0 to the number of rows in m. This is read as m.size(), since the size of m is its number of elements: that is, the number of vectors of vectors, each containing data from the consecutive row. The second for on line [33] traverses each element in a single row: that is, in a single vector. To do this, its iterator variable c iterates from 0 to m[ 0 ].size(). Let’s explain this: m[ 0 ] is the first element: the first row of vectors. This is a std::vector< double >, so it has its own size, which is accessed by calling the size function on it (with help of the dot . operator). Then, on line [34], to verify whether a diagonal element is processed, the row number is compared to the column number. Only non-diagonal elements of m are added together and finally displayed on the screen identified by the std::cout object.

As we can see, RealMatrix allows for some matrix operations. However, its use is limited, so we will expand this example in Section 3.15.