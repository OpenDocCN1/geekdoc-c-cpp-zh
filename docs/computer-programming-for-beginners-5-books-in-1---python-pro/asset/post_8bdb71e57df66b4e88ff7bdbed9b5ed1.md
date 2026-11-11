
```python
# If you don’t, you will get an error due to using mathematical operators on text
curtain_width = (float(window_width) * 0.75) + 20
print('\t', curtain_width)
curtain_length = float(window_height) + 15
print('\t\t', curtain_length)
# Next, you need to figure out the number of widths of material you need
# and calculate the length of cloth needed for every curtain.
# keep all measurements in centimeters
widths = curtain_width / roll_width
print('\t\t\t', widths)
total_length = curtain_length * widths
print('\t\t\t\t', total_length)
# Don’t forget you have two curtains.
# Double the material and divide by ten for result in meters instead of centimeters
total_length = (total_length * 2) / 10
print('\t\t\t\t', total_length)
# Now we need the price in total
price = total_length * price_per_metre
print('\t\t\t\t', price)
```

That’s it for now. Keep in mind that we used a number of tab white spaces “\t” in order to separate the variable columns and arrange our trace table. Now that we have all we need, we can put the design to the test. Here’s how the results should look:

```text
Enter the height of the window (cm): 100

Enter the width of the window (cm): 100
```

| width | height | widths | total | price |
|-------|--------|--------|-------|-------|
| 95.0 | | | | |
| | 115 | | | |
| | | 0.678571428571 | | |
| | | | 78.0357142857 | |
| | | | 15.6071428571 | |
| | | | | 78.0357142857 |

You need 15.6071428571 meters of cloth for 78.0357142857.

Now that we have our first test we can see a couple of problems. Firstly, our results are off because the conversion to meters wasn’t accurate. You should be able to easily fix this. Additionally, we have far too many decimals as we really don’t need to be that accurate with our numbers when it comes to curtains and fabric. In order to solve this minor issue, we should use the “round” function. It will take two parameters, the number from which we need to remove a number of decimal points, and the number of decimal places we want. In this case, we really don’t need more than two decimal points. Keep in mind however, that we are rounding the displayed number and not the actual calculations that are done inside the program. We don’t want to change the actual values because that may lead to other problems and more errors. Now if you perform another test with these small modifications, the result should look something like this:

You need 2.92 meters of cloth for 14.59.

We have managed to improve the results, however if we actually go to purchase these amounts of material we’ll probably end up somewhat short. For some reason, the results are smaller than they should be. In conclusion, we need to know exactly what kind of values to expect in order to confirm that the program is working properly and it’s offering accurate results. Without running tests multiple times, it’s nearly impossible to make the calculations accurate enough for them to be truly useful to someone. However, while the results of our findings are discouraging, seeing these differences between the result and the expectation can help us figure out what happened. You should take a few minutes now, go through the program, run a few more tests, and try to see what isn’t working as it should be. The application’s design requires some fine tuning, so let’s see what we can do.

## Adding the Conditionals

The next step in improving our program is to apply conditional statements. Ideally, we need to give the application the ability to measure the cloth in more than one way. For instance, if the length of the curtain is smaller than the width of the material roll, then we can flip it and simply use one width of material. But what if the curtain needs to be longer as well as wider than the fabric roll allows? Let's say we need an amount of material that is equivalent to less than half of the width of a roll. This means we'd have to buy another roll of material with the same length. However, if we need more than half we'd have to buy two additional rolls. The situations we just described are conditions that we need to code into the program. As usual, let's start putting all of these ideas into pseudo code, but this time mimicking actual Python syntax:

```text
if curtain width < roll width:
    total_length = curtain width
else:
    total_length = curtain length
```

```text
if (curtain width > roll width) and (curtain length > roll width):
    if extra material < (roll width / 2):
        width += 1
    if extra material > (roll width / 2):
        width += 2
```

The next step is to calculate how many roll widths there are in a curtain width and how much fabric we need to determine an entire width. Here's a simple way of performing the calculation:

```text
widths = int(curtain_width / roll_width)
additional_material = curtain_width % roll_width
```

All we needed was an integer function in order to cut out the decimals and then figure out how much additional material we have with the help of the modulo operator. Now you can use all of the knowledge you gained so far to stitch all these pieces together and improve your program.

Furthermore, you should consider repeating this entire process by applying different values, however you might not want to write everything manually. The purpose of programming is to make everything as smooth and efficient as possible by automating most of the tasks and by avoiding repetition. All of this can be achieved with the help of a loop, which means that a specific task is repeated and executed multiple times. In Python, as well as programming in general, there are two ways of creating a loop. You either use the “while” statement or the “for” statement.

## “While” Loops

A “while” loop will verify if a condition is true and then execute a statement for as long as that condition remains true. Here’s a simple example:

```python
x = 1

while x < 10:
    print(x)
    x += 1
```

This simple loop verifies whether x is smaller than ten. As long as this condition is true, the loop will keep being executed. During each iteration, the value of x is incremented by one. When x reaches a value of ten, the condition will no longer be met, which means the loop will stop being executed and the rest of the program will continue. On a side note, iteration is simply the repetition of a number of statements, such as those in this example.

When you construct “while” loops you need to take two things into consideration. Before the loop is executed, the variable used in the conditional statement needs to be first initialized. Furthermore, you need to make sure that the variable updates with every loop execution, otherwise you will end up creating an infinite loop. Keep in mind that infinite loops can be quite troublesome, especially because Python won’t alert you when one is created. When the program is stuck in one, you need to kill it, but depending on the complexity of the program, trying to simply close the application might not work. While they won’t damage your system or cause any such drastic issues, infinite loops should simply be avoided.

When you write a conditional statement you can use any type of variable. Let’s take the example of a program that needs to calculate the mean of multiple values that are introduced by the user. On what problem should such an application focus? We need to take the user’s input into consideration because we don’t know how many values he’ll use or whether they will be positive. The solution is simple. We need a loop that contains a so called sentinel value. A sentinel value is used to signal the application that it should break the loop when that special value is tested. The program needs to verify whether the user’s input number holds a type of value that the script should accept. For instance, while the value is positive, the loop continues iterating, however when a negative value is introduced, the program will break the loop. Here’s an example of this in code:

```python
offset = 0

total = 0

x = 0

while x >= 0:
    x = int(input("Enter a positive value: "))
    total += x
    offset += 1

mean = total / offset

print(mean)
```

As mentioned earlier, one of the issues is not knowing the type of value inserted by the user. To solve this, we automatically convert the user’s input to an integer. If the user attempts to input a string, the program will be terminated due to a value error.

The next question regarding loops is how to quit them. There are a few methods of breaking out of a loop without causing any problems and they are with the help of the “break” and “continue” keywords. For instance, if you want to quit a loop at a certain time without going through more conditional statements you need to use “break”. However, if you want to leave just one specific iteration you can use the “continue” keyword and the loop will go over the next iteration.

In another situation you might want the program to verify the validity of a
