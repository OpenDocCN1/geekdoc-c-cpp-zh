+   10. **(For thought)** Discuss whether the `isvalidInt()` function used in Program 14.19 should be modified to accept a string that ends in a decimal point. For example, should the input `12.` be accepted and converted to the integer number 12 or simply be rejected as noninteger input?

+   11. **(Useful utility)**
+      a. Write a C++ function named `isvalidReal()` that checks for a valid double-precision number. This kind of number can have an optional `+` or `-` sign, at most one decimal point (which can be the first character), and at least one digit between 0 and 9. The function should return the Boolean value `true` if the entered number is a real number; otherwise, it should return the Boolean value `false`.
+      b. Modify the `isvalidReal()` function written for Exercise 11a to remove all leading and trailing blank spaces from its string argument before determining whether the string corresponds to a valid real number.

+   12. **(Useful utility)** Write and test a C++ function named `getReal()` that uses exception handling to accept an input string continuously until a string that can be converted to a real number is entered. This function should return a double value corresponding to the string value the user enters.

# 14.6 Common Programming Errors

Here are the common errors associated with defining and processing strings:

+   1. Forgetting to include the string header file when using string class objects.
+   2. Forgetting that the newline character, `\n`, is a valid data input character.
+   3. Forgetting to convert a string class object by using `c_str()` when converting string class objects to numerical data types.
+   4. Not defining a catch block with the correct parameter data type for each thrown exception.
+   5. Attempting to declare an exception parameter in a catch block as a string class variable.

# 14.7 Chapter Summary

+   1. A string literal is any sequence of characters enclosed in quotation marks. It’s referred to as a string value, a string constant, and, more conventionally, a string.
+   
+   2. A string can be constructed as an object of the string class.
+   
+   3. The string class is commonly used for constructing strings for input and output purposes, as for prompts and displayed messages. Because of its capabilities, this class is used when strings need to be compared or searched or specific characters in a string need to be examined or extracted as a substring. It’s also used in more advanced situations when characters in a string need to be replaced, inserted, or deleted regularly.
+   
+   4. Strings can be manipulated by using the functions of the class they’re objects of or by using the general-purpose string and character methods.