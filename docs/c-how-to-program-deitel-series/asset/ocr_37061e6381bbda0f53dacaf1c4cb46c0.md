**9.17**  *(Constructor Overloading)* Can a Time class definition that includes **both** of the following constructors:

```cpp
Time( int h = 0, int m = 0, int s = 0 );
Time();
```

be used to default construct a Time object? If not, explain why.

**9.18**  *(Constructors and Destructors)* What happens when a return type, even void, is specified for a constructor or destructor?

+   **9.19**  *(Date Class Modification)* Modify class Date in Fig. 9.17 to have the following capabilities:
+   
+    a) Output the date in multiple formats such as
+   
+   ```text
+   DDD YYYY
+   MM/DD/YY
+   June 14, 1992
+   ```
+   
+    b) Use overloaded constructors to create Date objects initialized with dates of the formats in part (a).
+   
+    c) Create a Date constructor that reads the system date using the standard library functions of the `<ctime>` header and sets the Date members. See your compiler's reference documentation or en.cppreference.com/w/cpp/chrono/c for information on the functions in header `<ctime>`. You might also want to check out C++11's new chrono library at en.cppreference.com/w/cpp/chrono.

In Chapter 10, we'll be able to create operators for testing the equality of two dates and for comparing dates to determine whether one date is prior to, or after, another.

**9.20**  *(SavingsAccount Class)* Create a SavingsAccount class. Use a static data member annual-InterestRate to store the annual interest rate for each of the savers. Each member of the class contains a private data member savingsBalance indicating the amount the saver currently has on deposit. Provide member function calculateMonthlyInterest that calculates the monthly interest by multiplying the savingsBalance by annualInterestRate divided by 12; this interest should be added to savingsBalance. Provide a static member function modifyInterestRate that sets the static annualInterestRate to a new value. Write a driver program to test class SavingsAccount. Instantiate two different objects of class SavingsAccount, a small and saver2, with balances of $2000.00 and $3000.00, respectively. Set the annualInterestRate to 3 percent. Then calculate the monthly interest and print the new balances for each of the savers. Then set the annualInterestRate to 4 percent, calculate the next month's interest and print the new balances for each of the savers.

+   **9.21**  *(IntegerSet Class)* Create class IntegerSet for which each object can hold integers in the range 0 through 100. Represent the set internally as a vector of bool values. Element `a[i]` is true if integer `i` is in the set. Element `a[j]` is false if integer `j` is not in the set. The default constructor initializes a set to the so-called “empty set,” i.e., a set for which all elements contain false.
+   
+    a) Provide member functions for the common set operations. For example, provide a `unionOfSets` member function that creates a third set that is the set-theoretic union of two existing sets (i.e., an element of the result is set to true if that element is true in either or both of the existing sets, and an element of the result is set to false if that element is false in each of the existing sets).
+   
+    b) Provide an `intersectionOfSets` member function which creates a third set which is the set-theoretic intersection of two existing sets (i.e., an element of the result is set to false if that element is false in either or both of the existing sets, and an element of the result is set to true if that element is true in each of the existing sets).
+   
+    c) Provide an `isEqual` member function that places a new integer `k` into a set by setting `a[k]` to true. Provide a `deleteElement` member function that deletes integer `m` by setting `a[m]` to false.

![](bbox=[0.03, 0.41, 0.085, 0.445])