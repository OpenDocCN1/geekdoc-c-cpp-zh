# CHAPTER 4: Making Decisions About...and Planning Program Flow

section until some condition is met. This is called **looping**. It enables you to repeat sections of programming logic—without rewriting those sections of code—until a condition is met.

# ## Using Loops to Repeat Program Statements

A **loop** is a sequence of program statements that is specified once, but can be repeated several times in succession. A loop can repeat a specified number of times (count-controlled) until some condition (condition-controlled) occurs.

In this section, you'll learn about count-controlled loops and condition-controlled loops. You will also learn how to control your loops with Boolean logic.

# ## Count-Controlled Loops

A count-controlled loop is a loop that repeats a specified number of times. Objective-C and Alice, this is a **for loop**. A loop has a counter variable. This variable enables the developer to specify the number of times the loop will be executed. See Listing 4–3.

**Listing 4–3.** A Count-Controlled Loop

```
int i;
for ( i = 0; i < 10; i++)
{
    //repeat all code in braces 10 times
}
continue
```

The loop in Listing 4-3 will loop 10 times. The variable i starts at zero and increments at the end of the } by one. The incrementing is done by the i++ in the **for** statement; i++, which is equivalent to i = i +1, is then incremented by 1 to 10 and then checked to if it is less than 10. For this loop will end when i = 9 and the } is reached.

> NOTE: It is common for developers to confuse the number of times they think their loops repeat. If the loop started at 1 in Listing 4–3, the loop would repeat nine times instead of 10.

In Objective-C, for loops have their counter variable declared in the loop declaration itself.

**Listing 4–4.** Counter Variable is Initialized For Loop Declaration

```
for (int i = 0; i < 10; i++)
{
    //repeat all code in braces 10 times
}
continue
```

Occasionally, you will need to repeat just one line of code in a loop. This can be accomplished by not using any {}. The first line of code encountered after the declaration is repeated, as specified in the loop declaration. See Listing 4–5.