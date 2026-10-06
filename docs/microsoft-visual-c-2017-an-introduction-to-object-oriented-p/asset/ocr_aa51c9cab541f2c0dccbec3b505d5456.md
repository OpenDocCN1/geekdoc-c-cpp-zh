# CHAPTER 11 Exception Handling

enters a 0 for the value of gallonsOfGas, the program saves time and computer memory. (Programmers say this program has "overhead.\ On the other hand, if you think dividing zero is infrequent—that is, the exception to the rule—then the decision will execute many times than it is needed. In other words, if a user enters 0 for gallonsOfGas in only one case out of 1000, then the if statement is executed unnecessarily 999 times. In that case, it is more efficient to eliminate the if test and instantiate an Exception when needed.

492

The creators of C define "inrequent" as an event that happens less than 30 percent of the time. That is, if you think an error will occur in less than 30 percent of all program executions, create an exception; if you think the error will occur more often, use traditional error checking. Of course, your boss or instructor might prefer a different percentage to use as a guideline.

Another advantage to using exception handling instead of decision making to control errors is when a program's main logic is interrupted by a series of if statements and decisions that might detect errors, the program can become more complicated and difficult to understand. The object-oriented approach to error handling separates a program's main tasks from code that deals with rare exceptions.

Programmers use the phrase sunny day to describe a scenario in everything goes well and no errors occur.

# Understanding Object-Oriented Exception-Handling Methods

Object-oriented exception handling uses three unique terms: try, throw, and catch.

+   - You "try" a procedure that may not complete correctly.
- A method that detects an error condition "throws" an exception.
- The block of code that processes the error "catches" the exception.

When you write a block of code in which something can go wrong, you can place the code in a try block, which consists of the following elements:

+   - The keyword try
- A pair of braces containing statements that might cause exceptions

You must at least one catch block or finally block immediately following a try block. (You will learn about finally blocks later in this chapter.) Each catch block can "catch" one type of exception—that is, an Exception object or an object of its child classes. Programmers sometimes refer to a catch block as a catch clause. You can create a catch block by typing the following elements:

+   - The keyword catch
- Parentheses containing an Exception type and, optionally, name an instance of the Exception type
- A pair of braces containing statements that deal with the error condition

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN-02-200-22