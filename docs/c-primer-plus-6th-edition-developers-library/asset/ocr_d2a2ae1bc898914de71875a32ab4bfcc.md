```
time = 1.998047 when terms = 10.
time = 1.999023 when terms = 11.
time = 1.999512 when terms = 12.
time = 1.999756 when terms = 13.
time = 1.999878 when terms = 14.
time = 1.999939 when terms = 15.
```

You can see that although you keep adding more terms, the total seems to level out. Indeed, mathematicians have proven that the total approaches 2.0 as the number of terms approaches infinity, just as this program suggests. Here’s one demonstration. Suppose you let S represent the sum:

```
S = 1 + 1/2 + 1/4 + 1/8 + ...
```

Here the ellipsis mean “and so on.” Then dividing by 2 gives

```
S/2 = 1/2 + 1/4 + 1/8 + 1/16 + ...
```

Subtracting the second expression from the first gives

```
S - S/2 = 1 +1/2 -1/2 + 1/4 -1/4 +...
```

Except for the initial value of 1, each other value occurs in pairs, one positive and one negative, so those terms cancel each other, leaving

```
S/2 = 1.
```

Then, multiplying both sides by 2 gives

```
S = 2.
```

One possible moral to draw from this is that before doing an involved calculation, check to see whether mathematicians have an easier way to do it.

What about the program itself? It shows that you can use more than one comma operator in an expression. You initialized time, power_of_2, and count. After you set up the conditions for the loop, the program itself is extremely brief.

# An Exit-Condition Loop: do while

The while loop and the for loop are both entry-condition loops. The test condition is checked before each iteration of the loop, so it is possible for the statements in the loop to never execute. C also has an exit-condition loop, in which the condition is checked after each iteration of the loop, guaranteeing that statements are executed at least once. This variety is called a do while loop. Listing 6.15 shows an example.