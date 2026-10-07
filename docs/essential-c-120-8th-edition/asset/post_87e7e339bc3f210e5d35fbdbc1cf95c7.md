
## 872 Chapter 17: Building Custom Collections

```sharp
{
    if(tree != null)
    {
      // Since each element in the pair is a tree,
      // traverse the tree and yield each
      // element
      foreach(T item in tree)
      {
        yield return item;
      }
    }
}
#endregion IEnumerable<T>
#region IEnumerable Members
System.Collections.IEnumerable
    System.Collections.IEnumerable.GetEnumerator()
    {
      return GetEnumerator();
    }
#endregion
// ...
```

In Listing 17.17, the first iteration returns the root element within the binary tree. During the second iteration, you traverse the pair of subelements. If the subelement pair contains a non-null value, you traverse into that node and yield its elements. Note that foreach (T item in tree) is a recursive call to a child node.

As observed with CSharpBuiltInTypes and Pair<T>, you can now iterate over BinaryTree<T> using a foreach loop. Listing 17.18 demonstrates this process, and Output 17.6 shows the results.

# LISTING 17.18: Using foreach with BinaryTree<string>

```sharp
// JFK
var jfkFamilyTree = new BinaryTree<string>(
    "John Fitzgerald Kennedy"
{
    SubItems = new Pair<BinaryTree<string>>(
        new BinaryTree<string>("Joseph Patrick Kennedy")
    {
```

```sharp
// Grandparents (Father's side)
SubItems = new Pair<BinaryTree<string>>(
    new BinaryTree<string>("Patrick Joseph Kennedy",
    new BinaryTree<string>("Mary Augusta Hickey"))),
{
    new BinaryTree<string>("Rose Elizabeth Fitzgerald")
{
    // Grandparents (Mother's side)
    SubItems = new Pair<BinaryTree<string>>(
        new BinaryTree<string>("John Francis Fitzgerald",
        new BinaryTree<string>("Mary Josephine Hannon"))
    )
})
});
```

```sharp
foreach (string name in jfkFamilyTree)
{
    Console.WriteLine(name);
}
```

```
OUTPUT 17.6
John Fitzgerald Kennedy
Joseph Patrick Kennedy
Patrick Joseph Kennedy
Mary Augusta Hickey
Rose Elizabeth Fitzgerald
John Francis Fitzgerald
Mary Josephine Hannon
```

# ADVANCED TOPIC

### The Dangers of Recursive Iterators
The code in Listing 17.17 creates new “nested” iterators as it traverses the binary tree. As a consequence, when the value is yielded by a node, the value is yielded by the node's iterator, and then yielded by its parent's iterator, and then yielded by its parent's iterator, and so on, until it is finally yielded to the original loop by the root's iterator. A value that is $n$ levels deep must actually pass its value up to $n$ iterators. If the binary tree is relatively shallow, this is not typically a problem; however, an imbalanced binary tree can be extremely deep and expensive to iterate recursively.

# Chapter 17: Building Custom Collections

> > CONSIDER using nonrecursive algorithms when iterating over potentially deep data structures.

# ADVANCED/BEGINNER TOPIC

### struct versus class

An interesting side effect of defining Pair<T> as a struct rather than as assigned class that SubItems.First and SubItems.Second cannot be assigned directly, even if the setter were public. If you modify the setter to be public, the following code produces a compile error indicating that SubItems cannot be modified "because it is not a variable":

```csharp
jfkFamilyTree.SubItems.First =
new BinaryTree<string>(
"Joseph Patrick Kennedy");
```

The issue is that SubItems is a property of type Pair<T>, a struct. Therefore, when the property returns the value, a copy of SubItems is made, and assigning First on a copy that is promptly lost at the end of the statement would be misleading. Fortunately, the C# compiler prevents this error.

To overcome the issue, don't assign First (see the approach in Listing 17.18), use class rather than struct for Pair<T>, create a SubItems property and instead use a field, or provide properties in BinaryTree<T> that give direct access to SubItems members.

# Canceling Further Iteration: yield break

Sometimes you might want to cancel further iteration. You can do so by including an if statement so that no further statements within the code are executed. However, you can also use yield break to cause MoveNext() to return false and control return immediately to the caller and end the loop. Listing 17.19 shows an example of such a method.

# Listing 17.19: Escaping Iteration via yield break

```csharp
public System.Collections.Generic.IEnumerable<T> GetNullEnumerator()
{
    if (First == null) || (Second == null)
    {
        yield break;
    }
    yield return Second;
    yield return First;
}
```

This method cancels the iteration if either of the elements in the Pair<T> class is null.

A yield break statement is similar to placing a return statement at the top of a function when it is determined that there is no work to do. It is a way to exit from further iterations without surrounding all remaining code with an block. As such, it allows multiple exits. Use with caution, because a casual reading of the code may overlook the early exit.

# ADVANCED TOPIC

### How Iterators Work

When the C# compiler encounters an iterator, it expands the code into the appropriate code. In the generated code, the C# compiler creates a nested class to implement the IEnumerator<T> interface, with its Current property and a NextNext() method. The Current property returns a type corresponding to the return type of the iterator. In Listing 17.15 of Pair<T>, an iterator returns a type. The C# compiler examines the code within the iterator and generates roughly equivalent to what you probably would have written manually (see 17.20).

# 876 Chapter 17: Building Custom Collections

LISTING 17.20: C# Equivalent of Compiler-Generated Code for Iterators

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
// ...
public struct Pair<T> : IPair<T>, IEnumerable<T>
{
    public Pair(T first, T second)
    {
        First = first;
        Second = second;
    }

    public T First { get; }

    public T Second { get; }

    public T this[PairItem index]
    {
        get
        {
            PairItem pairItem = index;
            PairItem pairItem2 = pairItem;
            T result;
            if (pairItem2 != PairItem.First)
            {
                if (pairItem2 != PairItem.Second)
                {
                    throw new NotImplementedException(
                        string.Format(
                            "The enum {0} has not been implemented",
                            index.ToString())
                        )
                    );
                }
                result = Second;
            }
            else
            {
                result = First;
            }
            return result;
        }
    }
}

public IEnumerator<T> GetEnumerator()
{
    yield return First;
    yield return Second;
    yield break;
}

Enumerator IEnumerable.GetEnumerator()
{
    return GetEnumerator();
}
```

Because the compiler takes the yield return statement and generates classes that correspond to what you probably would have written manually, iterators in C# exhibit the same performance characteristics as classes that implement the enumerator design pattern manually. Although there is no performance improvement, the gains in programmer productivity are significant.

# ADVANCED TOPIC

### Contextual Keywords

Many C# keywords are “reserved” and cannot be used as identifiers unless preceded with an @ sign. The yield keyword is a contextual keyword, not a reserved keyword; thus, it is legal (though confusing) to declare a local variable yielded. In fact, all the keywords added to C# after version 1.0 have contextual keywords; this helps prevent accidental breakages when upgrading existing programs to use new versions of the language.

Had the C# designers choose to use yield value; instead of yield return value; as the syntax for an iterator to yield a value, a possible ambiguity would have been introduced: yield(1+2); now might be yielding a value, or it might be passing the value as an argument to a method called yield.
