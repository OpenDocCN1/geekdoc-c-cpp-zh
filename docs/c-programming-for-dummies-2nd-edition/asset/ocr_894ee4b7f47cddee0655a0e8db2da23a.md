+   - Creating structures
+   - Declaring structure variables
+   - Assigning values to a structure variable
+   - Building structure arrays
+   - Putting one structure inside another

# Chapter 14
Structures, the Multivariable

Individual variables are perfect for storing single values. When you need more of one type of a variable, you declare an array. For data that consists of several different types of variables, you mold the variable types into something called a structure. It's the C language's method of creating a variable buffet.



I prefer to think of the C language structure as a multivariable, or several variables rolled into one. You use structures to store and access complex information. That way, you can keep various int, char, float variables, and even arrays, all in one neat package.



Some things just belong together — like your name and address or your bank account number and all the money that's supposedly there. You can craft such a relationship in C by using parallel arrays or specifically named variables. But this