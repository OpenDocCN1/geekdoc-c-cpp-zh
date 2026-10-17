
input and display an error message when the user enters any non-numeric or negative values. Additionally, the user has a maximum number of two retries. If the user enters more than three non-numeric or negative values, a message “Dude, you are dumb!” should be displayed and the script execution should end.

+   11. The area of a circle can be calculated using the following formula:

      Area = π · Radius²

      Write a PHP script that prompts the user to enter the length of the radius of a circle and then calculates and displays its area. The script should iterate as many times as the user wishes. At the end of each area calculation, the script should ask the user if he or she wishes to calculate the area of another circle. If the answer is “yes” the script should repeat; it should end otherwise. Make your script accept the answer in all possible forms such as “yes”, “YES”, “Yes”, or even “YeS”.

      Moreover, the script should validate data input and display an error message when the user enters any non-numeric or non-positive value for Radius.

      Hint: Use the `pi()` function to get the value of π.

+   12. Write a PHP script that displays all possible integer values of x and y within the range -100 to +100 that validate (when possible) the following formula:

      5x + 3y² = 0

+   13. Write a PHP script that displays all possible integer values of x, y, and z within the range -10 to +10 that validate the following formula:

      (x + y) / 2 + (3z²) / (x + 3y + 45) = x / 3

+   14. Write a PHP script that lets the user enter three positive integers and then finds their product using the Russian multiplication algorithm.

+   15. Write a PHP script that prompts the user to enter two positive integers and then displays all prime integers between them. Moreover, the script should validate data input and display an error message when the user enters a value less than +2.

      Hint: To make your PHP script operate correctly, independent of which integer given is the lowest, you can swap their values (if necessary) so that they are always in the proper order.

+   16. Write a PHP script that prompts the user to enter two positive four-digit integers and then displays all integers between them that are palindromes. Moreover, the script should validate data input and display an error message when the user enters any non-numeric characters, or any numbers other than four-digit ones.

      Hint: To make your PHP script operate correctly, independent of which integer given is the lowest, you can swap their values (if necessary) so that they are always in the proper order.

## More Exercises with Loop Control Structures

+   17. Write a PHP script that displays all possible RAM sizes between 1 byte and 1GByte, such as 1, 2, 4, 8, 16, 32, 64, 128, and so on.

      Hint: 1GByte equals 2³⁰ bytes, or 1073741824 bytes

+   18. Write a PHP script that displays the following sequence of numbers:

      1, 11, 23, 37, 53, 71, 91, 113, 137, ... 401

+   19. Write a PHP script that displays the following sequence of numbers:

      -1, 1, -2, 2, -3, 3, -4, 4, ... -100, 100

+   20. Write a PHP script that displays the following sequence of numbers:

      1, 11, 111, 1111, 11111, ... 11111111

+   21. The Fibonacci⁴ sequence is a series of numbers in the following sequence:

      1, 1, 2, 3, 5, 8, 13, 21, 34, 55, ...

      By definition, the first two numbers are 1 and 1 and each subsequent number is the sum of the previous two.

      Write a PHP script that lets the user enter a positive integer and then displays as many Fibonacci numbers as that given integer.

+   22. Write a PHP script that lets the user enter a positive integer and then displays all Fibonacci numbers that are less than that given integer.

+   23. Write a PHP script that prompts the user to enter a positive integer N and then finds and displays the value of y in the following formula:

      y = (2 + 4 + 6 + ⋯ + 2N) / (1 · 2 · 3 · 4 ⋯ N)

      Moreover, the script should validate data input and display an error message when the user enters any non-numeric value or a value less than 1.

+   24. Write a PHP script that prompts the user to enter an integer N and then finds and displays the value of y in the following formula

      y = (1 - 3 + 5 - 7 + ⋯ + (2N + 1)) / N

      Moreover, the script should validate data input and display an error message when the user enters any non-numeric value or a value less than 1.

> ⁴ Leonardo Pisano Bigollo (c. 1170–c. 1250), also known as Fibonacci, was an Italian mathematician. In his book *Liber Abaci* (published in 1202), Fibonacci used a special sequence of numbers to try to determine the growth of a rabbit population. Today, that sequence of numbers is known as the Fibonacci sequence. He was also one of the first people to introduce the Arabic numeral system to Europe; this is the numeral system we use today, based on ten digits with a decimal point and a symbol for zero. Before then, the Roman numeral system was being used, making numerical calculations difficult.

