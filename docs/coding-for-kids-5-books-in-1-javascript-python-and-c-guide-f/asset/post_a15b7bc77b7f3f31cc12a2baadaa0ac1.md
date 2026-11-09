
## The Input Function

To make a program interactive, we need to get input from the user. To take input from the user, we use the input() function. More often than not, we store the input in a variable, below is the syntax for the statement:

```python
name = input("Input your name")
```

### Example

```python
def func(color):
    print("Your favorite color is {}".format(color))

c = input("What is your favorite color? ")
func(c)
```

In the above code, we first ask the user for their favorite color and then pass the color as a parameter to the function func(). func() prints the statement “Your favorite color is ________”. Below is the output when we input our favorite color as Blue

```text
What is your favorite color? Blue
Your favorite color is Blue
>>>
```

## Exercise

- 1. Write a program in Python to take the user's name and age as input and display it on the python shell. Hint: You will need to use input(), variables and print().
- 2. Write a program in Python to take three numbers as input, calculate the sum of the three numbers and print the output. Hint: Create three variables a1, a2 and a3 and print a1+a2+a3

## Conditional Statement

Conditional Statements are also known as control statements. They help decide the flow of the program. Sometimes we want a specific block of code to execute only if a certain condition is met. Ex: We take the weather as an input from the user and print “Don’t forget your umbrella” if it’s rainy or prints “Have a nice day” if it is not.

```python
weather = input("Input the weather? ")
if weather == "rainy":
    print("Don't forget your umbrella")
else:
    print("Have a nice day")
```

If the user inputs “rainy”, print(“Don’t forget your umbrella” gets executed and python skips the code inside the else block. If the user inputs something other than “rainy”, Python skips the code inside the if block and executes the code in the else block. The general syntax is:

```python
if condition is True:
    …… execute this code block ……..
else:
    …….. execute this code block ……..
```

## Types of condition

### Boolean variable

A boolean variable can have either a value of True or False.

```python
boolean = True

if boolean:
    print("The value is True")
else:
    print("The value is False")
```

First, we declare a boolean variable called ‘boolean’ and set it True. If ‘boolean’ is True, we print “The value is True”. If it is false, we print “The value is False”. Below is the output when ‘boolean’ is set to True

```text
The value is True
>>>
```

### Comparison operators

The different type of comparison operators supported by Python are:

- `>` - greater than
- `<` - less than
- `==` - equal (Note there are two equal signs, a single equal is used to assign values to a variable, two equal signs are used for comparison)
- `!=` - not equal to
- `>=` - greater than or equal to
- `<=` - less than or equal to

Comparison can only be made between numbers or string. It is not possible to compare a number to a string. When we take input from the user, we get a string value. If the string contains only numeric characters, we can convert it to an int using int(). Conversion of data types is known as typecasting.

```python
number = int(input("Number? "))
if number > 10:
    print("{} is greater than 10".format(number))
else:
    print("{} is not greater than 10".format(number))
```

In the above code, we take an input from the user and convert it to an integer. We then compare it with 10 and print a statement. If we enter an input of 8, which is less than 10, we get the following output.

```text
Number? 8
8 is not greater than 10
>>>
```

We can also compare strings like the weather example mentioned at the beginning. Below are a few comparison examples in the Python Shell

```text
> 100 == 101
False
> 100 != 101
True
> 10 > 9
True
> 10 < 9
False
> 'a' > 'b'
False
> 'b' > 'a'
True
> 'hello' == 'hello'
True
> 'world' == 'WORLD'
False
>
```

Python is case sensitive, as it can be seen in the last example, ‘world’ != ‘WORLD’.

### Combination of conditions

Multiple conditions can be combined using the ‘and’, ‘or’ and ‘not’.

```text
>>> True and True
True
>>> True and False
False
>>> False and False
False
>>> False and True
False
>>> True or True
True
>>> True or False
True
>>> False or True
True
>>> False or False
False
>>> not True
False
>>> not False
True
```

## elif keyword

While only one of the if or else code blocks will execute, you may have a case where you want one of many code blocks to execute based on the condition. You can use the elif keyword for such a case. The elif keyword is roughly translated to “else if”.

```python
number = int(input("Number? "))

if number > 10:
    print("{} is greater than 10".format(number))
elif number > 5:
    print("{} is greater than 5".format(number))
else:
    print("{} is not greater than 5 or 10".format(number))
```

The above code is similar to the ‘number-checker’ code we had earlier, but now it also checks if the number is greater than 5. Below is the output when the user inputs 8

```text
Number? 8
8 is greater than 5
>>> |
```

## Example

- 1) A function to print the grade based on the mark input by the user

