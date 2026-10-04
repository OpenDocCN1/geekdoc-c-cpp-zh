# Point of Information

Where to Place the Opening Places

When the loop contains a compound statement, professional C++ programmers use two styles of writing for loops. The style used in this book takes the following form:

```
for (expression) {
    compound statement in here
}
```

An equally acceptable style places the compound statement's opening brace on the first line. Using this style, a for loop looks like the following:

```
for (expression) {
    compound statement in here
}
```

The advantage of the first style is that the braces lie one under another, making it easier to locate pairs. The advantage of the second style is that it makes code more compact and saves a line, so more code can be viewed in the same area. Both styles are used but are almost never mixedterm. Whichever style appeals to you and be consistent in its use. As the indentation (two or four spaces or a tab) should also be consistent throughout all your programs, the combination of styles you select becomes a “signature” for your programming work.

> Note that Program 5.10a, 5.10b, and 5.10c are all for Program 5.10, and although you might encounter them in your programming career, you shouldn't use them. Adding items other than loop control variables and their updating conditions in the for statement tends to make it confusing to read and can result in unwanted effects. Keeping the loop control structure “clean,” as in Program 5.10, is important and a good practice.

Although the initializing and altering are listed from a for statement, omitting the tested expression results in an infinite loop. For example, this statement creates an infinite loop:

```
for (count = 2 ; count = count + 1)
out << count;
```

As with the while statement, both break and continue statements can be used in a loop. A break forces an exit from the for loop, as it does in the while loop. A continue, forces control to be passed to the altering in a for statement, after which the tested expression is reevaluated. This action differs from continue's action in a while statement, where control is passed directly to reculation of the tested expression.

Figure 5.7 illustrates the internal workings of a for loop. As shown, when the for loop is completed, control is transferred to the first executable statement the loop. To avoid having illustrate every step, you can use a simplified set of flowchart symbols to describe loops. If you use the following flowchart symbol to represent a statement,