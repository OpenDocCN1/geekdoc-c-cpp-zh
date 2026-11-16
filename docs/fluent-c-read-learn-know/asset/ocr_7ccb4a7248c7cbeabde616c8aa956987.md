# THE FOREACH COMMAND

Back in Chapter 7 we looked at iteration commands that allow you to execute a statement block multiple times. At that time we skipped one, the foreach command, that executes a statement block once for each element in an array or other set type.

```
foreach (<type> <identifier> in <set>
{
    // do something
}
```

The foreach statement is roughly equivalent to a for statement, but much simpler, because you don't have to worry about how many elements are in the set, or index into it:

```
foreach (String currentDay in DaysOfWeek)
{
    MessageBox.Show(currentDay);
}
```

> Both of these snippets display each element of the Array in a MessageBox, but the syntax of foreach is much simpler.

```
for (Int32 x = 0; x < DaysOfWeek.Length; x++)
{
    MessageBox.Show(DaysOfWeek[x]);
}
```

PUT ON YOUR THINKING HAT
How would you write a foreach statement that did something for every element in an Array of Int32s called ValidDates?