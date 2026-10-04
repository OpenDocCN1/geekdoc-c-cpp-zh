A loop contained within another loop is a nested loop. Nested loops cannot "cross." For example, the following code won’t work:

```
do                  // Start a do..while loop.
{ 
    for( . . .)       // Start some for loop.
    { 
    } while( . . .)   // End do..while loop.
}                   // End for loop.
```

I’m not even sure what this chunk would mean, but it doesn’t matter because the compiler tells you that it’s not legal anyway.

A break statement within a nested loop breaks out of the inner loop only. In the following example, the break statement exits loop B and goes back into loop A:

```
// for loop A
for( . . .some condition . . .)
{
    // for loop B
    for( . . .some other condition . . .)
    {
        // . . . do whatever . . .
        if (something is true)
        {
            break;      // Breaks out of loop B and not loop A
        }
    }
}
```

C# doesn’t have a break command that exits both loops simultaneously.

That’s not as big a limitation as it sounds. In practice, the often-complex logic contained within such nested loops is better encapsulated in a method. Executing a return from within any of the loops exits the method — thereby bailing out of all loops, no matter how nested they are. We describe methods and the return statement in Chapter 7 of this minibook.

The DisplayXWithNestedLoops example (not shown here) illustrates nesting one loop inside another to do some primitive drawing on the screen.

# Don’t goto Pieces

You can transfer control in an unstructured fashion by using the goto statement. It’s followed by one of these items:

+   ♦ A label
♦ A case in a switch statement
♦ The keyword default (the default clause of a switch statement)