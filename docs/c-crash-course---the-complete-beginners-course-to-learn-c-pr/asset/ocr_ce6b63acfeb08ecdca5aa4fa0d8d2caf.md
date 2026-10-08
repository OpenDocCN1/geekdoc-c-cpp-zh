# # Chapter 4
Operators

**Objective:** Operators are a good follow-up to data types, because they perform the operations on your values. This chapter discusses the main operators in C# and how you use them to manipulate your code.

After you store values to your variables, you need to perform actions, whether they are mathematical calculations or just string manipulation. Regardless of what you need to do with the variables, you need an operator to perform each action. In this chapter, we discuss operators and how you can use them for your C code.

# ## Mathematical Operators

Mathematical operators are probably the most common, because you'll need to perform some type of calculation on your numeric variables. Mathematical operators are intuitive, because they follow the same rules that you learned in math class. Mathematical operators include addition, subtraction, division, and multiplication. C# also has a modulus operator for division remainders. With programming in C-style languages, you can also choose to use incremental and decremental operators. We'll cover all of these in this section.

The first operator is the addition operator. As the name suggests, you use this operator to add a value to an existing variable. The following code shows you how to add in C#.

```
int myNumber = 3;
int addedNumber = myNumber + 4;
```

In the code above, we first created a variable and then we created a second variable that contained the result of the addition of myNumber to 4. As you can probably guess, the result is 7.

The next operator is subtraction. Just like the addition operator, the subtraction operator is intuitive. It simply subtracts a number from a variable. The following code is an example of the subtraction operator.

```
int myNumber = 3;
int addedNumber = myNumber - 4;
```

The code above is the same as that we used in the addition example, except this time we subtracted the number 4 from the myNumber variable. The result is -1, stored in the addedNumber variable.