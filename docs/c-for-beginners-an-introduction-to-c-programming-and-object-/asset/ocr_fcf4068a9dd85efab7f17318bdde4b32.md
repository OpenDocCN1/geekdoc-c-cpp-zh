```
```
<statements...>
}
}
else
{
    //This block will be executed if <condition 1> is
    false.
    if ( <condition 3> )
    {
        //This block will be executed if <condition 1>
        is false and <condition 3> is true.
        <statements...>
    }
}
```
```

There is another way of writing *if-else* decision making construct using the *else if* statement. The way *else if* construct work is – There will be a mandatory *if* statement, if the condition of the *if* statement evaluates to *false*, the control will go to the immediate *else if* statement (if it is present) and will evaluate the condition of the *else if* statement. If it evaluates to *1*, the *else if* block will be executed and the remaining *else if* and *else* blocks (if present) will be ignored; if it evaluates to *0*, the control will go to the next *else if* or *else* statements if there are any. You can have as many *else if* statements as you want. The general syntax is as follows:

```
```
if ( <condition 1>)
{
    //This block will be executed if <condition 1> is
    true.
}
else if ( <condition 2> )
```
```