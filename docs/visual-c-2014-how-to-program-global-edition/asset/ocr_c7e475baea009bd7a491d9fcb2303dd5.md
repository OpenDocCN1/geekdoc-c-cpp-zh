# Answers to Self-Review Exercises 223

5.6 Combine the statements that you wrote in Exercise 5.5 into a C# app that calculates and displays the sum of the integers from 1 to 10. Use a while loop to loop the calculation and increment statements. The loop should terminate when the value of x becomes 11.

5.7 Determine the values of the variables in the following statement after it executes. Assume that when the statement begins executing, all variables are int and have the value 5.

```
product *= x++;
```

5.8 Identify and correct the errors in each of the following sets of code:

+   a) while (c <= 5)
{
product *= c;
++c;
b) if (gender == 1)
{
Console.WriteLine("Woman");
}
else
{
Console.WriteLine("Man");
}

5.9 What is wrong with the following while statement?
while (z >= 0)
{
sum += z;
}

# Answers to Self-Review Exercises

+   5.1 a sequence, selection, iteration. b) if...else. c) counter-controlled (or definite). d) signal, flag or dummy. e) sequence. f) 0 (zero). g) type. h) prefixed.

+   5.2 a) True. False. A set of statements contained within a pair of braces ({ }) is called a block. b) False. An iteration specifies that an action is to be repeated while some condition remains. A selection statement determines whether an action is performed based on true or falsity of a condition. d) True. e) True. f) True. The unary operator (double) creates a temporary floating-point copy of its operand. h) False. Instance variables of type bool are given the value false by default. i) True.

```
x = x + 1;
x++;
++;
x++;
```

5.4 The answers to Self-Review Exercises 5.4 are as follows:

+   a) z = x ++ + y;
b) if (count > 10)
{
Console.WriteLine("Count is greater than 10");
}
c) total --x;
d) q %= divisor;
q = q % divisor;