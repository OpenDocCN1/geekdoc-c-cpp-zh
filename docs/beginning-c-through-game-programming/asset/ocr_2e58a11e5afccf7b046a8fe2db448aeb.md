The next loop counts from 0 to 50, by fives. The loop begins:

```
for (int i = 0; i <= 50; i += 5)
```

Here, i is initialized to 0, and the loop continues as long as i is less than or equal to 50. But notice the action statement, i += 5. This statement increases i by five each time the loop body finishes. As a result, the loop displays the values 0, 5, 10, 15, and so on. The expression i <= 50 says to execute the loop body as long as i is less than or equal to 50.

You can initialize a counter variable, create a test condition, and update the counter variable with any values you want. However, the most common thing to do is to start the counter at 0 and increment it by 1 after each loop iteration.

Finally, the caveats regarding infinite loops that you learned about while studying while loops apply equally well to for loops. Make sure you create loops that can end; otherwise, you'll have a very unhappy gamer on your hands.

# Using Empty Statements in for Loops

You can use empty statements in creating your for loop, as I did in the following loop:

```
for ( ; count < 10; )
```

I used an empty statement for the initialization and action statements. That's fine because I declared and initialized count before the loop and incremented it inside the loop body. This loop displays the same sequence of integers as the very first loop in the program. Although the loop might look odd, it's perfectly legal.

# Hint

> Different game programmers have different traditions. In the last chapter, you saw that you can create a loop that continues until it reaches an exit statement—such as a break—using while (true). Well, some programmers prefer to create these kinds of loops using a for statement that begins for (;;). Because the test expression in this loop is the empty statement, the loop will continue until it encounters some exit statement.