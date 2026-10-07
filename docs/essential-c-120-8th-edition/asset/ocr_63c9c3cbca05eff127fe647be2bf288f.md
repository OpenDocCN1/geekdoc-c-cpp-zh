# What Makes a Class a Collection: IEnumerable 761

![](bbox=[0.166, 0.093, 0.833, 0.442])

FIGURE 15.1: A class diagram of the IEnumerator<T> and IEnumerator interfaces

two members of the collection class, it is possible to iterate over the collection by simply using a while loop, as demonstrated in Listing 15.5. (The Reset()) method usually throws a NotImplementedException, so it should never be called. The we need to restart an enumeration, just create a fresh enumeration.)

Listing 15.5: Iterating over a Collection Using while

```
System.Collections.Generic.Stack<int> stack = new();
int number;
// ...

// This code is conceptual, not the actual code
#if ConceptualCode
while(stack.MoveNext())
    number = stack.Current;
    Console.WriteLine(number)
```