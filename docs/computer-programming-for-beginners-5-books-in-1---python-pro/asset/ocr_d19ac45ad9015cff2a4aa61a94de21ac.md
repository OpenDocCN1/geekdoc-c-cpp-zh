'is equal to the value of it.' When you use two equals in a row, you are asking the compiler to check if a variable has a certain value recorded there. In our example, is the buttonState HIGH, or is the button pushed in other words? When this condition is true the now familiar *digitalWrite()* function is used to turn the LED on.

Next, we see an ‘else’ statement with its own curly braces. Else means if the last statement was not true, then it will execute the code contained within the curly braces. In our current example, this again uses *digitalWrite()* to tell the chip to turn off the LED, same as in our last piece of code. Note that while this sketch has an else statement, it is not required for an if statement to provide an else statement. Instead, if the condition isn’t met, it will not run that code, and it will go past it to proceed to the next instruction.

And that's it! That's all that's needed to make an LED blink at the push of a button. Alright, we've gotten some pretty simple circuits out of the way.

To follow along, open up:

File → Examples → 05.Control → WhileStatementConditional

The first part of this sketch will look quite familiar to you. We are declaring the variables we will need, initializing them, and setting the pins to the correct settings which are either input or output. Once we hit the main loop of the program, we see our very first while statement. Let's take a look at it now:

```
```cpp
while (digitalRead(buttonPin) == HIGH) {

  calibrate();

}
```
```

This statement is fairly complex so let's break it down piece by piece. First, while statements do mean something within the curly braces, as long as my condition is true. So, what is our condition first of all? If the button is being pressed. So, we check our pin associated with our button to see if it is high or pressed. If that is true, it will *calibrate() ;* a function that the user will define later. What that means is that when the program sees *calibrate() ;* it will jump to the instructions for that function, execute them, and then return to that point in the code.

Let's look at that function now since it is being called: