Listing 7.4 uses symbolic constants for the rates so that the constants are conveniently gathered in one place. If the power company changes its rates (it's possible), having the rates in one place makes them easy to update. The listing also expresses the rate breakpoints symbolically. They, too, are subject to change. BASE1 and BASE2 are expressed in terms of the rates and breakpoints. Then, if the rates or breakpoints change, the bases are updated automatically. You may recall that the preprocessor does not do calculations. Where BASE1 appears in the program, it will be replaced by 0.13230 * 360.0. Don't worry; the compiler does evaluate this expression to its numerical value (47.628) so that the final program code uses 47.628 rather than a calculation.

The flow of the program is straightforward. The program selects one of three formulas, depending on the value of kwh. You should pay particular attention to the fact that the only way the program can reach the first else is if kwh is equal to or greater than 360. Therefore, the else if (kwh <= BREAK2) line really is equivalent to demanding that kwh be between 360 and 482, as the program comment notes. Similarly, the final else can be reached only if kwh exceeds 720. Finally, note that BASE1, BASE2, and BASE3 represent the total charges for the first 360, 468, and 720 kilowatt-hours, respectively. Therefore, you need to add on only the additional charges for electricity in excess of those amounts.

Actually, the else if is a variation on what you already knew. For example, the core of the program is just another way of writing

```
if (kwh <= BREAK1)
    bill = RATE1 * kwh;
else
    if (kwh <= BREAK2)  // kwh between 360 and 468
        bill = BASE1 + (RATE2 * (kwh - BREAK1));
    else
        if (kwh <= BREAK3)  // kwh betweent 468 and 720
            bill = BASE2 + (RATE3 * (kwh - BREAK2));
        else                // kwh above 680
            bill = BASE3 + (RATE4 * (kwh - BREAK3));
```

That is, the program consists of an if else statement for which the statement part of the else is another if else statement. The second if else statement is said to be nested inside the first and the third inside the second. Recall that the entire if else structure counts as a single statement, which is why we didn't have to enclose the nested if else statements in braces. However, using braces would clarify the intent of this particular format.

These two forms are perfectly equivalent. The only differences are in where you put spaces and newlines, and these differences are ignored by the compiler. Nonetheless, the first form is better because it shows more clearly that you are making a four-way choice. This form makes it easier to skim the program and see what the choices are. Save the nested forms of indentation for when they are needed—for example, when you must test two separate quantities. An example of such a situation is having a 10% surcharge for kilowatt-hours in excess of 720 during the summer only.