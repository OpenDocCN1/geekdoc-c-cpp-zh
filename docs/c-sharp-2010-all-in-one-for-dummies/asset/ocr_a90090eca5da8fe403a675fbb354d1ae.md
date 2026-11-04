# Here We Go Loop-the-Loop

The if statement enables a program to take different paths through the code being executed depending on the results of a bool expression. This statement provides for drastically more interesting programs than programs without decision-making capability. Adding the ability to execute a set of instructions repeatedly adds another quantum jump in capability.

Consider the CalculateInterest program from the section “Introducing the if statement,” earlier in this chapter. Performing this simple interest calculation by using a calculator (or by hand, using a piece of paper) would be much easier than writing and executing a program.

If you could calculate the amount of principal for each of several succeeding years, that would even more useful. A simple macro in a Microsoft Excel spreadsheet is still easier to handle, but at least you’re getting closer.

What you need is a way for the computer to execute the same short sequence of instructions multiple times — known as a loop.

# Looping for a while

The C# keyword while introduces the most basic form of execution loop:

```
while(bool-expression)
{
    // . . . repeatedly executed as long as the expression is true.
}
```

When the while loop is first encountered, the bool expression is evaluated. If the expression is true, the code within the block is executed. When the block of code reaches the closed brace, control returns to the top and the whole process starts over again. (It’s kind of the way I feel when I’m walking the dog. The dog and I loop around and around the yard until the dog . . . well, until he’s finished.) Control passes beyond the closed brace the first time the bool expression is evaluated and turns out to be false.

If the condition is not true the first time the while loop is encountered, the set of commands within the braces is never executed.

Programmers often become sloppy in their speech. (Programmers are sloppy most of the time.) If a programmer says that a loop is executed until a condition is false, it implies that control passes outside the loop — no matter where the program happens to be executing — as soon as the condition becomes false. This definitely isn’t the case. The program doesn’t check whether the condition is still true until control specifically passes back to the top of the loop.

![](bbox=[0.07, 0.7, 0.18, 0.78])

![](bbox=[0.07, 0.8, 0.18, 0.9])