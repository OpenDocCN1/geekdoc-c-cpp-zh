# Exercise 23.5-3 **Is the Number a Palindrome?**

> **Notice:** Please note the way cases 4, 6, and 9 are written. Since there isn’t any break statement in any of those cases, they all reach case 11.

A palindrome is a number that remains the same after reversing its digits. For example, the number 13631 is a palindrome. Write a PHP script that lets the user enter a five-digit integer and tests whether or not this number is a palindrome. Moreover, individual error messages should be displayed when the user enters any non-numeric characters or any integer with either less than or more than five digits.

(Note that this involves data validation.)

# Solution

To test if the user enters a palindrome number, you need to split its digits into five different variables as you learned in Chapter 13. Then, you can check whether the 1st digit is equal to the 5th digit and the 2nd digit is equal to the 4th digit. If this evaluates to true, the number is a palindrome.

To validate data input, you need to check whether the user has entered a five-digit number. Keep in mind that all five-digit numbers are in the range of 10000 to 99999. Therefore, you can just restrict the data input to within this range.

In order to display many different error messages, the best practice is to use a multiple-alternative decision structure which first checks data input validity for all cases, and then tries to solve the required problem. For example, if you need to check for various errors, you can do something like the following.

![](bbox=[0.012, 0.575, 0.983, 0.975])