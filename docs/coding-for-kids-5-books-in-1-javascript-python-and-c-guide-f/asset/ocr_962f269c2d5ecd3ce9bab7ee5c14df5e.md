The numbers which are even between 0 and 10 are 2,4,6,8 and 2+4+6+8 = 20. Below is the output when input is 20

```
Please input the number? 20
90
>>>
```

The numbers which are even between 0 and 20 are 2,4,6,8,10,12,14,16,18 and 2+4+6+8+10+12+14+16+18 = 90. Therefore, our code works as expected

# Example 2

We will write a function which will print a $n \times n$ square filled with stars (*).

```
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
```

The function print_square takes in a number as a parameter and prints a $n \times n$ square filled with *.

+   1. First, we need a loop to iterate through each row of the square, this iterator is called “row” and goes from 0 to n-1.