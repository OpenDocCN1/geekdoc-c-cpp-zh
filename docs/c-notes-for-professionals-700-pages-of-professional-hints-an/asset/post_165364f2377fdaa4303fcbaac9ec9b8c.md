
## Duplicate key when using collection initialization

```
var people = new Dictionary<string, int>
{
    {"John", 30}, {"Mary", 35}, {"Jack", 40}, {"Jack", 40}
}; // throws ArgumentException since "Jack" already exists
```

## Section 27.3: SortedSet<T>

```
// create an empty set
var mySet = new SortedSet<int>();

// add something
// note that we add 2 before we add 1
mySet.Add(2);
mySet.Add(1);

// enumerate through the set
foreach(var item in mySet)
{
    Console.WriteLine(item);
}

// output:
// 1
// 2
```

## Section 27.4: T[] (Array of T)

```
// create an array with 2 elements
var myArray = new [] { "one", "two" };

// enumerate through the array
foreach(var item in myArray)
{
    Console.WriteLine(item);
}

// output:
// one
// two

// exchange the element on the first position
// note that all collections start with the index 0
myArray[0] = "something else";

// enumerate through the array again
foreach(var item in myArray)
{
    Console.WriteLine(item);
}

// output:
// something else
// two
```

## Section 27.5: List<T>

List<T> is a list of a given type. Items can be added, inserted, removed and addressed by index.

```
using System.Collections.Generic;

var list = new List<int>() { 1, 2, 3, 4, 5 };
list.Add(6);
Console.WriteLine(list.Count); // 6
list.RemoveAt(3);
Console.WriteLine(list.Count); // 5
Console.WriteLine(list[3]); // 5
```

List<T> can be thought of as an array that you can resize. Enumerating over the collection in order is quick, as is access to individual elements via their index. To access elements based on some aspect of their value, or some other key, a Dictionary<T> will provide faster lookup.

## Section 27.6: Stack<T>

```
// Initialize a stack object of integers
var stack = new Stack<int>();

// add some data
stack.Push(3);
stack.Push(5);
stack.Push(8);

// elements are stored with "first in, last out" order.
// stack from top to bottom is: 8, 5, 3

// We can use peek to see the top element of the stack.
Console.WriteLine(stack.Peek()); // prints 8

// Pop removes the top element of the stack and returns it.
Console.WriteLine(stack.Pop()); // prints 8
Console.WriteLine(stack.Pop()); // prints 5
Console.WriteLine(stack.Pop()); // prints 3
```

## Section 27.7: LinkedList<T>

```
// initialize a LinkedList of integers
LinkedList list = new LinkedList<int>();

// add some numbers to our list.
list.AddLast(3);
list.AddLast(5);
list.AddLast(8);

// the list currently is 3, 5, 8

list.AddFirst(2);
// the list now is 2, 3, 5, 8

list.RemoveFirst();
// the list is now 3, 5, 8

list.RemoveLast();
// the list is now 3, 5
```

Note that LinkedList<T> represents the doubly linked list. So, it's simply collection of nodes and each node contains an element of type T. Each node is linked to the preceding node and the following node.

## Section 27.8: Queue

```
// Initialize a new queue of integers
var queue = new Queue<int>();

// Add some data
queue.Enqueue(6);
queue.Enqueue(4);
queue.Enqueue(9);

// Elements in a queue are stored in "first in, first out" order.
// The queue from first to last is: 6, 4, 9

// View the next element in the queue, without removing it.
Console.WriteLine(queue.Peek()); // prints 6

// Removes the first element in the queue, and returns it.
Console.WriteLine(queue.Dequeue()); // prints 6
Console.WriteLine(queue.Dequeue()); // prints 4
Console.WriteLine(queue.Dequeue()); // prints 9
```

> Thread safe heads up! Use ConcurrentQueue in multi-thread environments.

## Chapter 28: Looping

## Section 28.1: For Loop

A For Loop is great for doing things a certain amount of time. It's like a While Loop but the increment is included with the condition.

A For Loop is set up like this:

```csharp
for (Initialization; Condition; Increment)
{
    // Code
}
```

- Initialization - Makes a new local variable that can only be used in the loop.
- Condition - The loop only runs when the condition is true.
- Increment - How the variable changes every time the loop runs.

An example:

```csharp
for (int i = 0; i < 5; i++)
{
    Console.WriteLine(i);
}
```

Output:

- 0
- 1
- 2
- 3
- 4

You can also leave out spaces in the For Loop, but you have to have all semicolons for it to function.

