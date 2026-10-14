will need to know the “old school” way of Python programming; many open-source programs are still written for Python 2.4.
If you are using Python 3.x and you want to type every example into your computer as we go along, please be aware that the print statements, as written, won’t work. They will have to be modified to use a print() function like in Listing 4.3.

# 4.3  Using the Python Command Prompt

If you write a statement that doesn’t require any “processing” by Python, it will simply return you to the prompt, awaiting your next order. The next code example shows the user assigning the value “spam” to the variable can. Python doesn’t have to do anything with this, in regards to calculations or anything, so it accepts the statement and then waits for a new statement.

Listing 4.4: Python statements

```
```
>>>can = "spam"
>>>
```


```

(By the way, Python was named after Monty Python, not the snake. Hence, much of the code you’ll find on the Internet, tutorials, and books will have references to Monty Python sketches.)

The standard Python interpreter can be used to test ideas before you put them in your code. This is a good way to hash out the logic required to make a particular function work correctly or see how a conditional loop will work. You can also use the interpreter as a simple calculator. This may sound geeky, but I often launch a Python session for use as a calculator because it’s often faster than clicking through Windows’ menus to use its calculator.

Here’s an example of the “calculator” capabilities:

Listing 4.5: Python as a calculator

```
```
>>>2+2
4
>>>4*4
16
>>>5**2  #five  squared
```


```