# 2.3 Working with Strings and Characters

In this section, you will learn how to work with string type and character type data and variables. The C# type string represents a combination of zero or more characters. “John Adams” and “P410-2023-3180-05” are examples of string type data. Note that strings are enclosed in quotes.

# Value and Reference Types

The integer and real types we discussed in Chapter 1 are called value types because each variable of these types holds the actual value t in the memory location for that variable.

By contrast, strings (and other objects like arrays) are called reference types because each variable of these types holds only a reference to the data—that is, the memory location or address of the data, not the actual data. Reference type is discussed later in Chapter 7.

To understand working with strings, let’s look at an application that creates a user name by combining the following three pieces of string type data:

+   1. First 5 characters of the last name
+   2. First character of the first name
+   3. Last two digits of the id

Figure 2-4 shows the user interface form named UserNameString.

# Figure 2-4: UserNameString form

![](bbox=[0.095, 0.5, 0.425, 0.69])