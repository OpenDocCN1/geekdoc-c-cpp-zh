The program creates a KeyedArray object ma of length 100 (that is, with 100 free elements). It continues by storing the ages of the children in The Simpsons TV show, indexed by each child’s name. Finally, the program retrieves Lisa’s age using the expression ma ["Lisa"] and displays the result. The expression ma ["Lisa"] is read as “ma sub-Lisa.”

Notice that the program has to cast the value returned from ma [] because KeyedArray is written to hold any type of object. The cast wouldn’t be necessary if the indexer were written to handle only int values — or if the KeyedArray were generic. (For more information about generics, see Chapter 8 in this minibook.)

The output of the program is simple yet elegant:

```
Let's find Lisa's age
Lisa is 10
Press Enter to terminate...
```

As an aside, the IList interface describes a class that provides an array-like integer indexer of the form object this[int]. C# also has an IList<T> interface, which you can use to replace object with your choice of type T. This would eliminate the need for a cast in the previous example.

For a generic version of the Indexer program, see the IndexerGeneric example on this book’s website.

![](bbox=[0.11, 0.48, 0.21, 0.56])

# Looping Around the Iterator Block

In previous versions of C#, the linked list we discuss in the section “Accessing Collections the Array Way: Indexes,” earlier in this chapter, was the primary practice for moving through collections, just like it was done in C++ and C before this. While that solution does work, it turns out that C# 2.0 has simplified this process so that

+   ♦ You don’t have to call GetEnumerator() (and cast the results).
♦ You don’t have to call MoveNext().
♦ You don’t have to call Current and cast its return value.
♦ You can simply use foreach to iterate the collection. (C# does the rest for you under the hood — it even writes the enumerator class.)

Well, to be fair, foreach works for the LinkedList class in.NET, too. That comes from providing a GetEnumerator() method. But I still had to write the LinkedListIterator class myself. The new wrinkle is that you can skip that part in your roll-your-own collection classes, if you choose.

Book I Chapter 7 Stepping through Collections