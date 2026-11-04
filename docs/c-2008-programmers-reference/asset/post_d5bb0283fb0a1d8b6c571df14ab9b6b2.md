
## Part I: C# Fundamentals

To call this static generic method, you can either explicitly specify the type or use generic type inference:

```csharp
SomeClass.DoSomething(3);
//---or---
SomeClass.DoSomething<int>(3);
```

### Generic Operators

Generics can also be applied to operators. Consider the generic MyStack class discussed earlier in this chapter. Suppose that you want to be able to join two MyStack objects together, like this:

```csharp
MyStack<string> stack1 = new MyStack<string>(4);
stack1.Push('A');
stack1.Push('B');

MyStack<string> stack2 = new MyStack<string>(2);
stack2.Push('C');
stack2.Push('D');
```

```csharp
stack1 += stack2;
```

In this case, you can overload the + operator, as highlighted in the following code:

```csharp
public class MyStack<T> where T : IComparable<T>
{
    private T[] _elements;
    private int _pointer;

    public MyStack(int size)
    {
        _elements = new T[size];
        _pointer = 0;
    }

    public void Push(T item)
    {
        if (_pointer > _elements.Length - 1)
        {
            throw new Exception("Stack is full.");
        }
        _elements[_pointer] = item;
        _pointer++;
    }

    public T Pop()
    {
        _pointer--;
        if (_pointer < 0)
        {
            return default(T);
        }
        return _elements[_pointer];
    }

    public bool Find(T keyword)
    {
        bool found = false;
        for (int i = 0; i < _pointer; i++)
        {
            if (_elements[i].CompareTo(keyword) == 0)
            {
                found = true;
                break;
            }
        }
        return found;
    }

    public bool Empty
    {
        get
        {
            return (_pointer <= 0);
        }
    }

    public static MyStack<T> operator +
        (MyStack<T> stackA, MyStack<T> stackB)
    {
        while (!stackB.Empty)
        {
            T item = stackB.Pop();
            stackA.Push(item);
        }
        return stackA;
    }
}
```

The + operator takes in two operands — the generic *MyStack* objects. Internally, you pop out each element from the second stack and push it into the first stack. The *Empty* property allows you to know if a stack is empty.

To print out the elements of *stack1* after the joining, use the following statements:

```csharp
stack1 += stack2;
while (!stack1.Empty)
    Console.WriteLine(stack1.Pop());
```

Here’s the output:

```
C
D
B
A
```

### Generic Delegates

You can also use generics on delegates. The following class definition contains a generic delegate, MethodDelegate:

```csharp
public class SomeClass<T>
{
    public delegate void MethodDelegate(T t);
    public void DoSomething(T t)
    {
    }
}
```

When you specify the type for the class, you also need to specify it for the delegate:

```csharp
SomeClass<int> sc = new SomeClass<int>();
SomeClass<int>.MethodDelegate del;
del = new SomeClass<int>.MethodDelegate(sc.DoSomething);
```

You can make direct assignment to the delegate using a feature known as delegate inferencing, as the following code shows:

```csharp
del = sc.DoSomething;
```

### Generics and the .NET Framework Class Library

The .NET Framework class library contains a number of generic classes that enable users to create strongly typed collections. These classes are grouped under the System.Collections.Generic namespace (the nongeneric versions of the classes are contained within the System.Collections namespace). The following tables show the various classes, structures, and interfaces contained within this namespace.

The following table provides a look at the classes contained within the System.Collections.Generic namespace.

