```
MemoryBlock current = head;
while (current != null)
{
    if (current.IsAllocated)
    {
        current.IsAllocated = false;
        // Merge adjacent free blocks
        if (current.Next != null && !current.Next.IsAllocated)
        {
            current.Size += current.Next.Size;
            current.Next = current.Next.Next;
        }
    }
    current = current.Next;
}

public void DisplayMemory()
{
    MemoryBlock current = head;
    while (current != null)
    {
        Console.Write($"[{ (current.IsAllocated ? "X" : " ") }:{current.Size}] ");
        current = current.Next;
    }
    Console.WriteLine();
}
```
```

# Step 4: Create the Main Program

Write the `Main` method to test the memory allocator:

```
```csharp
class Program
{
    static void Main(string[] args)
```