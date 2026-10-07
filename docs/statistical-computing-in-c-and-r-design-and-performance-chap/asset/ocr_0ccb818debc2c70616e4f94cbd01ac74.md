108

A SKETCH OF C++

3.31. Similar to Exercise 3.30, create a template class version of your class Vector from Exercise 3.32. As in Exercise 3.30, the template parameter must be used when the return type is a Vector object or a reference or pointer to a Vector object. For example, the return type for the overloaded + operator is Vector<T>.

3.32. Lists provide useful constructs for holding and managing data. As a minimal level of functionality is a list

+   a) holds of a particular type and expand or contract objects as are inserted or re-moved,

+   b) maintain a count of the number of objects in the list and

+   c) allow for access to any element in the list.

Create a list that can hold objects of a common (but arbitrary) type with the maximum size of the list being in the class constructor. List elements are identified by the value of a string that holds their names. Overload [] to access to the list elements by their names.

3.33. Create a file input inputFile read an array whose elements are any of the primitive data types and the dimension of the array is either read from the command line or in the first line of the input file. Demonstrate via an example that your class performs expected.

3.34. Create a data summary class that will produce statistics for an nRows x nCols array of doubles that are stored in the form of a pointer to double[] variables as columns. In particular, provide a method that uses the West algorithm from Section 2.6 to compute both the means and deviations for variables.

3.35. Create a template function that will read and write arrays of arbitrary sizes consisting of any of the primitive data types and from specified files.

3.36. Create a template function that adds addition for objects of class that supports the + operator. Demonstrate that it works with objects of type Matrix as well as those from your class Vector developed in Exercise 3.32.

3.37. Create a template function that will swap two objects of a given class (i.e., the objects' members are switched from one to the other) on the bases of the relational operators < and ==. Apply your function to a struct X with two int members a and b where ordering is in terms of only the member

3.38. In Exercise 3 get using standard input cin to read lines of input from the shell. This function also uses ifstream. For example, if inputFile is an ifstream and s is a string, getline(inputFile, s) will read a line of input from the file connected to inputFile until it reaches it the end-of-file or ii the newline character. In the latter instance, the newline character is discarded effectively moving the next operation to the next line of the file. Write a program that will run in a file containing 23 numbers: four on the first five rows of the file and three on the last row. Return the results to the shell that will produce output consisting of three rows with eight numbers on the first row, 11 on the second and on the third.

3.39. Create a class that has methods for computing the standard statistical tests associated with location parameters such as

+   a) the Wilcox signed-rank, statistic,

+   b) the paired t-statistic,

+   c) the two-sample t-statistic with a pooled variance estimator and

+   d) the two-sample Mann-Whitney U statistic.