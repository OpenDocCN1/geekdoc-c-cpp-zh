# PROGRAMMING PROJECTS

*Programming Projects require more problem-solving than Practice Programs and can usually be solved many different ways. Visit www.myprogramminglab.com to complete many of these Programming Projects online and get instant feedback.*

+   1. Write a program that converts from 24-hour notation to 12-hour notation. For example, it should convert 14:25 to 2:25 PM. The input is given as two integers. There should be at least three functions, one for input, one to do the conversion, and one for output. Record the AM/PM information as a value of type char, ‘A’ for AM and ‘P’ for PM. Thus, the function for doing the conversions will have a call-by-reference formal parameter of type char to record whether it is AM or PM. (The function will have other parameters as well.) Include a loop that lets the user repeat this computation for new input values again and again until the user says he or she wants to end the program.

+   2. Write a function that calculates a discount applicable on the price of an item. Your function should have three arguments: the price as a reference to a `double`, the discount as a `double` value, and a `bool` to indicate if the discount is calculated as a percentage or a fixed amount. You should calculate the discount and modify the price of the item accordingly.

+   3. Modify your program for Programming Project 2 so that it checks that the discount is not negative, and that the price of the item does not drop to zero after applying the discount. If it does violate these conditions, then your program should use an `assert` to exit the program.

+   4. Write a program that tells what coins to give out for any amount of change from 1 cent to 99 cents. For example, if the amount is 86 cents, the output would be something like the following:

```
86 cents can be given as
3 quarter(s) 1 dime(s) and 1 penny(pennies)
```

Use coin denominations of 25 cents (quarters), 10 cents (dimes), and 1 cent (pennies). Do not use nickel and half-dollar coins. Your program will use the following function (among others):

```
void computeCoins(int coinValue, int& num, int& amountLeft);
//Precondition: 0 < coinValue < 100; 0 <= amountLeft < 100.
//Postcondition: num has been set equal to the maximum number
//of coins of denomination coinValue cents that can be obtained
//from amountLeft. Additionally, amountLeft has been decreased
//by the value of the coins, that is, decreased by
//num * coinValue.
```