| Class | Description |
|---|---|
| `Comparer<T>` | Provides a base class for implementations of the `IComparer<T>` generic interface. |
| `Dictionary<TKey, TValue>` | Represents a collection of keys and values. |
| `Dictionary<TKey, TValue>.KeyCollection` | Represents the collection of keys in a `Dictionary<TKey, TValue>`. This class cannot be inherited. |
| `Dictionary<TKey, TValue>.ValueCollection` | Represents the collection of values in a `Dictionary<TKey, TValue>`. This class cannot be inherited. |
| `EqualityComparer<T>` | Provides a base class for implementations of the `IEqualityComparer<T>` generic interface. |
| `HashSet<T>` | Represents a set of values. |
| `KeyedByTypeCollection<TItem>` | Provides a collection whose items are types that serve as keys. |
| `KeyNotFoundException` | The exception that is thrown when the key specified for accessing an element in a collection does not match any key in the collection. |
| `LinkedList<T>` | Represents a doubly linked list. |
| `LinkedListNode<T>` | Represents a node in a `LinkedList<T>`. This class cannot be inherited. |
| `List<T>` | Represents a strongly typed list of objects that can be accessed by index. Provides methods to search, sort, and manipulate lists. |
| `Queue<T>` | Represents a first-in, first-out collection of objects. |
| `SortedDictionary<TKey, TValue>` | Represents a collection of key/value pairs that are sorted on the key. |
| `SortedDictionary<TKey, TValue>.KeyCollection` | Represents the collection of keys in a `SortedDictionary<TKey, TValue>`. This class cannot be inherited. |
| `SortedDictionary<TKey, TValue>.ValueCollection` | Represents the collection of values in a `SortedDictionary<TKey, TValue>`. This class cannot be inherited. |
| `SortedList<TKey, TValue>` | Represents a collection of key/value pairs that are sorted by key based on the associated `IComparer<T>` implementation. |
| `Stack<T>` | Represents a variable size last-in, first-out (LIFO) collection of instances of the same arbitrary type. |
| `SynchronizedCollection<T>` | Provides a thread-safe collection that contains objects of a type specified by the generic parameter as elements. |
| `SynchronizedKeyedCollection<K, T>` | Provides a thread-safe collection that contains objects of a type specified by a generic parameter and that are grouped by keys. |
| `SynchronizedReadOnlyCollection<T>` | Provides a thread-safe, read-only collection that contains objects of a type specified by the generic parameter as elements. |

The structures contained within the System.Collections.Generic namespace are described in the following table.

| Structure | Description |
|---|---|
| `Dictionary<TKey, TValue>.Enumerator` | Enumerates the elements of a `Dictionary<TKey, TValue>` |
| `Dictionary<TKey, TValue>.KeyCollection.Enumerator` | Enumerates the elements of a `Dictionary<TKey, TValue>.KeyCollection` |
| `Dictionary<TKey, TValue>.ValueCollection.Enumerator` | Enumerates the elements of a `Dictionary<TKey, TValue>.ValueCollection` |
| `HashSet<T>.Enumerator` | Enumerates the elements of a `HashSet<T>` object |
| `KeyValuePair<TKey, TValue>` | Defines a key/value pair that can be set or retrieved |
| `LinkedList<T>.Enumerator` | Enumerates the elements of a `LinkedList<T>` |
| `List<T>.Enumerator` | Enumerates the elements of a `List<T>` |
| `Queue<T>.Enumerator` | Enumerates the elements of a `Queue<T>` |
| `SortedDictionary<TKey, TValue>.Enumerator` | Enumerates the elements of a `SortedDictionary<TKey, TValue>` |
| `SortedDictionary<TKey, TValue>.KeyCollection.Enumerator` | Enumerates the elements of a `SortedDictionary<TKey, TValue>.KeyCollection` |
| `SortedDictionary<TKey, TValue>.ValueCollection.Enumerator` | Enumerates the elements of a `SortedDictionary<TKey, TValue>.ValueCollection` |
| `Stack<T>.Enumerator` | Enumerates the elements of a `Stack<T>` |

Following are descriptions of the interfaces contained within the System.Collections.Generic namespace.

| Interface | Description |
|---|---|
| `ICollection<T>` | Defines methods to manipulate generic collections |
| `IComparer<T>` | Defines a method that a type implements to compare two objects |
| `IDictionary<TKey, TValue>` | Represents a generic collection of key/value pairs |
| `IEnumerable<T>` | Exposes the enumerator, which supports a simple iteration over a collection of a specified type |
| `IEnumerator<T>` | Supports a simple iteration over a generic collection |
| `IEqualityComparer<T>` | Defines methods to support the comparison of objects for equality |
| `IList<T>` | Represents a collection of objects that can be individually accessed by index |

Prior to .NET 2.0, all the data structures contained in the System.Collections namespace are object-based. With .NET 2.0, Microsoft has released generic equivalents of some of these classes. The following table shows the mapping of these classes in the two namespaces.

| System.Collections | System.Collections.Generic |
|---|---|
| Comparer | Comparer<T> |
| HashTable | Dictionary<K, T> |
| - | LinkedList<T> |
| ArrayList | List<T> |
| Queue | Queue<T> |
| SortedList | SortedDictionary<K, T> |
| Stack | Stack<T> |
| ICollection | ICollection<T> |
| System.IComparable | IComparable<T> |
| IDictionary | IDictionary<K, T> |
| IEnumerable | IEnumerable<T> |
| IEnumerator | IEnumerator<T> |
| IList | IList<T> |
