When you write a conditional statement you can use any type of variable. Let’s take the example of a program that needs to calculate the mean of multiple values that are introduced by the user. On what problem should such an application focus? We need to take the user’s input into consideration because we don’t know how many values he’ll use or whether they will be positive. The solution is simple. We need a loop that contains a so called sentinel value. A sentinel value is used to signal the application that it should break the loop when that special value is tested. The program needs to verify whether the user’s input number holds a type of value that the script should accept. For instance, while the value is positive, the loop continues iterating, however when a negative value is introduced, the program will break the loop. Here’s an example of this in code:

```
offset = 0

total = 0

x = 0

while x >= 0:
    x = int (input (“Enter a positive value: ”))
    total += x
    offset += 1

mean = total / offset

print (mean)
```

As mentioned earlier, one of the issues is not knowing the type of value inserted by the user. To solve this, we automatically convert the user’s input to an integer. If the user attempts to input a string, the program will be terminated due to a value error.

The next question regarding loops is how to quit them. There are a few methods of breaking out of a loop without causing any problems and they are with the help of the “break” and “continue” keywords. For instance, if you want to quit a loop at a certain time without going through more conditional statements you need to use “break”. However, if you want to leave just one specific iteration you can use the “continue” keyword and the loop will go over the next iteration.

In another situation you might want the program to verify the validity of a