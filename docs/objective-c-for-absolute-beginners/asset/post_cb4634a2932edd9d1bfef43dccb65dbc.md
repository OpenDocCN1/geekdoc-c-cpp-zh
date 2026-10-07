
The Boolean operator XOR means exclusive-or. An easy way to remember how the XOR operator will return a TRUE if only one argument is TRUE, not both.

Objective-C does not have these operators built in, but consider that NAND and NOR mean NOT AND and NOT OR. After evaluating the AND and the OR arguments and results, simply negate the results.

## Truth Tables

Let's use a tool to help you evaluate all the Boolean Operators. A truth table is mathematical table used in logic to evaluate Boolean operators. They are helpful when trying to determine all the possibilities of a Boolean operator. Let's look at some common truth tables for AND, OR, XOR, NAND, and NOR.

In an AND truth table, there are four possible combinations of TRUE AND FALSE.

- TRUE AND TRUE = TRUE
- TRUE AND FALSE = FALSE
- FALSE AND TRUE = FALSE
- FALSE AND FALSE = FALSE

Placing these combinations in a truth table results in Table 4–1.

Table 4–1. An AND Truth Table

| A | B | A AND B |
|---|---|---|
| TRUE | TRUE | TRUE |
| TRUE | FALSE | FALSE |
| FALSE | TRUE | FALSE |
| FALSE | FALSE | FALSE |

An AND truth table only produces a TRUE result if both of its operands are TRUE.

Table 4–2 illustrates an OR truth table and all possible operands.

## CHAPTER 4: Making Decisions About...and Planning Program Flow

Table 4–2. An OR Truth Table

| A | B | A OR B |
|---|---|---|
| TRUE | TRUE | TRUE |
| TRUE | FALSE | TRUE |
| FALSE | TRUE | TRUE |
| FALSE | FALSE | FALSE |

An OR truth table produces a TRUE result if one or both of its operands are TRUE.

Table 4–3 illustrates a NOT truth table and all possible operands.

Table 4–3. A NOT Truth Table

| NOT | RESULT |
|---|---|
| TRUE | FALSE |
| FALSE | TRUE |

A NOT flips-the-bit or negates the original operand's Boolean value.

Table 4–4 illustrates an XOR (or exclusive-or) truth table and all possible operands.

Table 4–4. An XOR Truth Table

| A | B | A XOR B |
|---|---|---|
| TRUE | TRUE | FALSE |
| TRUE | FALSE | TRUE |
| FALSE | TRUE | TRUE |
| FALSE | FALSE | FALSE |

The operator XOR yields a TRUE result if only one of the operands is TRUE.

Table 4–5 illustrates a NAND truth table and all possible operands.

## Table 4–5. A NAND Truth Table

| A | B | A NAND B |
|---|---|---||
| TRUE | TRUE | FALSE |
| TRUE | FALSE | TRUE |
| FALSE | TRUE | TRUE |
| FALSE | FALSE | TRUE |

Table 4–6 illustrates a NOR truth table and all possible operands.

## Table 4–6. A NOR Truth Table

| A | B | A NOR |
|---|---|--|
| TRUE | TRUE | FALSE |
| TRUE | FALSE | FALSE |
| FALSE | TRUE | FALSE |
| FALSE | FALSE | TRUE |

The easiest way to look at the NAND and NOR operators is to simply negate the results from the AND and OR truth tables, respectively.

## Comparison Operators

In software development, the comparison of different data items is accomplished with comparison operators. These operators produce a logical TRUE or FALSE result. Table 4–7 shows the list of comparison operators.

## Table 4–7. Comparison Operators

- > greater than
- < less than
- >= greater than or equal to
- < less than or equal to
- == exactly equal to
- != not equal to

## Designing Apps

Now that we've introduced Boolean logic and comparison operators, you can start designing your apps. Sometimes, it's important to express all or parts of apps to others without having to write the actual code.

Writing code helps a developer think out loud and brainstorm with other developers regarding sections of code that are of concern—this helps to analyze problems and possible solutions before coding begins.

## Pseudo-Code

**Pseudo-code** refers to writing out code that is a high-level description of an algorithm you are trying to solve. Pseudo-code does not contain the necessary programming syntax for coding; however, it expresses the algorithm that is necessary to solve the problem at hand.

