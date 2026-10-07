# Chapter 11: Working with Numeric Functions 163

# 11.3 Functions That Work with Missing Values

In SAS, you can refer to a missing numeric value with a period and a missing character value by a single blank (inside single or double quotes). For example, take a look at the short program here that tests to see if several variables contain a missing value:

# Program 11.2: Testing for Missing Numeric and Character Values (without the MISSING Function)

Instead of using values for a missing numeric and character value, you can use the MISSING function instead. This function returns a value of true if its argument is a missing value and false otherwise. The amazing thing about this is that the argument can be either character or numeric—a real rarity among SAS functions. You can rewrite Program 11.2 using the MISSING function like this:

# Program 11.3: Demonstrating the MISSING Function

This makes programs easier to read, the MISSING function also returns a value of true for the alternate numeric values (.A, .B..., .Z, and _). These alternative numeric missing values can be useful when you have different categories of missing information.

For example, you could assign .A to did not answer and .B to Not applicable. SAS treats all of these values as missing for numeric calculations but allows you to distinguish among them.

# 11.4 Setting Character and Numeric Values to Missing

The CALL routine MISSING is a handy way to set one or more character and/or numeric variables to missing. When you use a variable list such as XI–10 or Char1–Char5, you need to precede the list with the keyword OF. Here are some examples: