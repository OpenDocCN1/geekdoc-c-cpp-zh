# EXERCISES

3.20. Create methods for class Matrix that provide analogs of the R cbind and rbind functions discussed in Appendix B.

3.21. Create functions for class Matrix that will

+   a) insert a specified Vector object into a specified column of a Matrix object and
b) extract a specified column from a Matrix object and return it as an object of class Vector.

3.22. Expand the class Vector from Section 3.9 to include

+   a) an overloaded + operator for vector addition,
b) an overloaded += operator for vector addition,
c) an overloaded * operator that computes a dot (or inner) product,
d) overloaded * operators that compute the left- and right-hand products of a vector and a scalar,
e) overloaded *= operators that compute the left- and right-hand products of a vector and a scalar,
f) overloaded ^ operator that raises every component of a vector to a specified integer power,
g) an overloaded << operator that provides a print utility function for the class. [Hint: Exercise 3.19].

Demonstrate through an example that all the operators/methods you have created for the class as expected.

3.23. Create a complex number class that has overloaded operators for subtraction, multiplication, division and conjugation (using ") as well as methods that return the real and complex parts of a complex number and its modulus. [Note: A file complex.h is likely to exist already, so it is safe to avoid this name.]

3.24. Create a class with three overloaded methods for computing the sum of a one-dimensional array of numbers stored in a pointer format. The three methods should compute pointers to int, float and double.

3.25. Repeat Exercise 3.24 using a simple number in a template class.

3.26. Repeat Exercise 3.25 except a template function.

3.27. Write code for a struct X that has two integer elements a and b. One method for the struct should have the prototype

```
bool compare(const & X)
```

The method should compare two X objects and return the object that has a smaller value for a member. How could you accomplish the same goal using operator overloading?

3.28. What happens if you remove the & from the statement that defines y in Listing 3.8? Explain why this occurs.

3.29. Construct a program that will take two integers as input (in arbitrary order) and sum all the integers (inclusive) between the two. The program should terminate if it requires more than .01 second to compute the sum.

3.30. Create a template class version of Matrix that can, for example, deal with matrices of integer, float or double elements. Note that the template parameter must also be used when the return type is a Matrix object or a reference or pointer to a Matrix object. Thus, for example, the return type of the overloaded = operator will be Matrix<T>&.