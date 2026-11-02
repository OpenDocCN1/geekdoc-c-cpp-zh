# Using Java's do statement

To write the program in Listing 15-4, you need a loop — a loop that repeatedly asks the user whether the importantData.txt file should be deleted. (The action of the loop in Listing 15-4 is illustrated in Figure 15-7.) The loop continues to ask until the user gives a meaningful response. The loop tests its condition at the end of each iteration, after each of the user's responses.

![](bbox=[0.28, 0.33, 0.82, 0.72])

Figure 15-7:
Here we go loop, do loop.

That's why the program in Listing 15-4 has a do loop (also known as a do ... while loop). With a do loop, the program jumps right in, executes some statements, and then checks a condition. If the condition is true, the program goes back to the top of the loop for another go-around. If the condition is false, the computer leaves the loop (and jumps to whatever code comes immediately after the loop).

# A closer look at the do statement

The format of a do loop is

```
do {
    Statements
} while (Condition)
```