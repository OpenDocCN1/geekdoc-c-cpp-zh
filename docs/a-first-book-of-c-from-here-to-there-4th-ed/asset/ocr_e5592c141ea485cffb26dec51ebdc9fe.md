# Point of Information

# Where to Place the Opening Braces

When the for loop contains a compound statement, professional C++ programmers use two styles of writing for loops. The style used in this book takes the following form:

```
for (expression)
{
    compound statement in here
}
```

An equally acceptable style places the compound statement's opening brace on the first line. Using this style, a for loop looks like the following:

```
for (expression) {
    compound statement in here
}
```

The advantage of the first style is that the braces line up under one another, making it easier to locate brace pairs. The advantage of the second style is that it makes the code more compact and saves a line, so more code can be viewed in the same display area. Both styles are used but are almost never intermixed. Select whichever style appeals to you and be consistent in its use. As always, the indentation you use in the compound statement (two or four spaces or a tab) should also be consistent throughout all your programs. The combination of styles you select becomes a "signature" for your programming work.

As this example shows, the only difference between the for and while statements is the placement of equivalent expressions. Grouping the initialization, expression test, and altering list in the for statement is convenient, especially when you're creating fixed-count loops. Now look at this for statement:

```
for (count = 2; count <= 20; count = count + 2)
    cout << count << " ";
```

In this statement, all the loop control information is contained in the parentheses. The loop starts with a count of 2, stops when the count exceeds 20, and increments the loop counter in steps of 2. Program 5.9 shows this for statement in an actual program. A blank space is placed between output values for readability.