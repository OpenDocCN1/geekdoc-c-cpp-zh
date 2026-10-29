# Loops

A loop is a MAXScript construct that lets you override the normal flow of execution. Instead of processing each line in your script once and then quitting, Max can use loops to do something several times.

For example,

```
j = 0
for i = 1 to 5 do
(
    j = j + i
)
```

This MAXScript uses two variables—i and j—but you can use any variables you want in your loops. The script sets the variable j to 0 and then uses the variable i to count from 1 to 5. Max repeats the code between the parentheses five times, and each time the variable i is incremented by 1. Inside the loop, Max adds the current value of i to j. Can you figure out what the value of j is at the end of the script? If you guessed 15, you're right. To see why, look at the value of each variable as the script is running:

| When | j | i |
|---|---|---|
| First line | 0 | 0 |
| Start of loop | 0 | 1 |
| After first loop | 1 | 1 |
| Start of second loop | 1 | 2 |
| After second loop | 3 | 2 |
| Start of third loop | 3 | 3 |
| After third loop | 6 | 3 |
| Start of fourth loop | 6 | 4 |
| After fourth loop | 10 | 4 |
| Start of fifth loop | 10 | 5 |
| After fifth loop | 15 | 5 |

A loop is also useful for processing each member of an array or collection. The following MAXScript shows one way to turn every teapot in a scene blue:

```
teapots = $teapot*      -- get the collection of teapots
for singleTeapot in teapots do
(
    singleTeapot.wirecolor = blue
)
```

You can use a for loop to create a bunch of objects for you. Try this MAXScript:

```
for i = 1 to 10 collect
(
    sphere radius:15
)
```

The collect keyword tells Max to create a collection with the results of the MAXScript in the block of code inside the parentheses. The line

```
sphere radius:15
```

tells Max to create a sphere with radius of 15, so the entire script created 10 spheres and added them to your scene. Unfortunately, Max puts them all in the same spot, so move them around a bit so you can see them: