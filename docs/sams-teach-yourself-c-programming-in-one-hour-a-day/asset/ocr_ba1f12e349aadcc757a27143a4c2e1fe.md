# Exercises

Because many solutions are possible for the following exercises, answers are not provided.

+   1. Use your compiler to compile multiple source files into a single executable file.
(You can use Listings 22.1, 22.2, and 22.3 or your own listings.)
2. Write an error routine that receives an error number, line number, and module name. The routine should print a formatted error message and exit the program. (Pass the predefined macros for the line number and module name. The line number and module name from the location where the error occurs.) Here’s a possible example of a formatted error:
module.c (Line ##): Error number ##
3. Modify exercise 22 to make the error message more descriptive. Create a text file with your editor that contains an error number and message. Call this file ERROR.TXT. It could contain information such as the following:

```
1 Error number 1
2 Error number 2
90 Error opening file
100 Error reading file
```

Have your error routine search this file and display the appropriate error message based on a number passed to it.

+   4. Some header files might be included more than once when you write a modular program. Use preprocessor directives to write the skeleton of a header file that compiles only the first time it is encountered during compilation.
5. Write a program that takes two filenames as command-line parameters. The program should copy the first file into the second file. (See Lesson 17, “Using Disk Files,” if you need help working with files.)
6. This is the last exercise of the book and its content is up to you. Select a programming task of interest to also meets a real need you have. For example, you could write programs to catalog your MP3 collection, keep track of your checkbox, or calculate financial figures related to a planned house purchase. There’s no substitute for tackling a real-world programming problem to sharpen your programming skills and help you remember all the things you learned in this book.