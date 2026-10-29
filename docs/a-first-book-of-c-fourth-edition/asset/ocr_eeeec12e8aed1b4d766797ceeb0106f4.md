+   2. **(Practice)** Define a union variable named `car` containing an integer named `year`, an array of 10 characters named `name`, and an array of 10 characters named `model`.
+   
+   3. **(Practice)** Define a union variable named `factors` that allows referencing a double-precision number by the variable names `watts` and `power`.
+   
+   4. **(Practice)** Define a union data type named `Amt` containing an integer variable named `intAmt`, a double-precision variable named `dblAmt`, and a pointer to a character variable named `ptKey`.
+   
+   5. **(Desk check)** a. What do you think the following section of code will display?
+   
+   ```cpp
+   union
+   {
+       char ch;
+       double btype;
+   } alt;
+   alt.ch = 'y';
+   cout << alt.btype;
+   ```
+   
+   b. Include the code in Exercise 5a in a program, and run the program to verify your answer to Exercise 5a.

# 16.6 Common Programming Errors

Three common errors are often made when using structures or unions:

+   1. Structures and unions, as complete entities, can't be used in relational expressions. For example, even if `TeleType` and `PhoneType` are two structures of the same type, the expression `TeleType == PhoneType` is invalid. Members of a structure or union can, of course, be compared if they're of the same data type, using any of C++'s relational operators.
+   
+   2. When a pointer is used to “point to” a structure or a union or is a member of a structure or a union, take care to use the address in the pointer to access the correct data type. If you're confused about exactly what's being pointed to, remember: “If in doubt, print it out.”
+   
+   3. Because a union can store only one of its members at a time, you must be careful to keep track of the currently stored variable. Storing one data type in a union and accessing it by the wrong variable name can result in an error that's particularly troublesome to locate.