# Section 52.32: continue

Immediately pass control to the next iteration of the enclosing loop construct (for, foreach, do, while):

```
```csharp
for (var i = 0; i < 10; i++)
{
    if (i < 5)
    {
        continue;
    }
    Console.WriteLine(i);
}
```
```

Output:

5
6
7
8
9

Live Demo on .NET Fiddle

```
```csharp
var stuff = new [] {"a", "b", null, "c", "d"};
foreach (var s in stuff)
{
    if (s == null)
    {
        continue;
    }
    Console.WriteLine(s);
}
```
```

Output:

a
b
c
d

Live Demo on .NET Fiddle

# Section 52.33: string

string is an alias to the .NET datatype System.String, which allows text (sequences of characters) to be stored.

Notation:

```
```csharp
string a = "Hello";
var b = "world";
```
```