```csharp
int input = Console.ReadLine();

for ( ; input < 10; input += 2)
{
    Console.WriteLine(input);
}
```

Output for 3:

- 3
- 5
- 7
- 9
- 11

## Section 28.2: Do - While Loop

It is similar to a while loop, except that it tests the condition at the end of the loop body. The Do - While loop executes the loop once irrespective of whether the condition is true or not.

```
int[] numbers = new int[] { 6, 7, 8, 10 };

// Sum values from the array until we get a total that's greater than 10,
// or until we run out of values.
int sum = 0;
int i = 0;
do
{
    sum += numbers[i];
    i++;
} while (sum <= 10 && i < numbers.Length);

System.Console.WriteLine(sum); // 13
```

## Section 28.3: Foreach Loop

foreach will iterate over any object of a class that implements IEnumerable (take note that IEnumerable<T> inherits from it). Such objects include some built-in ones, but not limit to: List<T>, T[] (arrays of any type), Dictionary<TKey, TValue>, as well as interfaces like IQueryable and ICollection, etc.

## syntax

```
foreach(ItemType itemVariable in enumerableObject)
    statement;
```

## remarks

- The type ItemType does not need to match the precise type of the items, it just needs to be assignable from the type of the items
- Instead of ItemType, alternatively var can be used which will infer the items type from the enumerableObject by inspecting the generic argument of the IEnumerable implementation
- The statement can be a block, a single statement or even an empty statement (;)
- If enumerableObject is not implementing IEnumerable, the code will not compile
- During each iteration the current item is cast to ItemType (even if this is not specified but compiler-inferred via var) and if the item cannot be cast an InvalidCastException will be thrown.

Consider this example:

```
var list = new List<string>();
list.Add("Ion");
list.Add("Andrei");
foreach(var name in list)
{
    Console.WriteLine("Hello " + name);
}
```

is equivalent to:

```
var list = new List<string>();
list.Add("Ion");
list.Add("Andrei");
```

```
IEnumerator enumerator;
try
{
    enumerator = list.GetEnumerator();
    while(enumerator.MoveNext())
    {
        string name = (string)enumerator.Current;
        Console.WriteLine("Hello " + name);
    }
}
finally
{
    if (enumerator != null)
        enumerator.Dispose();
}
```

## Section 28.4: Looping styles

## While

The most trivial loop type. Only drawback is there is no intrinsic clue to know where you are in the loop.

```
// loop while the condition satisfies
while(condition)
{
    // do something
}
```

## Do

Similar to while, but the condition is evaluated at the end of the loop instead of the beginning. This results in executing the loops at least once.

```
do
{
    // do something
} while(condition) // loop while the condition satisfies
```

## For

Another trivial loop style. While looping an index(i) gets increased and you can use it. It is usually used for handling arrays.

```
for ( int i = 0; i < array.Count; i++ )
{
    var currentItem = array[i];
    // do something with "currentItem"
}
```

## Foreach

Modernized way of looping through IEnumerable objects. Good thing that you don't have to think about the index of the item or the item count of the list.

```
foreach ( var item in someList )
{
    // do something with "item"
}
```

## Foreach Method

While the other styles are used for selecting or updating the elements in collections, this style is usually used for calling a method straight away for all elements in a collection.

```
list.ForEach(item => item.DoSomething());
// or
list.ForEach(item => DoSomething(item));
// or using a method group
list.ForEach(Console.WriteLine);
// using an array
Array.ForEach(myArray, Console.WriteLine);
```

It is important to note that this method is only available on List<T> instances and as a static method on Array - it is not part of Linq.

## Linq Parallel Foreach

Just like Linq Foreach, except this one does the job in a parallel manner. Meaning that all the items in the collection will run the given action at the same time, simultaneously.

```
collection.AsParallel().ForAll(item => item.DoSomething());
/// or
collection.AsParallel().ForAll(item => DoSomething(item));
```

## Section 28.5: Nested loops

```
// Print the multiplication table up to 5s
for (int i = 1; i <= 5; i++)
{
    for (int j = 1; j <= 5; j++)
    {
        int product = i * j;
        Console.WriteLine("{0} times {1} is {2}", i, j, product);
    }
}
```

## Section 28.6: continue

In addition to break, there is also the keyword continue. Instead of breaking completely the loop, it will simply skip the current iteration. It could be useful if you don't want some code to be executed if a particular value is set.

Here's a simple example:

```
for (int i = 1; i <= 10; i++)
{
    if (i < 9)
        continue;
    Console.WriteLine(i);
```
