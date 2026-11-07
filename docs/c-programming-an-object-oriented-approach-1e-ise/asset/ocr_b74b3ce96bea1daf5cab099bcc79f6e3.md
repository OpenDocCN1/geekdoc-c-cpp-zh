PRG-3. Redesign the Complex class (see PRG-2), but overload only the operators +, -, *, /, and << for the class.

PRG-4. Declare and define a class Set representing a set of integers. A set is a collection of data without repetition or ordering. The class should have only private data members: a pointer to a dynamically allocated array of integers and an integer that holds the size of the set. The following shows the operators to be defined for a set.

![](bbox=[0.33, 0.225, 0.81, 0.37])

Your solution must include an interface file, an implementation file, and an application file. It should have the following methods:

+   a. A constructor to create an empty set.
+   b. A destructor.
+   c. A function to add an element to the set (overload the += operator).
+   d. A function to remove an element from the set (overload the -= operator).
+   e. A binary friend function to get the intersection of two sets (overload the * operator).
+   f. A binary friend function to get the union of two sets (overload the + operator).
+   g. A binary friend function to determine the difference of two sets (overload the - operator).
+   h. A function to print the contents of a set.

PRG-5. Create a class Money that represents a money value (combination of dollars and cents). Overload the binary plus operator to add two money values to get a new one. Overload the binary minus operator to subtract a money value from a larger value to get a new one. Also overload the *= operator to multiply a money value by an integer and /= operator to divide a money value by an integer.

PRG-6. Redesign the Money class by overloading only the relational operators (<, >, ==, and !=) to compare the two Money objects.

PRG-7. In Chapter 9 we designed a class Pascal to define the value of all terms for a given n. Another approach is to overload the function call operator to find the coefficient of any term. For example, the coefficient of x^3 y^2 can be found using the call to operator() (5, 3). Use the fact that the coefficient of a term can be found as shown below:

```
```
coefficient of x^i y^j = factorial (i + j) / (factorial (i) * factorial (j))
```
```