```python
def func(mark):
    mark = int(mark)
    if mark >= 90:
        print("Grade A")
    elif mark < 90 and mark >= 80:
        print("Grade B")
    elif mark < 80 and mark >= 70:
        print("Grade C")
    elif mark < 70 and mark >= 60:
        print("Grade D")
    else:
        print("Grade F")

mark = input("Enter the Mark? ")
func(mark)
```

The function ‘func’ takes a variable mark as a parameter. It checks for the following conditions:

- If ‘mark’ is greater than or equal to 90, it prints “Grade A”
- If ‘mark’ is in the range of 80 - 89 (note it’s < 90 and not <= 90), it prints “Grade B”
- If ‘mark’ is in the range of 70 - 79, it prints “Grade C”
- If ‘mark’ is in the range of 60 - 69, it prints “Grade D”
- If none of the conditions is satisfied, it prints “Grade F”

For every input, only one of the conditions is satisfied, and as a result, only one print statement is executed. Below is the output for user’s input 65

```text
Enter the Mark? 65
Grade D
>>>
```

Since 65 is between 60-69, the third elif condition is satisfied.

Below is the output for user’s input 90

```text
Enter the Mark? 90
Grade A
>>>
```

Since 90 >=90, the if condition is satisfied, and the if block is executed.

Below is the output when the user’s input is 50

```text
Enter the Mark? 50
Grade F
>>>
```

50 is not in any of the above ranges. Therefore, none of the conditions is satisfied, and the else block is executed.

## 2) A Basic Calculator

```python
def Calculator(number1, number2, operation):
    number1 = int(number1)
    number2 = int(number2)
    if operation == '+':
        return number1 + number2
    elif operation == '-':
        return number1 - number2
    else:
        return "Operator is not supported"

n1 = input("Enter the first number? ")
n2 = input("Enter the second number? ")
op = input("Enter the operator? ")

print(Calculator(n1,n2,op))
```

The above code takes two numbers and an operator as an input from the user. It returns the sum or difference based on the operator the user inputs. The following checks are performed:

- If the operator is ‘+’, we return the sum of the two numbers
- If the operator is ‘-’, we return the difference between the two numbers
- If any other operator is input, we return an error message

Below is the output when the user inputs 10, 20, +

```text
Enter the first number? 10
Enter the second number? 20
Enter the operator? +
30
```

Since the operator is ‘+’, the if condition is executed and the sum is returned.

Below is the output when the user inputs 20, 10, -

```text
Enter the first number? 20
Enter the second number? 10
Enter the operator? -
10
>>> |
```

Since the operator is ‘-’, the elif condition is executed, and the difference is returned.

Below is the output when the user inputs an invalid operator

```text
Enter the first number? 20
Enter the second number? 10
Enter the operator? /
Operator is not supported
>>> |
```

The operator ‘/’ doesn’t satisfy the if or the elif condition, therefore, the else code block is executed

## Exercise

- 1. Extend the calculator function above to support multiplication and division operators.
- 2. Write a function which takes two numbers as input from the user and returns “Yes” if number 1 is divisible by number 2 and “No” if it is not. Hint: Use the modulo operator, ‘%’. It returns the remainder of number1 divided by number2. If it returns 0, it is divisible.
