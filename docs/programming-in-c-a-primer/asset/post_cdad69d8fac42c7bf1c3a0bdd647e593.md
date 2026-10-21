
+   3. if (code is 1)
+     person is male
+   4. if (age is more than 55)
+     person is retired

The if statement may be implemented in different forms depending on the complexity of the conditions to be tested.

+   1. Simple if statement
+   2. if..else statement
+   3. Nested if..else statement
+   4. else if ladder

## 6.3 SIMPLE IF STATEMENT

The general form of a simple if statement is

```
if(boolean-expression)
{
    statement-block;
}
statement-x;
```

The ‘statement-block’ may be a single statement or a group of statements. If the boolean-expression is true, the statement-block will be executed; otherwise the statement-block will be skipped and the execution will jump to the statement-x.

It should be remembered that when the condition is true both the statement-block and the statement-x are executed in sequence. This is illustrated in Fig. 6.2.

Consider the following segment of a program that is written for processing of marks obtained in an entrance examination.

```
if(category == SPORTS)
{
    marks = marks + bonus_marks;
}
System.Console.WriteLine(marks);
```

The program tests the type of category of the student. If the student belongs to the SPORTS category, then additional bonus_marks are added to his marks before they are printed. For others, bonus_marks are not added.

Consider a case having two test conditions, one for weight and another for height. This is done using the compound relation

```
if(weight < 50 && height > 170) count = count +1;
```

This could have been done equivalently using two if statements as follows:

```
if(weight<50)
if(height>170)
count = count+1;
```

![](img/bae4ee2c7c29c052feb3b9a9c5659998_98_0.png)

If the value of weight is less than 50, then the following statement is executed, which in turn is another if statement. This if statement tests height and if the height is greater than 170, then the count is incremented by 1. Program 6.1 illustrates the implementation of the above statement.

## Program 6.1 COUNTING WITH IF STATEMENT

```
using System;
class IfTest
{
    public static void Main()
    {
        int i, count, count1, count2;
        float[] weight = { 45.0F,55.0F,47.0F,51.0F,54.0F };
        float[] height = { 176.5F,174.2F,168.0F,170.7F,169.0F };

        count = 0;
        count1 = 0;
        count2 = 0;

        for (i = 0; i <= 4; i++)
        {
            if(weight[i] < 50.0 && height[i] > 170.0)
            {
                count1 = count1 + 1; // Executed when condition is true
            }
            count = count + 1;   // Always executed
        }
        count2 = count - count1;
        Console.WriteLine("Number of persons with ...");
        Console.WriteLine("Weight<50 and height>170 = "+count1);
        Console.WriteLine("Others = " + count2);
    }
}
```

The output of Program 6.1 will be:
    Number of persons with ...
    Weight<50 and height>170 = 1
    Others = 4

C and C++ programmers must note that in C# the expression in an if statement must resolve to a bool value. We cannot use integer values, like if(x).... Arrays are discussed in Chapter 9.

## 6.4 THE IF... ELSE STATEMENT

The if...else statement is an extension of the simple if statement. The general form is

```
if(boolean_expression)
{
    True-block statement(s)
}
else
{
```

# False-block statement(s)

} statement-x

If the boolean_expression is true, then the true-block statement(s), immediately following the if statement, are executed; otherwise, the false-block statement(s) are executed. In either case, either true-block or false-block will be executed, not both. This is illustrated in Fig. 6.3. In both the cases, the control is transferred subsequently to the statement-x.

Let us consider an example of counting the number of boys and girls in a class. We use code 1 for a boy and 2 for a girl. The program statements to do this may be written as follows:

```
........
........
if(code == 1)
    boy = boy + 1;
if(code == 2)
    girl = girl + 1;
........
........
```

![](img/bae4ee2c7c29c052feb3b9a9c5659998_100_0.png)

The first test determines whether or not the student is a boy. If yes, the number of boys is increased by 1 and the program continues to the second test. The second test again determines whether the student is a girl. This is unnecessary. Once a student is identified as a boy, there is no need to test again for a girl. A student can be either a boy or a girl, not both. The above program segment can be modified using the else clause as follows:

```
........
........
if(code == 1)
    boy = boy +1;
else
    girl = girl + 1;
xxx;
........
```

Here, if the code is equal to 1, the statement boy = boy + 1; is executed and the control is transferred to the statement xxx, after skipping the else part. If the code is not equal to 1, the statement boy = boy + 1; is skipped and the statement in the else part girl = girl + 1; is executed before the control reaches the statement xxx.

