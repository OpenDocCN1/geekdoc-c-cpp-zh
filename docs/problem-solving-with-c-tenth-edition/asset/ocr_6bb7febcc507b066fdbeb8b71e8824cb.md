2. Powers of numbers can be calculated by multiplying the number by itself for as many times as the value of the exponent. For example, 2 raised to the power 4 can be calculated by multiplying 2 by itself 4 times to get 16. Write a program that:

+   1. inputs a double as the base number and an int as the exponent;
+   2. multiplies the base number by itself using a loop that repeats for the number of times in the int;
+   3. outputs the exponential value calculated.

Use an if statement for the special case where the output is 1 if the int value is 0. For a more challenging version, deal with the case where the exponent is negative.

3. Many treadmills output the speed of the treadmill in miles per hour (mph) on the console, but most runners think of speed in terms of a pace. A common pace is the number of minutes and seconds per mile instead of mph.

Write a program that starts with a quantity in mph and converts the quantity into minutes and seconds per mile. As an example, the proper output for an input of 6.5 mph should be 9 minutes and 13.8 seconds per mile. If you need to convert a double to an int, which will discard any value after the decimal point, then you may use

```
intValue = static_cast<int>(db1Val);
```

4. Write a very simple conversational dialog program. Your program should do the following:

+   Say "Hello" to the user.
+   Ask them if they are having a good day, and record their input.
+   If their response is anything other than a 'y' for yes or an 'n' for no, repeat the question.
+   If they respond with a 'y', output "I'm glad to hear that", and if they answer with an 'n', then output "I hope your day gets better soon."

You may need to use a do-while loop to repeat the questions to the user.

![](bbox=[0.07, 0.38, 0.14, 0.52])