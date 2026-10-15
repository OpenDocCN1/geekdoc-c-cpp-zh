
into the if block and executes all the statements as well as instructions defined inside the if block. The syntax of the if statement is as follows:

```
int Number1, Number2;
if (Number1>Number2) // condition {
Console.WriteLine("Number1 is greater than Number2"); //statement
... //statements }
```

In the preceding code snippet, if the condition stated in the if statement is true, then the message, Number1 is greater than Number2, is displayed.

However, sometimes the condition inside the if statement is not fulfilled. In such cases, C# provides the if else statements that executes a block of code when a certain condition is fulfilled and another block of code when a certain condition is not fulfilled. The following code snippet shows the use of the if else statement:

```
if (Number1>Number2) // condition
{
Console.WriteLine("Number1 is greater than Number2"); //statement
... //statements
}
else
{
Console.WriteLine("Number2 is greater than Number1"); //statement
... //statements
}
```

In the preceding code snippet, when the condition (Number1>Number2) is not fulfilled, the program control transfers to the else block and executes the block of code inside it. In order to evaluate multiple conditions one by one, you can do nesting of if else statement. The following code snippet shows an example to understand the syntax of the nested if else statement:

```
if (Number1 > Number2 && Number1 > Number3) //condition
{
Console.WriteLine("Number1 is greatest"); //statement
... //statements
}
else
if (Number2 > Number3) //condition
{
Console.WriteLine("Number2 is greatest"); //statement
...//statements
}
else
{
Console.WriteLine("Number3 is greatest"); //statement
... //statements
}
```

In the preceding code snippet, first a condition (Number1 > Number2 && Number1 > Number3) is checked in the if block. If it is fulfilled, the statement inside the if block is executed; otherwise, the program control transfers to the else if block and checks another condition (Number2 > Number3). If this condition (Number2 > Number3) is fulfilled, then the statement inside the else if block gets executed; otherwise, the program control transfers to the else block.

## The switch Statement

The switch statement is another type of selection statement. The main purpose of the switch statement is to allow the value of a variable or an expression to control the flow of program execution. The variable or an expression is usually referred as the control variable of the switch statement. The switch statement is divided into two main parts, switch and case. In switch statement, the value of a variable inside the switch block is checked with the different case expressions. If the value of variable matches with any of the case expressions, then the statement inside that case statement executes.

The following code snippet shows an example of switch statement:

```
switch (Marks) // test expression
{
case 1: //expression
{
    Console.Write("Your marks are very low");
}
break;
case 2: //expression
{
    Console.Write("Your marks are low");
}
break;
case 3: //expression
{
    Console.Write("Your marks are average");
}
break;
case 4: //expression
{
    Console.Write("Your marks are good");
}
break;
case 5: //expression
{
    Console.Write("Your marks are very good");
}
break;
default:
break;
}
```

The keywords used in the preceding code snippet are as follows:

- switch — Denotes a keyword from where the switch statement starts and holds a test expression within the parenthesis
- test expression — Represents any integral expression, such as int and char, which needs to be compared with the case expression
- case — Denotes a keyword that holds an expression followed by a colon (:)
- expression — Represents any constant value, which is compared with the value of test expression
- break — Denotes a keyword that alters the flow of switch statement
- default — Denotes a keyword that makes the code inside the default block to execute in case none of the other case expression matches with the test expression

The switch statement contains a test expression, such as int, char, and string, and matches the cases with the value of that test expression. The program control flows from one case to another. If the case matches with the specified test expression, the program control is transferred to that specific case statement and the statements inside that case statement are executed. An optional block, known as default case, is also present in the switch statement. It does not specify any expression and is denoted by the default keyword instead of the case keyword. If none of the case expression matches with the test expression, the program execution is transferred to the statement following the default keyword.

## Iteration Statements or Loops

Suppose you want to execute a set of statements 50 times in your program. Instead of writing the code 50 times, you can write the code inside a loop and specify a condition to execute the loop 50 times; thereby, saving the complexity and time involved in coding. An iteration statement or loop executes a statement or a set of statements in a repeated manner. In C#, there are the following four types of iteration statements:

- while loop — Evaluates a condition before executing a loop. The loop continues executing as long as the specified condition is true.
- do...while loop — Executes the loop body at least once, before evaluating a condition.
- for loop — Continues to execute the loop body until the condition specified in the loop becomes false.
- foreach loop — Continues to execute the loop body for each element in an array or object collection.

Let's discuss these iteration statements or loops in detail.

## The while Loop

The while loop executes a statement or a block of statements as long as a Boolean expression (condition) evaluates to true. The while loop is mainly used in situations where you don't know in advance how many times the loop will be executed. The condition specified in the while loop is checked before starting the loop and the statements inside the loop execute as long as the specified condition is true. The loop terminates when the Boolean expression evaluates to false. The following code snippet shows an example of the while loop:

```
int Number= 51;
while (Number <= 50)    //condition
{
    Console.WriteLine("I will be executed 50 times");    //statement
    Number = Number + 1; //increment or decrement
}
```

In the preceding code snippet, the condition is a Boolean expression and the statements can be any C# statements. Before the execution of any statement inside the while loop, the condition is evaluated. If the condition evaluates to true, the statements will be executed, otherwise not. Once the statements inside the while loop are executed, the program control is transferred to the starting point of the while loop to check the condition again for the next iteration.

## The do...while Loop

The working of do...while loop is identical to that of the while loop, except that in the do...while loop, a condition is checked at the end of the loop after each iteration. It means that the do...while loop definitely executes at least once even if the condition is false. Unlike the while loop, a semicolon has to be placed after the while expression in the do...while loop; otherwise, the loop will not execute.

The following code snippet shows the syntax of the do...while loop:

```
int Number = 51;
do {
    Console.WriteLine("I will be executed 50 times "); //statement
    Number = Number + 1; //increment or decrement
}
while (Number <= 50) ; //condition
```

In the preceding code snippet, you can see that Boolean expression inside the while block is not true but the loop is executed once, since in the do...while loop, the condition specified in the while block is checked after executing the loop once.

## The for Loop

The for loop is probably the most important of all loops. It works similar to the while loop, except that the syntax of the for loop also includes an initializer that initializes a variable and a loop expression that increments or decrements the variable's value. Unlike the while loop, the for loop is applied in the situation when you exactly know how many times you want to execute the statements. The syntax of the for loop is as follows:

```
for ( initializer; condition; loop expression) {
    ...    //statements
}
```

The description of the terms used in the preceding syntax is as follows:

- initializer — Specifies the initial value of the variables used inside the loop. It is an expression that is evaluated before the first loop is executed. It is usually the initialization of a local variable as a loop counter.