Program 6.2 counts the even and odd numbers in a list of numbers using the if....else statement.

## Program 6.2 | EXPERIMENTING WITH IF....ELSE STATEMENT

```
using System;
class IfElseTest
{
public static void Main()
```

```
{
int[] number = { 50, 65, 56, 71, 81 };
int even = 0, odd = 0;

for (int i = 0; i < number.Length; i++)
{
    if ((number[i] % 2) == 0) // use of modulus operator
    {
        even += 1; // counting EVEN numbers
    }
    else
    {
        odd += 1; // counting ODD numbers
    }
}

Console.WriteLine("Even Numbers : " + even);
Console.WriteLine("Odd Numbers : " + odd);
}
```

Output of Program 6.2 would be:
    Even Numbers  : 2
    Odd Numbers   : 3
Note that number.Length gives the length of number array.
Program 6.3 presents different ways of using if statement in C#, including a single if statement, if-else construct and multiple else if statements. The program takes a number as an input from the user and provides information about the number using the various forms of if statement.

## Program 6.3 | IF ELSE ILLUSTRATED FURTHER

```
using System;
class IfElseExample
{
    public static void Main()
    {
        string numInput;
        int numValue;

        Console.Write("Please enter a number: ");
        numInput = Console.ReadLine();
        numValue = Int32.Parse(numInput);

        // A Single Decision with its Action
        if (numValue > 0)
        {
            Console.WriteLine("The number {0} is greater than zero.", numValue);
        }
        // A Single Decision with its Action without brackets

```
if (numValue < 0)
    Console.WriteLine("The number {0} is less than zero.", numValue);
// A Decision using Logical Operator
if (numValue != 0)
{
    Console.WriteLine("The number {0} is not equal to zero.", numValue);
}
else
{
    Console.WriteLine("The number {0} is equal to zero.", numValue);
}
// Multiple Else If Conditions
if (numValue < 0 || numValue == 0)
{
    Console.WriteLine("The number {0} is less than or equal to zero.", numValue);
}
else if (numValue > 0 && numValue <= 10)
{
    Console.WriteLine("The number {0} falls in the range from 1 to 10.", numValue);
}
else if (numValue > 10 && numValue <= 20)
{
    Console.WriteLine("The number {0} falls in the range from 11 to 20.", numValue);
}
else if (numValue > 20 && numValue <= 30)
{
    Console.WriteLine("The number {0} falls in the range from 21 to 30.", numValue);
}
else
{
    Console.WriteLine("The number {0} is greater than 30.", numValue);
}
}
```

```
C:\WINNT\system32\cmd.exe

C:\Chapter 6>IfElseExample
Please enter a number: 44
The number 44 is greater than zero.
The number 44 is not equal to zero.
The number 44 is greater than 30.

C:\Chapter 6>
```

## 6.5 NESTING OF IF....ELSE STATEMENTS

When a series of decisions are involved, we may have to use more than one if....else statement in nested form as follows:

The logic of execution is illustrated in Fig. 6.4. If the condition-1 is false, the statement-3 will be executed; otherwise it continues to perform the second test. If the condition-2 is true, then statement-1 will be evaluated; otherwise statement-2 will be evaluated and the control transferred to statement-x.

A commercial bank has introduced an incentive policy of giving a bonus to all its deposit holders. The policy is as follows: A bonus of 2 per cent of the balance held on 31st December is given to every one, irrespective of their balances, and 5 per cent is given to female account holders if their balance is more than Rs 5000. This logic can be coded as follows:

```
......
if(sex is female)
{
    if (balance > 5000)
        bonus = 0.05 * balance;
    else
        bonus = 0.02 * balance;
}
else
{
    bonus = 0.02 * balance;
}
 balance = balance + bonus;
........
```

When nesting, care should be exercised to match every if with an else. Consider the following alternative to the above program (which looks right at first sight):

```
if(sex is female)
    if(balance > 5000)
        bonus = 0.05 * balance;
else
    bonus = 0.02 * balance;
    balance = balance + bonus;
```

There is an ambiguity as to over which if the else belongs to. In C# an else is linked to the closest non-terminated if. Therefore, the else is associated with the inner if and there is no else option for the outer if. This means that the computer is trying to execute the statement
balance = balance + bonus;
without really calculating the bonus for the male account holders.

![](img/bae4ee2c7c29c052feb3b9a9c5659998_103_0.png)

Fig. 6.4 Flowchart of nested if....else statements

Consider another alternative which also looks correct:
