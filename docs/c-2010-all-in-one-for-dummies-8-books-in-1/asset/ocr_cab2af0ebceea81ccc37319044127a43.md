# 164 Looping Around Iterator Block

If you think about it, this implementation simply moves the functionality of the old custom iterator class, LinkedListIterator, into the LinkedList class itself. It's all swept under the iterator block, you may say.

Under the hood, foreach makes the necessary cast for you (assuming it's a legal cast). If you stored strings in the list, your foreach loop looks like this:

```
foreach(string s in llc) // foreach does the cast for you.
{
    Console.WriteLine(s);
}
```

For a generic version of this linked list, complete with an iterator enumerator, see the GenericLinkedListContainer example on this book's Web. (It isn't shown here.) That example demonstrates instantiating the generic LinkedList for string and then you'll get a kick out of stepping through the example in the debugger to see how works. For comparison, see the new, built-in LinkedList<T> class in the System.Collections.Generic namespace.

Leave behind the whole nongeneric collection world — except for the good old array, which of course is still quite useful and type-safe. Use generic collections. (Of course, I am not to violate this in the next section.)

# One more wrinkle

The original iterator implementation in LinkedList implemented its iterator as a separate iterator class designed as a companion to the iterator block. That setup had one feature that's missing from now versions in the preceding section: You could easily create multiple instances of the iterator object and use each one for an independent iterator of the linked list. So iterator1 may be halfway through the list when iterator2 is just starting.

But in this chapter we address that problem (although for a simpler collection, not LinkedList). IteratorBlock ticks with the separate iterator object, with intimate access to the collection's internal values. But that iterator object is implemented using an iterator block:

![](bbox=[0.147, 0.339, 0.215, 0.52])

```
// In file Program.cs:
// IteratorBlock -- Implements a separate iterator object as a
// companion to a collection class, a la LinkedList, but
// implements the actual iterator with an iterator block
using System;
using System.Collections;
namespace IteratorBlock
{
    Class Program
    
```

![](bbox=[0.147, 0.796, 0.215, 0.837])