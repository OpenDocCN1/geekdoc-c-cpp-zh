```
```csharp
// Display the list backward by manually walking
// from last to first.
Console.Write("Follow links backwards: ");
for (node = ll.Last; node != null; node = node.Previous)
    Console.Write(node.Value + " ");

Console.WriteLine("\n");

// Remove two elements.
Console.WriteLine("Removing 2 elements.");
// Remove elements from the linked list.
ll.Remove("C");
ll.Remove("A");

Console.WriteLine("Number of elements: " +
    ll.Count);

// Use foreach loop to display the modified list.
Console.Write("Contents after deletion: ");
foreach(char ch in ll)
    Console.Write(ch + " ");

Console.WriteLine("\n");

// Add three elements to the end of the list.
ll.AddLast("X");
ll.AddLast("Y");
ll.AddLast("Z");

Console.Write("Contents after addition to end: ");
foreach(char ch in ll)
    Console.Write(ch + " ");

Console.WriteLine("\n");
}
```
```

Here is the output:

```
```text
Initial number of elements: 0

Adding 5 elements.
Number of elements: 5
Display contents by following links: E D C B A

Display contents with foreach loop: E D C B A

Follow links backwards: A B C D E

Removing 2 elements.
Number of elements: 3
Contents after deletion: E D B

Contents after addition to end: E D B X Y Z
```
```