
assignment operator. It assigns a value to a variable. Let's take a look one more time at the assignment operator.

```
int myNumber1 = 1;
```

The assignment operator is used to assign the value of 1 to myNumber.

You can also perform mathematical calculations on a variable and assign the result to it with one line of code. It's a form of shorthand code to use assignment operators with mathematical calculations. You use the same mathematical operators we used in the first section and combine them with the assignment operator.

Let's take a look at example.

```
int myNumber1 = 1;
myNumber1 += 2;
```

In this example, myNumber1 is first assigned the value of 1. The next statement adds 2 to the variable and then assigns it the new value. The second statement evaluates to 3 and assigns it to myNumber1.

You can do the same with any other mathematical operation. Let's take a look at one more example using the multiplication operator.

```
int myNumber1 = 1;
myNumber1 *= 2;
```

Notice that the syntax is used, except we have used the multiplication character. In this example, myNumber1 is multiplied by 2 and the value is assigned to myNumber1. The result is that myNumber1 now contains the value of 2.

Operators are a major part of any programming language, including C#. These operators are present in every major application, so you'll need to know them well to work in any programming language.

# Lab Questions

- 1. What operator tells the if statement to return true and execute its statements if one of two conditions equals true?
- a. ||
- b. &&
- c. !
- d. >=

Explanation: The conditional or operator (||) requires only one condition to equal true to execute the if statement.

- 2. What condition operator evaluates if two variables are greater than or equal to each other?
- a. ||
- b. &&
- c. !=
- d. >=

Explanation: The greater than or equal operator returns true if variable 1 is greater than variable 2 or if both variables are equal to each other.

- 3. What operator is shorthand for adding 1 to a variable?
- a. ||
- b. +
- c. ++
- d. +=

Explanation: The increment operator (++) adds 1 to the variable.

- 4. What operator adds a value to a variable and assigns it to the variable in one line of code?
- a. ||
- b. +
- c. ++
- d. +=

Explanation: The += assignment operator first adds a given value to the variable and assigns the new calculation result to the same variable.

# Chapter 5
Loops and If Statements

Objective: Loops and If statements control the way your code executes. We saw if statements in the last chapter, and we'll dive deeper into them along with a review of loops.

In every program, you need to evaluate statements and execute code depending on the way statements calculate. Loops iterate through a statement until they reach the stop condition, and if statements evaluate two conditions and execute statements based on the results. In this chapter, we'll show you how to use both structures to control the way your code executes.

# The For Loop

The for loop is the most popular of all the loop structures. Loops iterate through a series of conditions until a stop condition is met. If the stop condition is never met, you create an infinite loop, so you always need to remember to include the stop condition. The for loop is the most popular, because it's very difficult to reach the stop condition.

Let's take a look at the general syntax template you use for the for loop.

```
for ( init; condition; increment )
{
// statements execute here
}
```

The for loop initializes a variable, sets a stop condition, and then increments the initialized variable. These three statements are separated by semicolons. With each iteration, the initialized variable is incremented until the condition is met and the loop exits. Let's take a look at an example.

```
for ( int j = 0; j < 5; j++)
{
// statements execute here
}
```

In the above for loop, the j variable is initialized and set to 0. You can set the variable to any value, but the standard is to set it to zero because loops are usually used to iterate through arrays and these structures begin with index 0. The next statement is the condition. As long as j is less than 5, the loop continues. Once j equals 5 or is more than 5, the loop executes. The increment statement adds 1 to j after every loop. Let's add some more detail to what happens during a loop.

```
for ( int j = 0; j < 5; j++)
{
    Console.WriteLine(j.ToString());
}
```

The output from the above loop looks like the following.

- 0
- 1
- 2
- 3
- 4

Notice that the value 5 doesn't print, because when j reaches the 5 value, the loop exits.

You'll see loops again when we work with arrays.

# The While Loop

The while loop is similar to the for loop in that it has the same stop condition setup. However, the while loop does not initialize a variable and doesn't increment it after each iteration. You have a higher chance of causing an infinite loop when you use a while loop because there isn't any auto-incremented value, but you'll need a while loop when you have a condition to use that can't use a numerical condition.

Let's take a look at the while loop template.

```
while (condition)
{
    //while loop statements execute here
}
```

Notice the difference between this loop and the for loop is that this loop only has a condition to determine the next loop. Let's take a look at an example.
```
bool loop = true;
int j = 0;

while (loop)
{
    Console.WriteLine(j);
    if (j == 5)
    {
        loop = false;
    }
    j++;
}
```

Notice using a while loop requires a lot more code. This is one reason they aren’t preferred over a for loop. We first define two variables that we’ll use to control the loop. The while loop is then initiated with its condition. The condition is set to always loop as long as the loop variable is equal to true. Since it's initialized to true, the while loop will iterate at least once.

Within the while loop, we have several statements. The first statement prints out the value of j. The next statement is an if statement that identifies the value of j. If j has reached the value of 5, the if statement flips the loop to false. Finally, the last statement adds 1 to j.

# The If Statement

We covered the if statement little in the last chapter. The if statement is very common in programming, because it’s a way to change the code.

First, let’s take a look at the basic template for an if statement.

```
if (expression)
{
  // statements that execute when the expression equals true
}
```

We already saw some examples, but let’s take a look at another one.

```
int myNumber1 = 1;
int myNumber2 = 2;
if (myNumber1 == 2)
{
  Console.WriteLine("The variable equals the value of 2");
}
```

We used the same code in the previous if statement to give you another example. In this example, we gave the if statement some code to execute. The if statement prints “The variable equals the value of 2” if myNumber1 is equal to 2. Since myNumber1 is initialized to the value of 1, the result is that the if statement does not execute the code within the brackets.

Up until now, we've only looked at an if statement with one condition, but the if statement also lets you combine the condition with an else and an if-else statement. Both of these add even more control to your code. Let's take a look at a template for this statement.

```
if(expression)
{
// statements that execute when the expression equals true
}
else
{
// statements that execute when the expression doesn't equal true
}
```

The above if-else statement gives you an option to execute alternative code should the condition in the if statement evaluate to false.

Let's take a look at some actual code that works with the if-else structure.

```
int myNumber1 = 1;
int myNumber2 = 2;
if (myNumber1 == 2)
{
    Console.WriteLine("The variable equals the value of 2");
}
else
{
    Console.WriteLine("The variable does not equal 2");
}
```

We used the same code in the previous if statement, but we added the else statement. Just like the previous if statement, this one evaluates to false as default. Instead of just skipping the if statements altogether, the else statement executes by default. This time, the result of the if statement execution is that “The variable does not equal 2” is displayed in the console.
