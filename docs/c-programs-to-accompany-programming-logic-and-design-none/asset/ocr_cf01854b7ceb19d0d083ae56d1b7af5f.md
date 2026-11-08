# ## LAB 7-1: WRITING SIMPLE FUNCTIONS

In this lab, you complete a partially prewritten C++ program that includes simple functions. The program prompts the user for his or her age. If the user is 21 or older, the program should call a function named allowEntry that displays the message “You are old enough to enter this establishment.” If the user is younger than 21, the program should call a function named doNotAllowEntry that displays the message “Sorry, you'll have to wait until you are 21.” The source code file provided for this lab includes the necessary variable declarations and the input statement. Comments are included in the file to help you write the remainder of the program.

+   1. Open the source code file named `AllowEntry.cpp` using Notepad or the text editor of your choice.
+   2. Write the C++ statements as indicated by the comments.
+   3. Save this source code file in a directory of your choice and then make that directory your working directory.
+   4. Compile the source code file, `AllowEntry.cpp`.
+   5. Execute the program.

# ## WRITING FUNCTIONS THAT REQUIRE A SINGLE PARAMETER

As you learned in *Programming Logic and Design, Fifth Edition*, some functions require data to accomplish their task. You also learned that designing a program so that it sends data (which can be different each time the program runs) to a function (which doesn't change) keeps you from having to write multiple functions to handle similar situations. For example, suppose you are writing a program that has to determine if a number is even or odd. It is certainly better to write a single function, to which the program can pass a number entered by the user, than to write individual functions for every number.

In Figure 7-2, you see the C++ code for a program that includes a function that can determine if a number is odd or even. The line numbers are not actually part of the program but are included for reference only. The program allows the user to enter a number, and then passes that number to a function as an argument. After it receives the argument, the function can determine if the number is an even number or an odd number.