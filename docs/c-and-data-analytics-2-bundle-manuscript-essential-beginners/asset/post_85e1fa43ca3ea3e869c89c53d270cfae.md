
This loop executes a statement sequence over and over again while abbreviating the code that manages the loop variables.

Written like this

```
for ( init; condition; increment)
{
    statement(s);
}
```

### Do...while loop

The Do...while loop is going to be similar to the while statement, but it is going to test the condition when you reach the end of your statement, rather than the beginning.

Written like this

```
do
{
    statement(s);
} while (condition);
```

### Nested loops

The nested loop is going to have a loop that works inside of another loop, to create a continuous loop of loops. This one can get confusing after awhile.

Written like this

tutorials for other languages as well, not just C++; dabble around and see what you like.

## Chapter 5: Working with Operators in C++

With any of the coding languages that you plan to use, it is important that you learn how to use the operators. These are going to help you to tell the program what you would like to do and can make dealing with your own codes so much easier. There are four main types of operators that you are able to use inside your program and they will each tell the program how to behave in a different way. Some of the operators that you will be able to use with the C++ language include:

- Logical operators
- Arithmetic operators
- Assignment operators
- Relational operators

Let’s take a look at how some of these work and how you can bring them out to work well when writing code in the C++ language.

### Logical operators

The first type of operator that we are going to use in this guidebook are the logical operators. These are going to help you to compare some of the parts that you are putting into the system. Some of the logical operators that you can work with include:

- `||`: this is known as the logical OR. With this one, the condition is going to be true if one of your operands is not zero.
- `&&`: this one is known as the logical AND. If you have two operands and they are not zero, your condition is true.
- `!`: this is the logical NOT. You will be able to use this to reverse the status of your operand. So if the condition ends up being false, this sign will make it true.

### Arithmetic operators

Another of the operators that you are able to use is the arithmetic operators. These are pretty much the same as using math in school. You are going to tell the program to add, subtract, and do other equations with the information that you are providing. Some of the arithmetic operators that you are able to use include:

- `+`: this is the addition operator that will add together two operands of your choices.
- `-`: this is the subtraction operator. It is going to take the right hand operand and subtract it from the left hand operand.
- `*`: this is the operator that makes it possible to do multiplication in the C++ language.
- `/`: this operator helps you to do division in C++.
- `++`: this is the increment operator. It is going to increase the value of your operand by one.
- `--`: this is the decrement operator. It is going to decrease the operand value by just one.

### Assignment operators

The assignment operators will make it easier for you to assign a name to your variable and can help with searching for, saving, and so on with the different parts of the code that you are writing. Some of the assignment operators that you may use inside of C++ include:

- `=`: this operator is the simple assignment operator. It is going to assign the value of the operand on the right hand to the one that is on the left.
- `+=`: this one is called the Add AND operator. It is going to add together the values from both operands and then assigns the sum of these over to the operand on the left side.
- `*=` : this is the Multiply AND operator. It is going to multiply both of the operands and then gives the results over to the operand on the left side.
- `-=`: this is the one that will subtract the value of your operand on the right side from the one on the left and then gives this difference to the left operand.
- `/=` : this is the divide AND operator. It is going to divide the value that is on the left side by the one on the right side and then assigns this amount to the left operand.

### Relational operators

- `==`: this operator is going to check the equality of your two operands. If they are equal, the condition will be true.
- `>`: this operator is going to check the value of your operands. If the operand on the left side is higher than the one on the right, the condition will be true.
- `<`: this operator is basically the opposite of the one above. If you find that the value of your operand on the left side is less than the one on the right side, the condition will be true.
- `!=`: this one is going to check the equality of your two operands and if the values are unequal, your condition is true.
- `<=`: this operator is going to check whether the operand on the left side is less than or equal to the operand on the right side. If it meets this criteria, the condition is true.
- `>=`: this one is going to check if the value of the operand on the left side is greater than or equal to the one on the right side. If it is true, the condition is true.

## Chapter 6: Helping C++ to Make Decisions

There are times when you will need the program to make decisions for you. You are able to set it up to act in a certain way based on the information that the user puts into the computer and what you decide needs to be met for the conditions to be true. The decision making is a bit more advanced inside of this system, but you will find that is pretty easy to learn and will open up a lot of ideas that you are able to work with in the C++ system. Let’s take a look at some of the things that you are able to do to help the system to make decisions on its own.

### Switch Statements

The first decision that we are going to work with inside of this system are the switch statements. These statements are nice because they are going to allow you to check the equality of your variable against a set of values, or cases. The variable that you are trying to check is going to be compared with each of the cases. A good example of the syntax that you are able to use for this include:

```
switch (expression) {
    case constant-expression:
        statement(s);
        break; // optional
    case constant-expression:
        statement(s);
        break; // optional

    // you can add in as many of these case statements as you would like

    default: // optional
        statement(s);
}
```

When you are working inside of these statements, there are a few rules that you should keep in mind. First, the expression of the switch statement should be the integral or enumerated class type. In addition, it can also belong to a class that has a conversion function. With C++, there isn’t going to be a limit to the amount of case statements that you add into the syntax so you can make them as long or short as you would like. Just

### If Statements

One of the most basic things that you are able to do in your programs is create an if statement. These are going to be based on a true and false idea inside the system. If the system says that the input is true with the condition that you set out, then the program is going to run whatever you ask it to. For example, you set it up to have the system ask what the answer to 2 + 2 is. If the user puts in the answer as 4, you could have a message come up that says “That is Correct! Good Job!”

Any time that the user puts in an input that ends up being true based on the conditions that you are setting out, you are going to get the statement to show up that you picked out. On the other hand, what is going to happen if the person puts in the wrong answer. If they put the answer as 5 to the question above, it is not going to be right and the system is going to see that the answer is false.

Since the if statement is pretty basic, you are going to find that it is not going to be prepared if the person puts in the wrong answer. At this stage, if they put in any number other than 4 for the example above, the screen is just going to go blank and nothing is going to happen.
