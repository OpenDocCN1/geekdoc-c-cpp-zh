# Section 8.3

+   1. Write a switch statement that increases balance by adding amount to it if the value of the character variable transCode is 'D'; decreases balance by subtracting amount from it if transCode is 'W'; displays the value of balance if transCode is 'P'; and displays an illegal-transaction message otherwise.

+   2. Write a switch statement that, for two given integers a and b, and a given character operation, computes and displays a + b, a - b, a * b, or a / b according to whether the operation is '+', '-', '*' , or '/' , and displays an illegal-operator message if it is not one of these.

For Exercises 3–6, write functions that use switch statements to compute what is required. To test these functions, you should write driver programs as instructed in Programming Problems 1–4 for Section 8.3 at the end of this chapter.

+   3. Given a distance less than 1000, return a shipping cost as determined by the following table:

| Distance | Cost |
|---|---|
| 0 through 99 | $5.00 |
| At least 100 but less than 300 | $8.00 |
| At least 300 but less than 600 | $10.00 |
| At least 600 but less than 1000 | $12.00 |

+   4. Given a number representing a TV channel, return the call letters of the station that corresponds to that number, or some message indicating that the channel is not used. Use the following channel numbers and call letters (or use those that are available in your locale):
+   2: WCBS
+   4: WNBC
+   5: WNEW
+   7: WABC
+   9: WOR
+   11: WPIX
+   13: WNET

+   5. Given the number of a month, return the name of the month (or an error message indicating an illegal month number).

+   6. Proceed as in Exercise 5, but return the number of days in the month. (A leap year is a multiple of 4; but if it is a multiple of 100, it must also be a multiple of 400.)