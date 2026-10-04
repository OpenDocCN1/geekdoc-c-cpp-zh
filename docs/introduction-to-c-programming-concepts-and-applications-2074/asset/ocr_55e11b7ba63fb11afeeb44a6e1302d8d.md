# READINGS

a Stroustrup, *Programming Principles and Practice Using C++*, section 4.4.1.
b Lippman, Lajoie, and Moo, *C++ Primer*, sections 4.1, 4.2, and 5.3.

# Exercise 1 Solution

The overall expression is **false**.

Click here to go back to the exercise.

# Exercise 2 Solution

If you run the code, you find that even people who should have gotten a discount got a message meant for those who didn't and that everyone received the same cost, $75.50. Why did that happen?

When you get to the **else** statement, because there were no curly braces, only the first command after the **else** applied to the **else** clause. The other lines—second **cout** and setting **price** to **7.5**—will run for every situation. The fact that they're indented't matter to the computer; they need to be in curly braces if they only apply to the **else**.

This is the type of mistake that happens easily, even to experienced programmers, when people aren't careful to put curly braces around their **if** clauses.

Click here to go back to the exercise.