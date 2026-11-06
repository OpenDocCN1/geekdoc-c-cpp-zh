**P4.4** Complete the program in How To 4.1 on page 162. Your program should read twelve temperature values and print the month with the highest temperature.

**P4.5** *Credit Card Number Check.* The last digit of a credit card number is the check digit, which protects against transcription errors such as an error in a single digit or switching two digits. The following method is used to verify actual credit card numbers but, for simplicity, we will describe it for numbers with 8 digits instead of 16:

+   - Starting from the rightmost digit, form the sum of every other digit. For example, if the credit card number is 43589795, then you form the sum 5 + 7 + 8 + 3 = 23.
+   - Double each of the digits that were not included in the preceding step. Add all digits of the resulting numbers. For example, with the number given above, doubling the digits, starting with the next-to-last one, yields 18 10 18 10 8. Adding all digits in these values yields 1 + 8 + 1 + 8 + 1 + 0 + 8 = 27.
+   - Add the sums of the two preceding steps. If the last digit of the result is 0, the number is valid. In our case, 23 + 27 = 50, so the number is valid.

Write a program that implements this algorithm. The user should supply an 8-digit number, and you should print out whether the number is valid or not. If it is not valid, you should print out the value of the check digit that would make the number valid.

**P4.6** *Currency conversion.* Write a program that first asks the user to type today’s exchange rate between U.S. dollars and Japanese yen, then reads U.S. dollar values and converts each to yen. Use 0 as a sentinel.

![](bbox=[0.463, 0.517, 0.759, 0.671])

**P4.7** Write a program that first asks the user to type in today’s exchange rate between U.S. dollars and Japanese yen, then reads U.S. dollar values and converts each to Japanese yen. Use 0 as the sentinel value to denote the end of dollar inputs. Then the program reads a sequence of yen amounts and converts them to dollars. The second sequence is terminated by another zero value.

**P4.8** Write a program that reads a set of floating-point values. Ask the user to enter the values, then print

+   - the average of the values.
+   - the smallest of the values.
+   - the largest of the values.
+   - the range, that is the difference between the smallest and largest.

Of course, you may only prompt for the values once.