
## 5.2 Condition-Controlled Loops: While, Do-While, and Do-Until

Notice that the Do-Until loop is a posttest. First, one or more statements are executed, and then a condition is tested. If the condition is false, the program's execution flows back to the point after the first statement in the body of the loop, and this repeats. If the condition is true, the program exits the loop.

> NOTE: Because the Do-Until loop is a posttest, it will always iterate at least one time.

### Writing a Do-Until Loop in Pseudocode

In pseudocode, we will use the Do-Until statement to write a Do-Until loop. Here is the general format of the Do-Until statement:

```
Do
statement
statement
etc.
Until condition // These statements are the body of the loop. They are always performed once, and then repeated until the condition is true.
```

In the general format, the statements that appear in the lines between the Do and the Until clauses are the body of the loop. The condition that appears after the While is a Boolean expression. When the loop executes, the statements in the body of the loop are executed, and then the condition is tested. If the condition is true, the loop starts over and the statements in the body are executed again.

As shown in the general format, you should use the following conventions to write a Do-Until statement:

- Make sure the do clause and the Until clause are aligned.
- Indent the statements in the body of the loop.

The pseudocode in Program 5-7 shows an example of the Do-Until loop. The loop in lines 6-16 repeatedly asks the user to enter a string until "prospero" is entered. Figure 5-11 shows a flowchart for the program.

Program 5-7
```
1 // Declare a variable to hold the password.
2 Declare String password
3
4 // Repeatedly ask the user to enter a password
5 until the correct one is entered.
6 Do
7 // Prompt the user to enter the password.
8 Display "The password."
9 Input password
10
11 // Display an error message if the wrong
12 // password was entered.
13 If password != "prospero" Then
14 Display "Sorry, try again."
15 End If
16 Until password == "prospero"
```

```
17 // Indicate that the password is confirmed.
18 Display "Password confirmed."
19
```

Program Output (with Input Shown in Bold)
Enter the password.
ariel [Enter]
Sorry, try again.
enter the password.
callibah [Enter]
Sorry, try again.
enter the password.
prospero [Enter]
Password confirmed.

Figure 5-11 Flowchart for Program 5-7

![](img/c939132f78787c7f339c6977b3fc8c85_214_0.png)

## 5.3 Count-Controlled Loops and the For Statement

> NOTE: Not all programming languages provide a Do-Until loop because you can write a Do-While loop that is logically equivalent to any Do-Until loop.

### Deciding Which Loop to Use

In this section, we have introduced three different types of condition-controlled loop: the Do-While loop, the Do-While loop, and the Do-Until loop. When you write a program that requires a condition-controlled loop, you will have to decide which loop to use.

You want to use the While loop to repeat a task as long as a condition is true. The While loop is a preprocess loop, so it is ideal in situations where the condition might be false to start, and in such cases you do not want the loop to iterate at all. The pseudocode that you saw in Program 5-2 is a good example.

The Do-While loop is also a candidate in situations where a task must be repeated as long as a condition is true. It is a posttest loop, so it is the best choice when you always want the task to be performed at least once, regardless of whether the condition is true or false to start.

The Do-Until loop is also a posttest loop, so it performs a task at least once. It is the best choice when you want to perform a task until a condition is true. The Do-Until loop will repeat as long as its condition is false. When the condition is true, the Do-Until loop stops.

### Checkpoint

- 5.4 What is a loop iteration?
- 5.5 What is the difference between a preprocess loop and a posttest loop?
- 5.6 Does the Do-While loop test its condition before or after it performs an iteration?
- 5.7 What is an infinite loop?
- 5.8 What is the difference between a Do-While loop and a Do-Until loop?

## 5.3 Count-Controlled Loops and the For Statement

CONCEPT: A count-controlled loop iterates a specific number of times. Although you can write the logic of a condition-controlled loop so it iterates a specific number of times, most languages provide a loop known as the For loop, which is specifically designed as a count-controlled loop.

As mentioned at the beginning of this chapter, a count-controlled loop iterates a specific number of times. Count-controlled loops are commonly used in programs. For example, suppose a business is open six days per week, and you are going to write a program that calculates the total sales for a week. You will need a loop that iterates exactly six times. Each time the loop iterates, it will calculate the sales.

The way a count-controlled loop works is simple: it uses a variable, called counter, to store the number of times it has performed. A count-controlled loop typically performs three actions: initialization, test, and increment.

- Initialization: Before the loop begins, the counter is set to the starting value.
- Test: The counter is compared to the maximum value. If the counter is greater than maxValue, the loop stops. Otherwise:
    a. The statements that appear in the body of the loop are executed.
    b. The counter is incremented.
    c. The loop starts over at Step 2.

Figure 5-12 Logic of count-controlled loop
![](img/c939132f78787c7f339c6977b3fc8c85_216_0.png)

## 5.3 Count-Controlled Loops and the For Statement

A count-controlled loop iterates a specific number of times. Count-controlled loops are commonly used in programs. For example, suppose a business is open six days per week, and you are going to write a program that calculates the total sales for a week. You will need a loop that iterates exactly six times. Each time the loop iterates, it will calculate the sales for the day.

The way a count-controlled loop works is simple: it uses a variable, called counter, to store the number of times it has performed. A count-controlled loop typically performs three actions: initialization, test, and increment.

- Initialization: Before the loop begins, the counter is set to the starting value.
- Test: The counter is compared to the maximum value. If the counter is greater than maxValue, the loop stops. Otherwise:
    a. The statements that appear in the body of the loop are executed.
    b. The counter is incremented.
    c. The loop starts over at Step 2.

Figure 5-12 Logic of count-controlled loop
![](img/c939132f78787c7f339c6977b3fc8c85_216_0.png)

### The For Statement

A count-controlled loop iterates a specific number of times. Count-controlled loops are commonly used in programs. For example, suppose a business is open six days per week, and you are going to write a program that calculates the total sales for a week. You will need a loop that iterates exactly six times. Each time the loop iterates, it will calculate the sales for the day.

The way a count-controlled loop works is simple: it uses a variable, called counter, to store the number of times it has performed. A count-controlled loop typically performs three actions: initialization, test, and increment.

- Initialization: Before the loop begins, the counter is set to the starting value.
- Test: The counter is compared to the maximum value. If the counter is greater than maxValue, the loop stops. Otherwise:
    a. The statements that appear in the body of the loop are executed.
    b. The counter is incremented.
    c. The loop starts over at Step 2.

Figure 5-13 Count-controlled loop
![](img/c939132f78787c7f339c6977b3fc8c85_217_0.png)

A count-controlled loop iterates a specific number of times. Count-controlled loops are commonly used in programs. For example, suppose a business is open six days per week, and you are going to write a program that calculates the total sales for a week. You will need a loop that iterates exactly six times. Each time the loop iterates, it will calculate the sales for the day.

The way a count-controlled loop works is simple: it uses a variable, called counter, to store the number of times it has performed. A count-controlled loop typically performs three actions: initialization, test, increment.

Program 5-8
```
1 Declare Integer counter
2 Constant Integer MAX_VALUE = 5
3
4 For counter = 1 To MAX_VALUE
5 Display "Hello world"
6 End For
```

Program Output
```
Hello world
Hello world
Hello world
Hello world
Hello world
```
