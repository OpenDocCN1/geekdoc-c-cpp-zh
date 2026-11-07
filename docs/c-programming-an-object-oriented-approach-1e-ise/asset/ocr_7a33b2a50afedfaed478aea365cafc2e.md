**PRG-8.** Design a *Big_Integer* class that handles integers of arbitrary sizes given as a string of digits such as "345672134579098765". Use the following guide lines:

+   a. Use the *popBack* and *pushFront* functions we defined for strings in Chapter 10 to extract the rightmost digit of a big integer or to insert a digit at the left of an integer.
+   b. Overload the << operator to print a big integer.
+   c. Overload the + operator to add two big integers. Note that when we add two digits in mathematics, we may have a *carry* (digit 1). For example, adding integers 7 and 8 results in 5 with a *carry* to be added to the next column.
+   d. Overload the − operator to subtract one integer from another. Note that when we subtract one digit from another one, we may have a *borrow* (digit 1). For example, subtracting integers 7 from 5 results in 8 with a borrow to be used in the next column. Note that if the first integer is smaller than the second, the result of subtraction must be complemented to give a negative integer.
+   e. It is easier to add leading zeros to integers to make their size the same in adding and subtracting and to remove leading zeros when printing the result.