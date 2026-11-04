the few legitimate uses I can think of is the type switch mentioned in Chapter 6, “A Primer on Types and Objects,” the section, “Intermezzo: The Mythical Type Switch.”

```
```csharp
if ((f = item as Fruit) != null)
{
    // Do something with the juicy piece of fruit...
}
```
```

Because you already know everything about assignments, there’s no need to repeat that here.

# Pre- and Post-Increment/Decrement

The increment and decrement operators are similar to assignments with regard to their usual treatment as statements. Useful for their side effects, they’re typically used in loop constructs, as you will see later. Let’s revisit the example from Chapter 5.

```
```csharp
for (int i = 0; i < array.Length; i++)
{
    // Do something
}
```
```

In fact, in such a setting it doesn’t matter whether prefix or postfix syntax is used for those operators because the only difference lies in the value that gets returned and not in the side effect they’re causing. You’ll see both styles used interchangeably, with some (ancient) C/C++ developers slightly preferring the prefix notation for its performance benefit over the postfix one.

# The Empty Statement

To ease into the subject of statements gradually, let’s start with the most mind-blowing of all: the empty statement. Written as a simple semicolon by itself, it’s rarely useful. One of the only cases where this comes in handy is when you’re writing some kind of “message pump,” a loop that calls some processing method until it returns false to indicate no further messages are to be handled:

```
```csharp
while (ProcessMessage())
    ;
```
```

I predict most readers won’t ever have to write such a loop anymore—we’re well beyond the manual message pumping required in classic Win32—but it’s good to know about its existence in case you encounter this kind of code. In fact, you could eliminate the use of the preceding empty statement by using an empty block instead: