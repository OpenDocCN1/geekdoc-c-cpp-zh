
- Are all the declared variables being used?
- Are all variables bound at appropriate times—that is, are you striking a conscious balance between the flexibility of late binding and the increased complexity associated with late binding?
- Does each variable have one and only one purpose?
- Is each variable’s meaning explicit, with no hidden meanings?

## Key Points

- Data initialization is prone to errors, so use the initialization techniques described in this chapter to avoid the problems caused by unexpected initial values.
- Minimize the scope of each variable. Keep references to a variable close together. Keep it local to a routine or class. Avoid global data.
- Keep statements that work with the same variables as close together as possible.
- Early binding tends to limit flexibility but minimize complexity. Late binding tends to increase flexibility but at the price of increased complexity.
- Use each variable for one and only one purpose.

## Chapter 11: The Power of Variable Names

### Contents

- 11.1 Considerations in Choosing Good Names: page 259
- 11.2 Naming Specific Types of Data: page 264
- 11.3 The Power of Naming Conventions: page 270
- 11.4 Informal Naming Conventions: page 272
- 11.5 Standardized Prefixes: page 279
- 11.6 Creating Short Names That Are Readable: page 282
- 11.7 Kinds of Names to Avoid: page 285

### Related Topics

- Routine names: Section 7.3
- Class names: Section 6.2
- General issues in using variables: Chapter 10
- Formatting data declarations: “Laying Out Data Declarations” in Section 31.5
- Documenting variables: “Commenting Data Declarations” in Section 32.5

As important as the topic of good names is to effective programming, I have never read a discussion that covered more than a handful of the dozens of considerations that go into creating good names. Many programming texts devote a few paragraphs to choosing abbreviations, spout a few platitudes, and expect you to fend for yourself. I intend to be guilty of the opposite: to inundate you with more information about good names than you will ever be able to use!

This chapter’s guidelines apply primarily to naming variables—objects and primitive data. But they also apply to naming classes, packages, files, and other programming entities. For details on naming routines, see Section 7.3, “Good Routine Names.”

### 11.1 Considerations in Choosing Good Names

You can’t give a variable a name the way you give a dog a name—because it’s cute or it has a good sound. Unlike the dog and its name, which are different entities, a variable and a variable’s name are essentially the same thing. Consequently, the goodness or badness of a variable is largely determined by its name. Choose variable names with care.

Here’s an example of code that uses bad variable names:

![](img/649c8eee28c38ca1e062691e45dc9883_296_0.png)

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

### The Most Important Naming Consideration

![](img/649c8eee28c38ca1e062691e45dc9883_296_1.png)

The most important consideration in naming a variable is that the name fully and accurately describe the entity the variable represents. An effective technique for coming up with a good name is to state in words what the variable represents. Often that statement itself is the best variable name. It’s easy to read because it doesn’t contain cryptic abbreviations, and it’s unambiguous. Because it’s a full description of the entity, it won’t be confused with something else. And it’s easy to remember because the name is similar to the concept.

For a variable that represents the number of people on the U.S. Olympic team, you would create the name numberOfPeopleOnTheUsOlympicTeam. A variable that represents the number of seats in a stadium would be numberOfSeatsInTheStadium. A variable that represents the maximum number of points scored by a country’s team in any modern Olympics would be maximumNumberOfPointsInModernOlympics. A variable that contains the current interest rate is better named rate or interestRate than r or x. You get the idea.

Note two characteristics of these names. First, they’re easy to decipher. In fact, they don’t need to be deciphered at all because you can simply read them. But second, some of the names are long—too long to be practical. I’ll get to the question of variable-name length shortly.

Table 11-1 shows several examples of variable names, good and bad:

**Table 11-1 Examples of Good and Bad Variable Names**

