# Chapter 3 Introduction to C# App Programming

Possible Erroneous User Input
Technically, the user can type anything as the input value.ReadLine will accept it and pass it off to int's Parse method. This method assumes that the string contains a valid integer value. If the user types a noninteger value, a runtime error called an exception will occur and the app will terminate. The string processing techniques you'll learn in Chapter 16 can be used to check that the input is in the correct format before converting the string to an int. C# also offers a technique called exception handling will help you make your apps more robust by enabling them to handle exceptions and continue executing. We introduce exception handling in Section 8.4, then use it again in Chapter 10. We take a deeper look at exception handling in Chapter 13 and throughout the book.

Assigning a Value to a Variable
In Line 16, the result of the call to int's Parse method (an int value) is placed in variable number1 using the assignment operator, =. The statement reads "number1 gets the value returned by int.Parse." Operator = a binary operator, because it works on two pieces of information. These are known as operands—in this case, the operands are number1 and the result of the method call int.Parse. This statement is called an assignment statement, because it assigns a value to a variable. Everything to the right of the assignment operator, = is evaluated before the assignment is performed.

> Good Programming Practice 3.9
Place spaces on either side of a binary operator to make the code more readable.

# 3.6 Prompting the User for Input and Reading a Value into number2

```
Line 18
Console.Write("Enter second integer:"); // prompt user
prompts the user to enter the second integer.
number2 = int.Parse(Console.ReadLine());
```

# 3.6 Summing number1 and number2

```
Line 22
sum = number1 + number2; // add numbers
calculates the sum of number1 and number2 and assigns the result to variable sum using the assignment operator. The statement reads "sum gets the value of number1 + number2." When number1+number2 is encountered, the values stored in the variables are used in the calculation. The addition operator is a binary operator—two operands. An expression is any part of a statement that has a value associated with it. For example, the value of the expression number1+number2 is the sum of the numbers. Similarly, the value of the expression Console.ReadLine() is the string of characters typed by the user.
```