iterator yields a sequence of values of the type argument provided for T.  
If the nongeneric version of *IEnumerator* is used, the yielded values will instead be of type *object*.

To correctly implement the iterator pattern, you need to maintain some internal state to keep track of where you are while enumerating the collection. In the *BinaryTree<T>* case, you track which elements within the tree have already been enumerated and which are still to come. Iterators are transformed by the compiler into a “state machine” that keeps track of the current position and knows how to “move itself” to the next position.

The **yield** **return** statement yields a value each time an iterator encounters it; control immediately returns to the caller that requested the item. (An interesting point here is that control really does *immediately* return, unlike, ironically, the **return** statement. A **return** statement will run finally blocks along the way; **yield** **return** does not.) When the caller requests the next item, the code begins to execute immediately following the previously executed **yield** **return** statement. In Listing 17.13, you return the C# built-in data type keywords sequentially.

# **LISTING 17.13: Yielding Some C# Keywords Sequentially**

```
```
using System;
using System.Collections.Generic;

public class CSharpBuiltInTypes: IEnumerable<string>
{
    public IEnumerator<string> GetEnumerator()
    {
        yield return "object";
        yield return "byte";
        yield return "uint";
        yield return "ulong";
        yield return "float";
        yield return "char";
        yield return "bool";
        yield return "ushort";
        yield return "decimal";
        yield return "int";
        yield return "sbyte";
        yield return "short";
        yield return "long";
        yield return "void";
        yield return "double";
        yield return "string";
    }
}
```
```