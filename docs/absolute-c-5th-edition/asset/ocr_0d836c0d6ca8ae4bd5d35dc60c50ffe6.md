# CHAPTER 8 Operator Overloading, and References

5. Write the definition for a class Vector2D that stores information about a two-dimensional vector. The class should have functions to get and set the x and y components, where x and y are integers.

Next, overload the * operator so it returns the dot product of two vectors. The dot product of two-dimensional vectors A and B is equal to

```
(A \cdot B) + (A \times B)
```

Finally, write a main subroutine that tests the * operation.

6. Define a class Integer that stores an integer and has functions to get and set the integer's value. Then, overload the [] operator so it returns the digit in position i, where i = 0 is the least-significant digit. If no such digit exists then -1 should be returned.

For example, if x is of type Integer and set to 418, x[0] should return 8, x[1] should return 1, x[2] should return 4, and x[3] should return -1.

7. Define a class PrimeNumber that stores a prime number. The default constructor should set the prime number to 1. Add another constructor that allows the caller to set the prime number. Also add a function to get the prime number. Finally, overload the prefix ++ and -- operators so they return a PrimeNumber object that is the next prime number (for ++) and the next smallest prime number (for --). For example, if the object's prime is set to 13, invoking ++ should return a PrimeNumber object whose prime number is set to 17. Create an appropriate test program for the class.

8. Do Programming Project 6.10, the definition of a Temperature class, except overload ==, << and >> as member operators. The == operator should return true if the two temperature values are identical, and << should output the temperature in Fahrenheit and >> should output the temperature in Fahrenheit. Create appropriate tests for the overloaded operators.

9. Programming Project 6.12 asked you to write a BoxOfProduce class that stores three bundles of fruits or vegetables (in an array of strings of size 3) to ship to a customer. Rewrite this to use a vector instead of an array and add appropriate constructors, mutators, and accessors. The class should have a function to add additional fruits or vegetables to the box so there could be more than three bundles in one box. Overload the + operator to return a new BoxOfProduce object that combines the vector contents of both operand BoxOfProduce objects. Test your functions and + operator from the main function. You do not have to implement the rest of Programming Project 6.12, only the changes to the BoxOfProduce class.

![](bbox=[0.06, 0.368, 0.155, 0.453])