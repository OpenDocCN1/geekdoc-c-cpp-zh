# If thine int offends thee, cast it out

The run in Figure 7-6 seems artificial. Why would you start with 138 cents? Why not use the more familiar $1.38? The reason is that the number 1.38 isn't a whole number, and whole numbers are more accurate than other kinds of numbers. In fact, without whole numbers, the remainder operator isn't very useful.

For example, the value of 1.38 % 0.25 is 0.129999999999999. All those nines are tough to work with. Imagine reading your credit card statement and seeing that you owe $0.129999999999999. You'd probably pay $0.13 and let the credit card company keep the change. But after years of rounding numbers, the credit card company would make a fortune! Chapter 8 describes inaccuracies caused by using double values in a bit more detail.

Throughout this book, I illustrate Java's double type with programs about money. Many authors do the same thing. But for greater accuracy, avoid using double values for money. Instead, you should use int values or use the long values that I describe in the last section of this chapter. Even better, look up BigInteger and BigDecimal in Java's API documentation.

These BigSomethingOrOther types are cumbersome to use, but they provide industrial-strength numeric range and accuracy.

Now what if you want to input 1.38, and then have the program take your 1.38 and turn it into 138 cents? How can you get your program to do this?

My first idea is to multiply 1.38 by 100:

```
//This doesn't quite work.
double amount;
int total;
amount=keyboard.nextDouble();
total=amount*100;
```

In everyday arithmetic, multiplying by 100 does the trick. But computers are fussy. With a computer, you have to be very careful when you mix int values and double values. (See the first figure in this sidebar.)

![](bbox=[0.52, 0.6, 0.78, 0.7])

![](bbox=[0.25, 0.7, 0.78, 0.9])