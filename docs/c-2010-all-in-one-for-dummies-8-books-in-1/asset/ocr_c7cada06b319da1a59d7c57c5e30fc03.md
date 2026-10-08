# 106 Nesting Loops

The increment operator is particularly popular when writing for loops. (I describe the increment operator along with other operators in Chapter 4 of this minibook.) The previous for loop is usually written this way:

```
for(int year = 1; year < nDuration; year++) {
    // // body of code ...
}
```

You almost always see the postincrement operator used in a for loop instead of the preincrement operator, although in this case it is the same. There's no reason other than the fact that it looks cooler.(The next time you want to break the ice, just haul your C# listing full of postincrement operators to show how cool you are. It almost never works, but it's a try.)

![](bbox=[0.153, 0.269, 0.222, 0.318])

The for loop has one variation that I can't claim to understand. If the logical condition is missing, it's assumed to be true. Thus for(;;) is an infinite loop.

You see for(;;) used as an infinite loop more often than while(true).I have no idea why that's the case.

![](bbox=[0.153, 0.448, 0.222, 0.497])

# Nesting Loops

An inner loop can appear within an outer loop, in this way:

```
for( . .some condition . .)
  for( . .some other condition . .)
    // do whatever . . .
}
```

The inner loop is executed to completion after each pass through the outer loop. The loop variable (such as year) used in the for loop isn't defined outside the inner loop's scope.

![](bbox=[0.143, 0.736, 0.229, 0.804])

A loop contained within another loop is a nested loop. Nested loops "cross." For example, the following code won't:

```
do // Start a do..while loop.
  for( . . . ) // Start some for loop.
    while( . . . ) // End do..while loop.
  // End for loop.
}
```

I'm not sure what this chunk would mean, but it doesn't matter because the compiler tells you that it's not legal anyway.