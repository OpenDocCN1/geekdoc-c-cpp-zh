# Character Strings and String Functions

You will learn about the following in this chapter:

+   - Functions:
+     `gets(), gets_s(), fgets(), puts(), fputs(), strcat(), strncat(), strcmp(), strncmp(), strcpy(), strncpy(), sprintf(), strchr()`
+   - Creating and using strings
+   - Using several string and character functions from the C library and creating your own string functions
+   - Using command-line arguments

The character string is one of the most useful and important data types in C. You have been using character strings all along, but there still is much to learn about them. The C library provides a wide range of functions for reading and writing strings, copying strings, comparing strings, combining strings, searching strings, and more. This chapter will add these capabilities to your programming skills.

# Representing Strings and String I/O

Of course, you already know the most basic fact: A character string is a char array terminated with a null character (\0). Therefore, what you’ve learned about arrays and pointers carries over to character strings. But because character strings are so commonly used, C provides many functions specifically designed to work with strings. This chapter discusses the nature of strings, how to declare and initialize strings, how to get them into and out of programs, and how to manipulate strings.

Let’s look at a short program (see Listing 11.1) that illustrates some of the ways to represent strings in a program.