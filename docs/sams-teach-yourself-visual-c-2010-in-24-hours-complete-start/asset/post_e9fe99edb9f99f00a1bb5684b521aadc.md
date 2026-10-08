
## TABLE 9.8 Common Members of HashSet<T> and SortedSet<T>

| Name | Description |
| --- | --- |
| IsProperSubsetOf | Determines if the set is a proper subset of the specified collection. |
| IsProperSupersetOf | Determines if the set is a proper superset of the specified collection. |
| IsSubsetOf | Determines if the set is a subset of the specified collection. |
| IsSupersetOf | Determines if the set is a superset of the specified collection. |
| Overlaps | Determines if the set and a specified collection share common elements. |
| Remove | Removes the specified element from the set. |
| RemoveWhere | Removes all elements that match the specified conditions from the set. |
| Reverse | Returns an enumerator that iterates over the set in reverse order. (SortedSet<T> only.) |
| SetEquals | Determines if the set and a specified collection contain the same elements. |
| SymmetricExceptWith | Modifies the current set to contain only elements that are present either in the set or the specified collection, but not both. |
| TrimExcess | Sets the capacity of the set to the actual number of elements it contains, rounded up to a nearby value. (HashSet<T> only.) |
| UnionWith | Modifies the current set to contain all elements that are present in both the set and the specified collection. |

## Why HashSet<T>?

Unlike most of the other generic collections, HashSet<T> has a name that is based on its implementation details rather than its purpose. The reason is that Set is a reserved word in Visual Basic, so it could be used only by escaping it:

```vb
Dim s as [Set] of Int
```

Rather than requiring this syntax, the designers of the .NET Framework chose a name that would not conflict with any reserved words.

## Did you know?

## Try It Yourself

### Working with Sets

By following these steps, you see how to work with HashSet<T> and SortedSet<T>.

- 1. Create a new Console application.
- 2. In the **Main** method of the Program.cs file, declare two integer sets, as follows:
  ```csharp
  HashSet<int> even = new HashSet<int>() { 0, 2, 4, 6, 8, 10, 12 };
  HashSet<int> odd = new HashSet<int>() { 1, 3, 5, 7, 9, 11 };
  ```
- 3. Print the result of performing a **SetEquals** call between *even* and *odd*.
- 4. Run the application using Ctrl+F5, and observe that the output is *False*.
- 5. Calculate the union between *even* and *odd* by executing the **UnionWith** method.
- 6. Print the contents of the *even* set using a **foreach** statement.
- 7. Run the application again using Ctrl+F5, and observe that the output contains the numbers from the original *even* set and the numbers from the *odd* set.
- 8. Calculate the intersection between *even* and *odd* by executing the **IntersectWith** method.
- 9. Repeat the line of code entered from step 3.
- 10. Run the application again using Ctrl+F5 and observe that the final output matches what is shown in Figure 9.10.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_234_0.png)

- 11. Change the declarations of *even* and *odd* to use **SortedSet<int>**.
- 12. Run the application again using Ctrl+F5, and observe that the final output matches what is shown in Figure 9.11.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_235_0.png)
![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_235_1.png)

# Stacks and Queues

Stacks and queues are relatively simple collections that represent either a last-in-first-out (LIFO) collection or first-in-first-out (FIFO) collection. Even though these are simple collections, they are nevertheless very useful as well. Queues are useful for storing data in the order received for sequential processing, whereas stacks are useful for operations such as statement parsing. In general, stacks and queues are used when operations should be restricted to either the beginning or end of the list.

The Stack<T> class provides a stack implemented as an array in which operations always occur at the end of that array and can contain duplicate elements and null elements. Stack<T> provides a simple public interface, shown in Table 9.9.

## TABLE 9.9 Common Members of Stack<T>

| Name | Description |
| :-- | :-- |
| Count | Gets the number of elements contained in the stack |
| Clear | Removes all elements from the stack |
| Contains | Determines if an element is in the stack |
| Peek | Returns the element at the top of the stack without removing it |
| Pop | Removes and returns the element at the top of the stack |
| Push | Inserts an element at the top of the stack |
| TrimExcess | Sets the capacity to the actual number of elements in the stack, if that number is less than 90% of the current capacity |

