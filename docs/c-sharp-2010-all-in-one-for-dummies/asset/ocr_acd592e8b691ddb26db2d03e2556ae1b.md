The goto statement is unpopular for the very reason that makes it such a powerful control: It is almost completely unstructured. Tracking the flow of control through anything larger than a trivial piece of code can be difficult if you use goto. (Can you say "spaghetti code"?)

![](bbox=[0.15, 0.3, 0.26, 0.42])

Religious wars have sprung up over the use of the goto statement. In fact, the C# language itself has been criticized for its inclusion of the control. Actually, goto is neither all that horrible nor necessary. Because you can almost always avoid using goto, I recommend staying away from it, other than occasionally using it to link two cases within a switch statement, like this:

```
switch(n) // This example becomes gnarly in the logic department . . .
{
case 0:
// Do something for the 0 case, then . . .
goto 3; // jump to another case; no break statement needed.
break;
case 1:
// Do something for the 1 case.
break;
case 3: // Case 0 jumps to here after doing its thing.
// Add some case 3 stuff to what case 0 did, thus "chaining" the cases.
break;
default:
// Default case.
break;
}
```

Don't get addicted to goto, though. Really.