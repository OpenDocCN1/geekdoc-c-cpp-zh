
## Nested Conditional Statements

In cases when we want multiple conditions to be checked, using keywords ‘and’ and ‘or’ makes code hard to read, therefore, we used nested conditional statements. Nested conditional statements are simply if..else blocks inside an if, elif or else block. Below is the general syntax:

```
if *condition is True*:
    if *condition is True*:
        ...... execute this code block .......
    elif *condition is True*:
        ...... execute this code block .......
    else:
        ...... execute this code block .......
else:
        ...... execute this code block .......
```

### Example

In this example, we are going to take a 4-digit year as an input and check if it is a leap year. Now, this is a little more complicated than we think. We know that every 4 years is a leap year. So that is our first check. So, a year like 1996 would be a leap year. But, every 100 years, there is no leap year. So, 1800 and 1900 are not leap years. Also, there is another exception. Every 400 years, it is a leap year. So, 1600 and 2000 are leap years. So, there are 3 checks.

```python
def check_leap(year):
    year = int(year)
    leap = False
    if year % 4 == 0:
        leap = True
        if year % 100 == 0:
            leap = False
            if year % 400 == 0:
                leap = True
    return leap

year = input("Enter the year ")

if check_leap(year):
    print("It is a leap year")
else:
    print("It is not a leap year")
```

The function check_leap takes the year as a parameter and returns True or False based on the conditions. First, we declare a boolean variable ‘leap’ and initially set it to False. Then we perform the following checks:

- If the year is divisible by 4, we set leap to True and return True. Then we enter the second loop to check if it is divisible by 100.
  - If the year is divisible by 100, we set the leap to False since the year might not be a leap year. If it is divisible by both 4 and 100, we enter the 3rd loop to check if it is divisible by 400.
    - If the year is divisible by 400, it must be a leap year, so we set leap to True and return True.
    - If the year is not divisible by 400, but it is divisible by 100, it is not a leap year. We set leap to False and return False.
  - If the year is not divisible by 100, we return True.
- If it is not, we set it to False since a leap year must be divisible by 4 and return False.

We take the year as input from the user, call the function, passing the input as a parameter, and check if the return value is true or false.

- If check_leap returns True, the year is leap and we print “It is a leap year”.
- If the check_leap returns False, the year is not leap, and we print “It is not a leap year”.

Below are a few executions of the code:

```text
Enter the year? 1992
It is a leap year
>>>
Enter the year? 1995
It is not a leap year
>>>
Enter the year? 1900
It is not a leap year
>>>

Enter the year? 2000
It is a leap year
>>>
```

As you can see from the above code and results, it accurately calculates the leap year using 3 nested IF statements.

- 1992 is a leap year since it is divisible by 4.
- 1995 is not a leap year since it is not divisible by 4.
- 1900 is not a leap year since it is divisible by both 100 and 4; but not divisible by 400.
- 2000 is a leap year since it is divisible by 4, 100 and 400.

### Exercise

- 1. Write a program that takes in as user input the number of inches of snow, number of inches of ice and the presence of salt. Check if snow day should be declared or not. It is a snow day if there is more than 15 inches of Snow. However, if there is salt, no snow day is given. If there is ice and snow together, snow day is given irrespective of whether salt is present or not.
- 2) Write a program that takes in a TV program time, TV program type and whether parents are present. Check if children can watch TV or not. Children can watch TV anytime between 6:00 pm and 7:00 pm. After 7, the rating of the tv show will have to be checked. If it’s for a general audience and before 10 pm, they can watch TV. If it’s for a mature audience before 10 pm and a parent is present, they can watch it. However, if a parent is not present, they cannot watch it. They cannot watch TV irrespective of the rating and presence of their parents after 10pm.

## A Short message from the Author:

Hey, are you enjoying the book? I’d love to hear your thoughts!

Many readers do not know how hard reviews are to come by, and how much they help an author.

![](img/443990a0ec620659ce8be783c0758bc6_452_0.png)

I would be incredibly thankful if you could take just 60 seconds to write a brief review on Amazon, even if it’s just a few sentences!

[>> Click here to leave a quick review](#)

Thank you for taking the time to share your thoughts!

Your review will genuinely make a difference for me and help gain exposure for my work.

## Loops

Loops in Python are used when we want a block of code to be repeated. We usually set conditions for the block to be repeated, as long as the condition is satisfied the block of code is repeated. As soon as the condition is no longer satisfied, the loop ends and the code block is no longer repeated.

Python has two kinds of loop:

- 1. for loop
- 2. while loop

### FOR loop

A FOR loop is used when we know the number of times, we want the loop to be executed. For loops are also used in arrays, which will be discussed in the next chapter. Below is the syntax for a for loop to repeat a block of code 10 times.

```
for i in range(0,10):
    ........ block of code ........
```

In the above piece of code, the variable ‘i’ is initially set to 0, and ‘i’ is incremented by 1 every time the block of code executes. Before executing the block of code, a check is made: if ‘i’ is less than 10, the loop is executed, if ‘i’ is greater than or equal to 10 the loop is not executed and Python starts executing the code outside of the loop. In general, the variable is initially set to the first parameter in range and is incremented by 1 every time the loop is executed until its value reaches the second parameter.

```
for i in range(0,10):
    print(i)
```

In the above code, we print the value of the variable ‘i’ during each execution of the loop. Below is the output:

```
0
1
2
3
4
5
6
7
8
9
>>>
```

After ‘i’ = 9, ‘i’ is incremented to 10 and since ‘i’ is no longer less than 10, we exit the loop.

#### Example 1

We will write a program which takes an integer as an input from the user and returns the sum of all even numbers between 0 and that number.

```python
def sum_even(number):
    number = int(number)
    sum = 0
    for i in range(0,number):
        if i%2 == 0:
            sum = sum + i
    return sum

number = input("Please input the number? ")
print(sum_even(number))
```

The function sum_even takes in a number as a parameter and returns the sum of all the even numbers up to that number, excluding the number. The following steps are performed:

- 1. We set variable ‘sum’ to 0
- 2. A loop is created which starts at ‘i’ =0 and runs till ‘i’ = number input by user with increments of 1
- 3. Inside the loop a check is performed to determine if ‘i’ is even or not
- 4. If ‘i’ is even, we update the value of ‘sum’ to the ‘sum’ + i
- 5. Once i is equal to the input number, we exit the loop and return the sum.

Below is the output when input is 10

```text
Please input the number? 10
20
>>>
```

The numbers which are even between 0 and 10 are 2,4,6,8 and 2+4+6+8 = 20.

Below is the output when input is 20

```
Please input the number? 20
90
>>>
```

The numbers which are even between 0 and 20 are 2,4,6,8,10,12,14,16,18 and 2+4+6+8+10+12+14+16+18 = 90. Therefore, our code works as expected.

#### Example 2

We will write a function which will print a $n \times n$ square filled with stars (*).

```python
def print_square(number):
    n = int(number)
    for row in range(n):
        for col in range(n):
            print("*",end='')
        print('')

number = input("Please enter the value of n:")
print_square(number)
```

The function print_square takes in a number as a parameter and prints a $n \times n$ square filled with *.

- 1. First, we need a loop to iterate through each row of the square, this iterator is called “row” and goes from 0 to n-1.
