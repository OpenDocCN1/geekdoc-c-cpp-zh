**E6.20** Write a function
```
vector<int> merge_sorted(vector<int> a, vector<int> b)
```
that merges two sorted vectors, producing a new sorted vector. Keep an index into each vector, indicating how much of it has been processed already. Each time, append the smallest unprocessed element from either vector, then advance the index. For example, if a is
1 4 9 16
and b is
4 7 9 9 11
then merge_sorted returns the vector
1 4 4 7 9 9 9 11 16

**E6.21** Write a function that modifies a vector<string>, moving all strings starting with an uppercase letter to the front, without otherwise changing the order of the elements.

**E6.22** Write a function that counts the number of distinct elements in a vector<string>. Do not modify the vector.

**E6.23** Write a function that finds the first occurrence of a value in a two-dimensional array. Return an int array of length 2 with the row and column, or null if the value was not found.

**E6.24** Write a function that checks whether all elements in a two-dimensional array are identical.

**E6.25** Write a function that checks whether all elements in a two-dimensional array are distinct.

**E6.26** Write a function that checks whether two two-dimensional arrays are equal; that is, whether they have the same number of rows and columns, and corresponding elements are equal.

**E6.27** Write a function that swaps two rows of a two-dimensional array.

**E6.28** Write a function that swaps two columns of a two-dimensional array.

# PROGRAMMING PROJECTS

**P6.1** A run is a sequence of adjacent repeated values. Write a program that generates a sequence of 20 random die tosses and prints the die values, marking the runs by including them in parentheses, like this:
1 2 (5 5) 3 1 2 4 3 (2 2 2) 3 6 (5 5) 6 3 1
Use the following pseudocode:

```
in_run = false
For each valid index i in the array
  if in_run
    if values[i] is different from the preceding value
      Print )
      in_run = false
```