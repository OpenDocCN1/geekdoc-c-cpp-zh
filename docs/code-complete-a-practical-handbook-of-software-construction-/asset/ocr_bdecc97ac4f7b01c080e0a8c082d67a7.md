Here’s an example of code that uses bad variable names:

![](bbox=[0.11, 0.125, 0.2, 0.21])

```
Java Example of Poor Variable Names
x = x - xx;
xxx = fido + SalesTax( fido );
x = x + LateFee( x1, x ) + xxx;
x = x + Interest( x1, x );
```

What’s happening in this piece of code? What do x1, xx, and xxx mean? What does fido mean? Suppose someone told you that the code computed a total customer bill based on an outstanding balance and a new set of purchases. Which variable would you use to print the customer’s bill for just the new set of purchases?

Here’s a version of the same code that makes these questions easier to answer:

```
Java Example of Good Variable Names
balance = balance - lastPayment;
monthlyTotal = newPurchases + SalesTax( newPurchases );
balance = balance + LateFee( customerID, balance ) + monthlyTotal;
balance = balance + Interest( customerID, balance );
```

In view of the contrast between these two pieces of code, a good variable name is readable, memorable, and appropriate. You can use several general rules of thumb to achieve these goals.

# The Most Important Naming Consideration

![](bbox=[0.1, 0.65, 0.21, 0.75])

The most important consideration in naming a variable is that the name fully and accurately describe the entity the variable represents. An effective technique for coming up with a good name is to state in words what the variable represents. Often that statement itself is the best variable name. It’s easy to read because it doesn’t contain cryptic abbreviations, and it’s unambiguous. Because it’s a full description of the entity, it won’t be confused with something else. And it’s easy to remember because the name is similar to the concept.

For a variable that represents the number of people on the U.S. Olympic team, you would create the name numberOfPeopleOnTheUsOlympicTeam. A variable that represents the number of seats in a stadium would be numberOfSeatsInTheStadium. A variable that represents the maximum number of points scored by a country’s team in any modern Olympics would be maximumNumberOfPointsInModernOlympics. A variable that contains the current interest rate is better named rate or interestRate than r or x. You get the idea.