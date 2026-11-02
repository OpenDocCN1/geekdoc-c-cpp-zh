# Figure 7-6 Change for $1.38

```
How many cents do you have? 138
From 138 cents you get
5 quarters
1 dimes
0 nickels
3 cents
```

You keep going like this until you've divided away all the nickels. At that point, the value of whatsLeft is just 3 (meaning 3 cents).

![](bbox=[0.13, 0.48, 0.22, 0.62])

The code in Listing 7-3 makes change in U.S. currency with the following coin denominations: 1 cent, 5 cents (one nickel), 10 cents (one dime), and 25 cents (one quarter). With these denominations, the MakeChange program gives you more than simply a set of coins adding up to 138 cents. The MakeChange class gives you the smallest number of coins that add up to 138 cents. With some minor tweaking, you can make the code work in any country's coinage. You can always get a set of coins adding up to a total. But, for the denominations of coins in some countries, you won't always get the smallest number of coins that add up to a total. In fact, I'm looking for examples. If your country's coinage prevents MakeChange from always giving the best answer, please, send me an e-mail (BeginProg@allmycode.com), tweet to @allmycode, or post on Facebook at /allmycode. Thanks.

![](bbox=[0.15, 0.7, 0.22, 0.84])

When two or more variables have similar types, you can create the variables with combined declarations. For example, Listing 7-3 has two combined declarations — one for the variables quarters, dimes, nickels, and cents (all of type int); another for the variables whatsLeft and total (both of type int). But to create variables of different types, you need separate declarations. For example, to create an int variable named total and a double variable named amount, you need one declaration int total; and another declaration double amount;

![](bbox=[0.15, 0.88, 0.22, 0.98])

Listing 7-3 has a call to System.out.println() with nothing in the parentheses. When the computer executes this statement, the cursor jumps to a new line on the screen. (I often use this statement to put a blank line in a program's output.)