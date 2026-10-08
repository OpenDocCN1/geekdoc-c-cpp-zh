# Passing data to functions

A function has to be told values to work with. For example, in "print(a, b, c)", the function "print()" is passed the values "a", "b", and "c". In "height(1, 45)", the values 1 and 45 are being passed to the function "height".

![](bbox=[0.685, 0.075, 0.965, 0.185])

+   Add parameters to the function
Values passed to a function are called "parameters". Parameters are put inside parentheses next to the function's name in its definition.

+   Values are defined
The code inside the function uses the values that are passed to it.

"m" and "cm" are the parameters

Calls the function to get the answer when "m" = 1 and "cm" = 45

```
def height(m, cm):
    total = (100 * m) + cm
    print(total, 'cm tall')
```

```
>>> height(1, 45)
145 cm tall
```

Prints the value of "total" followed by "cm tall"

Shows that 1 m 45 cm is equal to 145 cm

Work out in the total "cm", the value of "m" needs to be multiplied by 100 (because 1 m = 100)

# Getting data back from functions

![](bbox=[0.675, 0.515, 0.965, 0.635])

Functions are most useful when they send some data back to the program—a return value. To make a function return a value, add "return" followed by the value to be sent.

+   Define a function that returns a number
Python's "input()" always returns a string, even if never is a number. The new function below gives back a number number.

+   Number as output
If the program used the function "input", "a + b" would put the strings "10" and "7" together to get "107".

```
def num_input(prompt):
    type = input(prompt)
    num = int(type)
    return num
```

```
Enter a 10
Enter b 7
a + b = 17
```

Returns the value stored in the variable

This converts the string into a number and stores it in the variable "num"

```
a = num_input('Enter a')
b = num_input('Enter b')
print('a + b =', a + b)
```

Adding "a + b" outputs "107" because the function "num_input" gives back numbers, not strings