# For Loops

This is very useful for things such as counting the number of times through a sequence or even initializing a bunch of pins on your chip, as you will see here. Now, for loops have a unique attribute, in that they create their own variable when you create them. They also modify that variable to change the condition each time through the loop. Let's look at an empty for loop for a moment.

```
for (variable; condition; increment/decrement) {}
```

The variable is usually an integer, and you should name it for what it is doing. If it is going through the pins on your chip, ‘thisPin’ is a very good name, because it makes sense what it is for. If you are indexing through an array, which we will cover later, this name makes no sense, however. In that case, the variable name index might be appropriate. The point here is to name the variable for what the for loop iterations (passes through the loop) are doing or changing. Next, the conditional statement. This takes the form of a Boolean comparison. By Boolean, we mean >, <, >=, <=, ==. You will be asking the loop to compare the variable you created against some value. In our example, it is 8.

Finally, we come to the increment or decrements part of the for loop. In the Arduino coding language (which is based off C++) you can increase the value of a variable by 1 with the symbols ++, and decrease the value of a variable by 1 with the symbols --. Let's see that now in a separate case.

```
int pizzaSlices = 1// We only have one slice of pizza
```

```
pizzaSlices--// we ate a slice, and now pizzaSlices will be 0
```

```
pizzaSlices++// our friend gave us their slice; now we have 1
```

Hopefully, that will clarify how increments and decrements work. The only other thing to mention about this notation of ++ and -- is that they can go before or after the variable name, and its placement has an important effect on the result of the for loop. If the symbol is before the variable name, e.g., t ++*thisPin*, it will change the variable before executing the code in the curly braces. When the symbols go after the variable, e.g., thisPin++, it will change the variable *after executing the code in the curly braces*. Speaking of which, it is very, very important with for