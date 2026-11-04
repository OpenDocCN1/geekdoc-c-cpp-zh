To add items into the stack, use the Push() method. The following statements push four strings into the tasks stack:

```
tasks.Push("Do homework"); //---this item will be at the bottom of the stack
tasks.Push("Phone rings");
tasks.Push("Get changed");
tasks.Push("Go for movies"); //---this item will be at the top of the stack
```

To retrieve the elements from a stack, use either the Peek() method or the Pop() method. Peek() returns the object at the top of the stack without removing it. Pop() removes and returns the object at the top of the stack:

```
Console.WriteLine(tasks.Peek()); //---Go for movies---
Console.WriteLine(tasks.Pop()); //---Go for movies---
Console.WriteLine(tasks.Pop()); //---Get changed---
Console.WriteLine(tasks.Pop()); //---Phone rings---
Console.WriteLine(tasks.Pop()); //---Do homework---
```

If a stack is empty and you try to call the Pop() method, an InvalidOperationException error occurs. For that reason, it is useful to check the size of the stack by using the Count property before you perform a Pop() operation:

```
if (tasks.Count > 0)
    Console.WriteLine(tasks.Pop());
else
    Console.WriteLine("Tasks is empty");
```

To extract all the objects within a Stack object without removing the elements, use a foreach statement, like this:

```
foreach (string t in tasks)
    Console.WriteLine(t);
```

Here's what prints out:
Go for movies
Get changed
Phone rings
Do homework

# Queues

The queue is a first in, first out (FIFO) data structure. Unlike the stack, items are removed based on the sequence that they are added.

In .NET, you can use the Queue class (or the generic equivalent of Queue<T>) to represent a queue collection. The following statement creates an instance of the Queue class of type string:

```
Queue<string> tasks = new Queue<string>();
```