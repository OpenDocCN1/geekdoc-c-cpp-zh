28. Relational operators, discussed in Chapter 4, can be applied to the string type.

29. In a string, the position of the first character is 0, the position of the second character is 1, and so on.

30. The length of a string is the number of characters in the string.

31. In C++, [] is called the array subscript operator.

32. To access an individual character within a string, use the array subscript operator together with the position of the character.

33. The string type contains functions such as at, append, clear, compare, erase, find, find_first_of, find_first_not_of, insert, length, replace, size, and swap to manipulate strings. These functions are described in Table 7-1.

# EXERCISES

+   1. Mark the following statements as true or false.

+   a. The following is a valid C++ enumeration type:
+   
+   ```cpp
+   enum romanNumerals {I, V, X, L, C, D, M};
+   ```

+   b. Given the declaration:
+   
+   ```cpp
+   enum cars {FORD, GM, TOYOTA, HONDA};
+   cars domesticCars = FORD;
+   ```
+   
+   the statement:
+   
+   ```cpp
+   domesticCars = domesticCars + 1;
+   ```
+   
+   sets the value of domesticCars to GM.

+   c. A function can return a value of an enumeration type.

+   d. You can input the value of an enumeration type directly from a standard input device.

+   e. The only arithmetic operations allowed on the enumeration type are increment and decrement.

+   f. The values in the domain of an enumeration type are called enumerators.

+   g. The following are legal C++ statements in the same block of a C++ program:
+   
+   ```cpp
+   enum mathStudent {BILL, JOHN, LISA, RON, CINDY, SHELLY};
+   enum historyStudent {AMANDA, BOB, JACK, TOM, SUSAN};
+   ```

+   h. The following statement creates an anonymous type:
+   
+   ```cpp
+   enum {A, B, C, D, F} studentGrade;
+   ```

+   i. You can use the namespace mechanism with header files with the extension h.