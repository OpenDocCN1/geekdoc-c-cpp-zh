
better choice in general is to return a collection instance with no items. In so doing, you avoid forcing the caller to check for null before iterating over the items in the collection. For example, given a zero-size IEnumerable<T> collection, the caller can immediately and safely use a foreach loop over the collection without concern that the generated call to GetEnumerator() will throw a NullReferenceException. Consider using the Enumerable.Empty<T>() method to easily generate an empty collection of a given type.

One of the few times to deviate from this guideline is when null is intentionally indicating something different from zero items. For example, a collection of user names for a website might be null to indicate that an up-to-date collection could not be obtained for some reason; that is semantically different from an empty collection.

## Guidelines

DO NOT represent an empty collection with a null reference.
CONSIDER using the Enumerable.Empty<T>() method instead.

## Iterators

Chapter 14 went into detail on the internals of the foreach loop. This section discusses how to use iterators to create your own implementation of the IEnumerator<T>, IEnumerable<T>, and corresponding nongeneric interfaces for custom collections. Iterators provide clean syntax for specifying how to iterate over data in collection classes, especially using the foreach loop. The iterator allows end users of a collection to navigate its internal structure without knowledge of that structure.

## ADVANCED TOPIC

## Origin of Iterators

In 1972, Barbara Liskov and a team of scientists at MIT began researching programming methodologies, focusing on user-defined data abstractions. To prove much of their work, they created a language called CLU that had a concept called “clusters” (CLU being the first three letters of this term). Clusters were predecessors to the primary data abstraction that programmers use today: objects. During their research, the team realized that although they were able to use the CLU language to abstract some data representation away from end users of their types, they consistently found themselves having to reveal the inner structure of their data to allow others to intelligently consume it. The result of their consternation was the creation of a language construct called an iterator. (The CLU language offered many insights into what would eventually be popularized as “object-oriented programming.”)

If classes want to support iteration using the foreach loop construct, they must implement the enumerator pattern. As Chapter 14 describes, in C# the foreach loop construct is expanded by the compiler into the while loop construct based on the IEnumerator<T> interface that is retrieved from the IEnumerable<T> interface.

The problem with the enumeration pattern is that it can be cumbersome to implement manually, because it must maintain all the state necessary to describe the current position in the collection. This internal state may be simple for a list collection type class; the index of the current position suffices. In contrast, for data structures that require recursive traversal, such as binary trees, the state can be quite complicated. To mitigate the challenges associated with implementing this pattern, C# 2.0 included a construct that makes it easier for a class to dictate how the foreach loop iterates over its contents.

## Defining an Iterator

Iterators are a means to implement methods of a class, and they are syntactic shortcuts for the more complex enumerator pattern. When the C# compiler encounters an iterator, it expands its contents into CIL code that implements the enumerator pattern. As such, there are no runtime dependencies for implementing iterators. Because the C# compiler handles implementation through CIL code generation, there is no real runtime performance benefit to using iterators. However, there is a substantial programmer productivity gain in choosing iterators over manual implementation of the enumerator pattern. To understand improvement, we first consider how an iterator is defined in code.

## Iterator Syntax

An iterator provides shorthand implementation of iterator interfaces, the combination of the IEnumerable<T> and IEnumerator<T> interfaces. Listing

```
public class Program
{
    static void Main()
    {
        var keywords = new CSharpBuiltInTypes();
        foreach (string keyword in keywords)
        {
            Console.WriteLine(keyword);
        }
    }
}
```

The results of Listing 16.13 appear in Output 16.5.

## OUTPUT 16.5

```
object
byte
uint
ulong
float
char
bool
ushort
decimal
int
sbyte
short
long
void
double
string
```

The output from this listing is a listing of the C# built-in types.

## Iterators and State

When GetEnumerator() is first called in a foreach statement (such as foreach (string keyword in keywords) in Listing 16.13), an iterator object is created and its state is initialized to a special “start” state that represents the fact that no code has executed in the iterator and, therefore, no values have been yielded yet. The iterator maintains its state as long as the foreach statement at the call site continues to execute. Every time the loop requests the next value, control enters the iterator and continues where it left off the previous time around the loop; the state information stored in the iterator object is used to determine where control must resume. When the foreach statement at the call site terminates, the iterator’s state is no longer saved.

![](img/25683ccec0773ba5b8794b11f2b12877_710_0.png)

## FIGURE 16.8: Sequence Diagram with yield return

It is always safe to call GetEnumerator() again; “fresh” enumerator objects will be created when necessary.

Figure 16.8 shows a high-level sequence diagram of what takes place. Remember that the MoveNext() method appears on the IEnumerator<T> interface.

In Listing 16.13, the foreach statement at the call site initiates a call to GetEnumerator() on the CSharpBuiltInTypes instance called keywords. Given the iterator instance (referenced by iterator), foreach begins each iteration with a call to MoveNext(). Within the iterator, you yield a value back to the foreach statement at the call site. After the yield return statement, the GetEnumerator() method seemingly pauses until the next MoveNext() request. Back at the loop body, the foreach statement displays the yielded value on the screen. It then loops back around and calls MoveNext() on the iterator again. Notice that the second time, control picks up at the second yield return statement. Once again, the foreach displays on the screen what CSharpBuiltInTypes yielded and starts the loop again. This process continues until there are no more yield return statements within the iterator. At that point, the foreach loop at the call site terminates because MoveNext() returns false.

## More Iterator Examples

Before you modify BinaryTree<T>, you must modify Pair<T> to support the IEnumerable<T> interface using an iterator. Listing 16.14 is an example that yields each element in Pair<T>.

## LISTING 16.14: Using yield to Implement BinaryTree<T>

```
public struct Pair<T>: IPair<T>,
    IEnumerable<T>
{
    public Pair(T first, T second) : this()
    {
        First = first;
        Second = second;
    }
    public T First { get; } // C# 6.0 Getter-only Autoproperty
    public T Second { get; } // C# 6.0 Getter-only Autoproperty

    #region IEnumerable<T>
    public IEnumerator<T> GetEnumerator()
    {
        yield return First;
        yield return Second;
    }
    #endregion IEnumerable<T>

    #region IEnumerable Members
    System.Collections.IEnumerator System.Collections.IEnumerable.GetEnumerator()
    {
        return GetEnumerator();
    }
    #endregion
}
```

In Listing 16.14, the iteration over the Pair<T> data type loops twice: first through yield return First, and then through yield return Second. Each time the yield return statement within GetEnumerator() is encountered, the state is saved and execution appears to “jump” out of the GetEnumerator()
