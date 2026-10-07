# CHAPTER 1: App Cubby

+   - Is 5 larger than 3?
- Does "now" have more than 5 letters?
- Is 6/2010 later than today?

Notice that there are only 2 possible correct answers to these questions: yes and no. if you are asking a question that could have more than 2 answers, that question will be worded differently for programming.

Each of these questions will be represented by an if statement then (for example, if 5 is greater than 3, then print a message to the user). Each if statement is required to have some sort of relational operator. A relational operator can be something like "greater than" or "is equal".

In order to start using these types of questions in your programs, you will first need to become familiar with the different relational operators available to you in the C and Objective-C languages. We will cover these first. After that, we will look into how different variables can behave with these operators.

# Using Relational Operators

Objective-C uses 6 relational operators. These are the standard algebraic operators with one real change: in the Objective-C language, as in most other programming languages, the equal operator is made by two equal signs (=). In chapter 4, Table 4-7, we describe the different operators available to you as a developer.

> NOTE: A single sign (=) is used to assign a value to a variable. Two equal signs (==) are needed to compare two values. For example, if(x=9) will assign 9 to the variable and return "yes" if 9 is successfully assigned to x, which will be in most, if not in all, of the cases. if(x==9) will actually do a comparison to see if x equals 9.

# Comparing Numbers

One of the difficulties developers had in the past was dealing with different data types in comparisons. Earlier in this book, we discussed the different types of variables. You may remember that 1 is an integer. If you wanted to compare an integer with a float such as 1.2, this could cause issues. Frankly, Objective-C helps us out with this. In Objective-C, you can compare any two data types without having to typecast (typecasting is still sometimes needed when dealing with other data types, and we cover this later in the chapter). This allows you to write code without worrying about the data types that need to be compared.