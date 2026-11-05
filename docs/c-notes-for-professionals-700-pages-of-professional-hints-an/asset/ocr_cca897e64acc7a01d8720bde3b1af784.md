```
// precondition code that can change the value of should_end_loop expression
if (should_end_loop)
    break;
// do something
}
```

Alternative:

```
bool endLoop = false;
for ( ; !endLoop; )
{
    // precondition code that can set endLoop flag
    if (!endLoop)
    {
        // do something
    }
}
```

Note: In nested loops and/or switch must use more than just a simple break.