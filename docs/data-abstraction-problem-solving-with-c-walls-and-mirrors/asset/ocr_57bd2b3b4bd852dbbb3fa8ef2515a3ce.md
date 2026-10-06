# CHAPTER 1 Data Abstraction: The Walls

7. The intersection of two bags is a new bag containing the entries that occur in both of the original two bags. Design and specify a method intersection for the ADT bag that returns a new bag intersection of the bag receiving the call to the bag that is the method's one argument. Include sufficient comments to fully specify the method.

Note that the intersection of two bags might contain duplicate items. For example, if x occurs five times in one bag and twice in another, the intersection of these bags contains x times. Suppose, if bag1 and bag2 contain strings a, b, and c; and bag2 contains the strings b, d, and e. The expression bag1.intersection(bag2) returns a bag containing only the string b. Note that intersection does not affect the contents of bag1 and bag2.

8. The difference of two bags is a new bag containing the entries that would be left in one after removing those that also occur in the second. Design and specify a method difference for the ADT bag that returns a new bag the difference of the bag receiving the call to the bag that is the method's one argument. Include sufficient comments to fully specify the method.

Note that the difference of two bags might contain duplicate items. For example, if x occurs five times in one bag and twice in another, the difference of these bags contains three times. Suppose, if bag1 and bag2 contain strings a, b, and c; and bag2 contains the strings b, d, and e. The expression bag1.difference(bag2) returns a bag containing only the strings a and c. Note that difference does not affect the contents of bag1 and bag2.

9. Consider the ADT polynomial in x—which operations include the following:

```
degree() // Returns the degree of a polynomial.
coefficient(power) // Returns the coefficient of the x^power term.
changeCoefficient(newCoefficient, power) // Replaces the coefficient of
// the x^power term with newCoefficient.
```

For this problem, only polynomials whose exponents are nonnegative integers. For example, p = 4x^5 + 7x^3 - x^2 + 9

The following examples demonstrate the ADT operations on this polynomial.

+   - .degree() is 5 (the highest power of x with a nonzero coefficient)
- .coefficient(3) is 7 (the coefficient of the x^3)
- .coefficient(4) is 0 (the coefficient of a missing term is implicitly 0)
- .changeCoefficient(-3, 7) changes the polynomial p to -3x^4 + 7x^3 - x^2 + 9

Using these ADT operations, write statements to perform the following tasks:

+   a. Display the coefficient of the term that has the highest power.
b. Increase the coefficient of the x^3 term by 8.
c. Compute the sum of two polynomials.

# PROGRAMMING PROBLEMS

+   1. Add a transaction to the banking example in Figure C-4 of Appendix C. This class keeps track of the date, amount, and type of transaction (checking or savings).

+   2. Consider a program that will read employee data, sort the data by employee number, write out the sorted data, and compute various statistics about the data, such as the average age of an employee. Design a solution to this problem using UML notation. What classes and methods did you identify during the design of your solution? Write complete specifications, including preconditions and postconditions, for each module.