## Working with Stack<T>

To implement an integer stack, follow these steps.

- 1. Create a new Console application.
- 2. In the `Main` method of the `Program.cs` file, declare an integer stack named `stack`.
- 3. Push the values 0, 2, and 4 on to the stack.
- 4. Print the current top of the stack by calling the `Peek()` method.
- 5. Push the values 6, 8, and 10 on to the stack.
- 6. Print the current top of the stack by calling the `Pop()` method and then again by calling the `Peek()` method.
- 7. Run the application using Ctrl+F5, and observe that the output matches what is shown in Figure 9.12.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_236_0.png)

The Queue<T> class provides a queue implemented as an array in which insert operations always occur at one end of the array and remove operations occur at the other. Queue<T> also allows duplicate elements and null as an element. Queue<T> provides a simple public interface, as shown in Table 9.10.

## TABLE 9.10 Common Members of Queue<T>

| Name | Description |
| :--- | :--- |
| Count | Gets the number of elements contained in the queue |
| Clear | Removes all elements from the queue |
| Contains | Determines if an element is in the queue |
| Dequeue | Removes and returns the element at the beginning of the queue |
| Enqueue | Adds an element to the end of the queue |
| Peek | Returns the element at the beginning of the queue without removing it |
| TrimExcess | Sets the capacity to the actual number of elements in the queue, if that number is less than 90% of the current capacity |

## Try It Yourself

### Working with Queue<T>

By following these steps, you implement an integer queue.

- 1. Create a new Console application.
- 2. In the `Main` method of the `Program.cs` file, declare an integer queue named `queue`.
- 3. Add the values 1, 3, and 5 to the end of the queue by calling the `Enqueue()` method.
- 4. Print the current beginning of the queue by calling the `Peek()` method.
- 5. Add the values 7, 9, and 11 to the queue.
- 6. Print the current beginning of the queue by calling the `Dequeue()` method and then again by calling the `Peek()` method.
- 7. Run the application using Ctrl+F5, and observe that the output matches what is shown in Figure 9.13.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_237_0.png)

**FIGURE 9.13** Results of working with Queue<T>

# Collection Initializers

Just as arrays provide array initialization syntax and objects provide object initialization syntax, collections also provide collection initialization syntax, in the form of a **collection initializer**. If you look back through the exercises for this hour, you can notice the use of collection initializers already.

Collection initializers enable you to specify one or more element initializers, which enable you to initialize a collection that implements IEnumerable. Using a collection initializer enables you to omit multiple calls to the Add method of the collection, instead letting the compiler add the calls for you. An element initializer can be a value, an expression, or an object initializer.

> **Collection Initializers Work Only with Add Methods**
> Collection initializers can be used only with collections that contain an Add method. This means they cannot be used for collections such as Stack<T> and Queue<T>.

The syntax for a collection initializer is similar to an array initializer. You must still call the new operator but can then use the array initialization syntax to populate the collection. Listing 9.3 shows the same example as Listing 9.2, but uses List<int> and a collection initializer.

## LISTING 9.3 Collection Initialization

```csharp
class Program
{
    static void Main()
    {
        List<int> list = new List<int>() { 0, 2, 4, 6, 8 };
    }
}
```

Collection initializers can also be more complex, enabling you to use object initializers for the element initializers, as shown in Listing 9.4.

## LISTING 9.4 Complex Collection Initialization

```csharp
class Program
{
    static void Main()
    {
        List<Contact> list = new List<Contact>()
        {
            new Contact() { FirstName = "Scott", LastName = "Dorman" },
            new Contact() { FirstName = "Jim", LastName = "Morrison" },
            new Contact() { FirstName = "Ray", LastName = "Manzarek" }
        };
        
        foreach(Contact c in list)
        {
            Console.WriteLine(c);
        }
    }
}
```
