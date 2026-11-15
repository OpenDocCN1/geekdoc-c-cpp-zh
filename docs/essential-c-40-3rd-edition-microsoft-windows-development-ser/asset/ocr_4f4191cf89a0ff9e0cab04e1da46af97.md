```
BubbleSort(items, AlphabeticalGreaterThan);
for (i = 0; i < items.Length; i++)
{
    Console.WriteLine(items[i]);
}
}
```

# Output 12.1:

```
Enter an integer: 1
Enter an integer: 12
Enter an integer: 13
Enter an integer: 5
Enter an integer: 4
1
12
13
4
5
```

The alphabetic order is different from the numeric order. Note how simple it was to add this additional sort mechanism, however, compared to the process used at the beginning of the chapter.

The only changes to create the alphabetic sort order were the addition of the AlphabeticalGreaterThan method and then passing that method into the call to BubbleSort().

# Anonymous Methods

C# 2.0 and later include a feature known as anonymous methods. These are delegate instances with no actual method declaration. Instead, they are defined inline in the code, as shown in Listing 12.11.

# LISTING 12.11: Passing an Anonymous Method

```
class DelegateSample
{
    // ...
    static void Main(string[] args)
    {
```