Pseudo-code can be written by hand on paper (or a whiteboard) or typed on a computer.

Using pseudo-code, you can apply what you know about Boolean data types, truth tables, and comparison operators. Refer to Listing 4–1 for pseudo-code examples.

**Listing 4–1.** *Pseudo-Code Examples Using Conditional Operators in If-Then-Else Code*

```
int x = 5;
int y = 6;
isComplete = TRUE;
if (x < y)
{
    // in this example, x is less than 6
    do stuff;
}
else
{
    do other stuff;
}
if (isComplete == TRUE)
{
    // in this example, isComplete is equal to TRUE
    do stuff;
}
else
{}
```

```
do other stuff;
//another way to check isComplete == TRUE
if (isComplete)
{
    //in this example, isComplete is TRUE
    do stuff;
}
//two ways to check if a value is false
if (isComplete == FALSE)
{
    do stuff;
}
else
{
    //in this example, isComplete is TRUE so the else block will be executed
}
//another way to check isComplete == FALSE
if (isComplete)
{
    do stuff;
}
else
{
    //in this example, isComplete is TRUE so the else block will be executed
```

Note that the ! switches the value of the Boolean it's applied to; so, using ! makes a TRUE value into a FALSE, and a FALSE value into a TRUE.

Often it is necessary to combine your comparison tests. A compound relationship is one or more simple relationship tests joined by either the && or || (two pipe characters).

&& and || are verbalized as logical-and and logical-or, respectively. Pseudo-code in Listing 4–2 illustrates logical-and and logical-or operators.

## Listing 4-2. Using && and || Logical Operators

```
int x = 5;
int y = 6;
isComplete = TRUE;
//using the logical and
if (x < y && isComplete == TRUE)
{
    //in this example, x is less than 6 and isComplete == TRUE
    do stuff;
}
if (x < y || isComplete == FALSE)
{
    //in this example, x is less than 6.
//Only one operand has to be TRUE for an OR to result in a TRUE.
//See Table 4-2 A OR Truth Table
    do stuff;
}
//another way to test for TRUE
if (x < y && isComplete)
```

```
{
  //in this example, x is less than 6 and isComplete == TRUE
  do stuff;
}
//another way to test for FALSE
if (x < y && !isComplete) {
  do stuff;
} else {
  //isComposite == TRUE
  do stuff;
}
```

## Design Requirements

As discussed in Chapter 1, the most expensive process in the software development life cycle is writing code. The least expensive process in the software development life cycle is gathering the requirements for your application; yet, this latter is the most overlooked and least used in software development.

Design requirements usually begin by asking clients, customers, and/or stakeholders how the application should work and what problems it should solve.

With respect to apps, requirements can include long or short descriptions, screen mockups, and formulas. It is far easier to open your word processor and change the requirements and screen mockups before coding begins than it is to modify iPhone/Mac app. The following is the design requirement for one view of a banking app:

- View: Accounts View
- Description: Displays the list of accounts the user has. The list of accounts will be in the following sections: Business Accounts, Personal Accounts and Car Loans, IRA, and Home Equity Loans.
- Cells: Each cell will contain the account name, the last four digits of the account, available balance, and present balance.

A picture is worth a thousand words. Screen mockups are helpful to developers and users because they can visualize how the views will look when they are. There are many tools that can quickly design mockups; one of these tools is OmniGraffle. See Figure 4–1 for an example of a screen mockup generated by OmniGraffle.

![](img/322e107ddf8f5cd963a6efafdcd86f38_79_0.png)

**Figure 4–1.** Screen mockup for a mobile app using OmniGraph and the ultimate iPhone Stencil Plug-in

Many developers believe that design requirements that take too long and are unnecessary. There is a lot of information presented on the Accounts screen in Figure 4–1. Many business rules can determine how information is displayed to the user, along with all of the error handling when things go bad. When designing your app, working with all the business stakeholders at the beginning of the development process is critical to getting it right the first time.

Figure 4–2 is an example of all stakeholders involved in your app's development. Having all stakeholders involved in every view from the beginning will eliminate multiple rewrites and application bugs.
