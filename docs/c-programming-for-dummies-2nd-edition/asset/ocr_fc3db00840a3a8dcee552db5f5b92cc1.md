# IN THIS CHAPTER

+   » Changing variable types
+   » Using typedef to create new variables
+   » Making static variables
+   » Creating a global variable
+   » Working with structures and functions
+   » Exploring enumerated constants

# Chapter 16

# Variable Nonsense

You have more to learn about C language variables than knowing the keywords int, char, float, and double. Yes, I'm including signed, unsigned, long, and anything else you may already know in that list. The reason is that the variable is a big part of C. Choosing the right data type and using it properly can make or break a program.

# Variable Control

That which is called a variable by any other name would still be a variable. That is, unless you mess with the variable's data type in your code by changing it into another type, giving it a new name altogether, or casting a spell upon the variable to meet your needs, benevolent or not.

# Typecasting into disbelief

When is a float variable not a float? When it's typecast into an int, of course. This trick is made possible in C by using the typecast. For example:

```
(int)debt
```