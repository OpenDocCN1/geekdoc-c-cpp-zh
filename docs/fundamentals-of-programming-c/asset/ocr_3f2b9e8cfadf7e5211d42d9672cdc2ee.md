# 11.2. ARRAYS

292

```
}
void print_matrix(const Matrix m) {
  for (auto row : m) {
    for (double elem : row)
      cout << setw(5) << elem;
    cout << endl;
  }
}

int main() {
  int rows, columns;
  cout << "How many rows ?";
  cin >> rows;
  cout << "How many columns ?";
  cin >> columns;
  // Declare the 2D vector
  Matrix mat(rows,vector<double>(columns));
  // Populate the vector
  populate_matrix(mat);
  // Print the vector
  print_matrix(mat);
}
```

An expression that uses just index with a 2D vector represents a single row within the 2D vector. This row is itself a 1D vector. If a is a 2D vector and i is an integer, then the expression

```
a[i]
```

We can build vectors with dimensions higher than two. Each “slice” of a 3D vector is simply a 2D vector, a a vector of 3D vectors. For example, the statement

```
matrix[x][y][z] = 1.0034;
```

assigns 1.0034 to an element in a 4D vector of doubles. In practice, vectors with more than two dimensions are rare, but advanced scientific and engineering applications sometimes require higher-dimensional vectors.

# 11.2 Arrays

C++ is an object-oriented programming language, and a vector is an example of a software object. The C programming language does not directly support object-oriented programming, and therefore does not have vectors to represent aggregate types. The C language uses a more primitive construct called an array. C++, as an extension of C, supports arrays as well as vectors. Some C libraries use arrays instead of vectors. C++ can use any the large number of C libraries that have been built up over the past 40 years, and many of these libraries processes arrays.

An array is what refers to a block of memory that, like a vector, hold multiple values simultaneously. An array has a name, and the values it contains are accessed via their position within the block of memory designated for that. Also like a vector, the elements within an array must be all of

©2014 Richard L. Halterman

Draft date: January 26, 2014