# Chapter 31 More Exercises with Loop Control Structures

+   25. Write a PHP script that prompts the user to enter an integer N and then finds and displays the value of y in the following formula:

      y = 1 − 1/2 + 1/3 − 1/5 + ⋯ + 1/N

      Moreover, the script should validate data input and display an error message when the user enters any non-numeric value or a value less than 1.

+   26. Write a PHP script that prompts the user to enter an integer N and then finds and displays the value of y in the following formula:

      y = 1/1^N + 1/2^(N−1) + 1/3^(N−2) + ⋯ + 1/N^1

      Moreover, the script should validate data input and display an error message when the user enters any non-numeric value or a value less than 1.

+   27. In mathematics, the factorial of a non-negative integer N is the product of all positive integers less than or equal to N, and it is denoted by N!. The factorial of 0 is, by definition, equal to 1. In mathematics, you can write

      N! = { 1 · 2 · 3 · … · N, for N > 0
           { 1,           for N = 0

      For example, the factorial of 5 is 5! = 1 × 2 × 3 × 4 × 5 = 120.

      Write a PHP script that prompts the user to enter a non-negative integer N and then calculates its factorial.

+   28. Write a PHP script that lets the user enter a value for x and then calculates and displays the exponential function e^x using the Taylor series, shown next, with an accuracy of 0.00001.

      e^x = 1 + x^1/1! + x^2/2! + x^3/3! + ⋯

      Hint: Keep in mind that x^0/0! = 1.

+   29. Write a PHP script that lets the user enter a value for x and then calculates and displays the sine of x using the Taylor series, shown next, with an accuracy of 0.00001.

      sin x = x − x^3/3! + x^5/5! − x^7/7! + ⋯

      Hint: Keep in mind that x is in radians and x^1/1! = x.

> Brook Taylor (1685–1731) was an English mathematician who is best known for the Taylor series and his contributions to the theory of finite differences.

# Chapter 31
More Exercises with Loop Control Structures

+   30. Write a PHP script that lets the user enter a value for x and then calculates and displays the cosine of x using the Taylor series, shown next, with an accuracy of 0.00001.

      $$\cos x = 1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \frac{x^6}{6!} + \cdots$$

      Hint: Keep in mind that x is in radians and $\frac{x^0}{0!}=1$.

+   31. Write a PHP script that prompts the user to enter the daily temperatures in August and then calculates and displays the average as well as the highest temperature.

      Moreover, since −459.67° (on the Fahrenheit scale) is the lowest temperature possible (it is called absolute zero), the script should validate data input and display individual error messages when the user enters a non-numeric or a value lower than absolute zero.

+   32. A scientist needs a software application to record the level of the sea based on values recorded at specific times (HH:MM), in order to extract some useful information. Write a PHP script that lets the scientist enter the level of the sea, the hour, and the minutes, repeatedly until the value of 9999 (used as a sea level) is entered. Then, the script should display the highest and the lowest sea levels as well as the hour and the minutes at which these levels were recorded.

+   33. Suppose that the letter A corresponds to the number 1, the letter B corresponds to the number 2, and so on. Write a PHP script that prompts the user to enter two integers and then displays all alphabet letters that exist between them. For example, if the user enters 3 and 6, the script should display C, D, E, F. Moreover, the script should validate data input and display individual error messages when the user enters any non-numeric, negative, or any value greater than 26.

      Hint: To make your PHP script operate correctly, independent of which integer given is the lowest, you can swap their values (if necessary) so that they are always in the proper order.

+   34. Write a PHP script that assigns a random secret integer between 1 and 100 to a variable and then prompts the user to guess the number. If the integer given is less than the secret one, a message “Your guess is smaller than my secret number. Try again.” should be displayed. If the integer given is greater than the secret one, a message “Your guess is bigger than my secret number. Try again.” should be displayed. This process should repeat until the user finally finds the secret number. Then, a message “You found it!” should be displayed, as well as the total number of the user’s attempts.

+   35. Expand the previous exercise/game by making it operate for two players. The player that wins is the one that finds the random secret number in fewer attempts.

+   36. The size of a TV screen always refers to its diagonal measurement. For example, a 40-inch TV screen is 40 inches diagonally, from one corner on top