| Purpose of Variable | Good Names, Good Descriptors | Bad Names, Poor Descriptors |
|---|---|---|
| Running total of checks written to date | runningTotal, checkTotal | written, ct, checks, CHKTTL, x, x1, x2 |
| Velocity of a bullet train | velocity, trainVelocity, velocityInMph | velt, v, tv, x, x1, x2, train |
| Current date | currentDate, todaysDate | cd, current, c, x, x1, x2, date |
| Lines per page | linesPerPage | lpp, lines, l, x, x1, x2 |

The names currentDate and todaysDate are good names because they fully and accurately describe the idea of “current date.” In fact, they use the obvious words. Programmers sometimes overlook using the ordinary words, which is often the easiest solution. Because they’re too short and not at all descriptive, cd and c are poor names. current is poor because it doesn’t tell you what is current. date is almost a good name, but it’s a poor name in the final analysis because the date involved isn’t just any date, but the current date; date by itself gives no such indication. x, x1, and x2 are poor names because they’re always poor names—x traditionally represents an unknown quantity; if you don’t want your variables to be unknown quantities, think of better names.

Names should be as specific as possible. Names like x, temp, and i that are general enough to be used for more than one purpose are not as informative as they could be and are usually bad names.

![](img/649c8eee28c38ca1e062691e45dc9883_297_0.png)

### Problem Orientation

A good mnemonic name generally speaks to the problem rather than the solution. A good name tends to express the what more than the how. In general, if a name refers to some aspect of computing rather than to the problem, it’s a how rather than a what. Avoid such a name in favor of a name that refers to the problem itself.

A record of employee data could be called inputRec or employeeData. inputRec is a computer term that refers to computing ideas—input and record. employeeData refers to the problem domain rather than the computing universe. Similarly, for a bit field indicating printer status, bitFlag is a more computerish name than printerReady. In an accounting application, calcVal is more computerish than sum.

### Optimum Name Length

The optimum length for a name seems to be somewhere between the lengths of *x* and *maximumNumberOfPointsInModernOlympics*. Names that are too short don’t convey enough meaning. The problem with names like *x1* and *x2* is that even if you can discover what *x* is, you won’t know anything about the relationship between *x1* and *x2*. Names that are too long are hard to type and can obscure the visual structure of a program.

![](img/649c8eee28c38ca1e062691e45dc9883_298_0.png)

Gorla, Benander, and Benander found that the effort required to debug a program was minimized when variables had names that averaged 10 to 16 characters (1990). Programs with names averaging 8 to 20 characters were almost as easy to debug. The guideline doesn’t mean that you should try to make all of your variable names 9 to 15 or 10 to 16 characters long. It does mean that if you look over your code and see many names that are shorter, you should check to be sure that the names are as clear as they need to be.

You’ll probably come out ahead by taking the Goldilocks-and-the-Three-Bears approach to naming variables, as Table 11-2 illustrates.

**Table 11-2 Variable Names That Are Too Long, Too Short, or Just Right**

| Too Long | Too Short | Just Right |
|---|---|---|
| numberOfPeopleOnTheUsOlympicTeam | n, np, ntm | numTeamMembers, teamMemberCount |
| numberOfSeatsInTheStadium | n, ns, nsisd | numSeatsInStadium, seatCount |
| maximumNumberOfPointsInModernOlympics | m, mp, max, points | teamPointsMax, pointsRecord |

### The Effect of Scope on Variable Names

> **Cross-Reference** Scope is discussed in more detail in Section 10.4, “Scope.”

Are short variable names always bad? No, not always. When you give a variable a short name like *i*, the length itself says something about the variable—namely, that the variable is a scratch value with a limited scope of operation.

A programmer reading such a variable should be able to assume that its value isn’t used outside a few lines of code. When you name a variable *i*, you’re saying, “This variable is a run-of-the-mill loop counter or array index and doesn’t have any significance outside these few lines of code.”

A study by W. J. Hansen found that longer names are better for rarely used variables or global variables and shorter names are better for local variables or loop variables
