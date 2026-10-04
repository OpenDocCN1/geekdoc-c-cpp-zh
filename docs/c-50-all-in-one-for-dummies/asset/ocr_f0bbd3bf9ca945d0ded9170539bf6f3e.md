Beyond any sort of song-and-dance justification that I may make, the most important reason to understand the for loop is that it’s the loop everyone uses — and it (along with its cousin, foreach) is the one you see 90 percent of the time when you’re reading other people’s code.

![](bbox=[0.13, 0.28, 0.22, 0.42])

The for loop is designed so that the first expression initializes a counting variable and the last section increments it; however, the C# language doesn’t enforce any such rule. You can do anything you want in these two sections — however, you would be ill advised to do anything but initialize and increment the counting variable.

The increment operator is particularly popular when writing for loops. (I describe the increment operator along with other operators in Chapter 4 of this minibook.) The previous for loop is usually written this way:

```
for(int year = 1; year < nDuration; year++)
{
    // . . . body of code . . .
}
```

![](bbox=[0.13, 0.55, 0.22, 0.65])

You almost always see the postincrement operator used in a for loop instead of the preincrement operator, although the effect in this case is the same. There’s no reason other than habit and the fact that it looks cooler. (The next time you want to break the ice, just haul out your C# listing full of postincrement operators to show how cool you are. It almost never works, but it’s worth a try.)

The for loop has one variation that I can’t claim to understand. If the logical condition expression is missing, it’s assumed to be true. Thus for( ; ) is an infinite loop.

![](bbox=[0.13, 0.71, 0.22, 0.81])

You see for( ; ) used as an infinite loop more often than while(true). I have no idea why that’s the case.

# Nesting Loops

An inner loop can appear within an outer loop, this way:

```
for( . . .some condition . . . )
{
    for( . . .some other condition . . . )
    {
        // . . . do whatever . . .
    }
}
```

The inner loop is executed to completion after each pass through the outer loop. The loop variable (such as year) used in the inner for loop isn’t defined outside the inner loop’s scope.