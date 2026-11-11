+   - Do not use keywords or any system library names for identifiers. LO 1.1
+   - Use meaningful and intelligent variable names. LO 1.2
+   - Do not create variable names that differ only by one or two letters. LO 1.2
+   - Integer constants, by default, assume **int** types. To make the numbers **long** or **unsigned**, we must append the letters L and U to them. LO 1.2
+   - Floating point constants default to **double**. To make them to denote **float** or **long double**, we must append the letters F or L to the numbers. LO 1.2
+   - Use single quote for character constants and double quotes for string constants. LO 1.2
+   - A character is stored as an integer. It is therefore possible to perform arithmetic operations on characters. LO 1.2
+   - Do not use lowercase l for long as it is usually confused with the number 1. LO 1.3
+   - C does not provide any warning or indication of overflow. It simply gives incorrect results. Care should be exercised in defining correct data type. LO 1.3
+   - Each variable used must be declared for its type at the beginning of the program or function. LO 1.4
+   - All variables must be initialized before they are used in the program. LO 1.4
+   - Do not combine declarations with executable statements. LO 1.4
+   - Do not use semicolon at the end of **#define** directive. LO 1.4
+   - The character # should be in the first column. LO 1.4
+   - Do not give any space between # and **define**. LO 1.4
+   - A variable defined before the main function is available to all the functions in the program. LO 1.4
+   - A variable defined inside a function is local to that function and not available to other functions. LO 1.4
+   - A variable can be made constant either by using the preprocessor command **#define** at the beginning of the program or by declaring it with the qualifier **const** at the time of initialization. LO 1.5

# ## KEY TERMS TO REMEMBER

+   - **Identifiers:** Refer to the names of variables, functions and arrays. LO 1.1
+   - **Constants:** Refer to fixed values that do not change during the execution of a program. LO 1.2
+   - **String constant:** Is a sequence of characters enclosed in double quotes where characters could be letters, numbers, special characters or blank space. LO 1.2
+   - **Variable:** Is a data name that may be used to store a data value. LO 1.2
+   - **Storage class:** Provides information related to the location and visibility of a variable. LO 1.4
+   - **scanf:** Is a predefined standard C function that reads formatted input from stdin (standard input) stream. LO 1.4