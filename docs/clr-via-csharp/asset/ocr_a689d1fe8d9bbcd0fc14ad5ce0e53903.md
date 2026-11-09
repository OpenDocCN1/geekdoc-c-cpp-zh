I can now write code to create a linked list in which each node is a different data type. The code could look something like this:

```
~~~csharp
private static void DifferentDataLinkedList() {
    Node head = new TypedNode<Char>('.');
    head = new TypedNode<DateTime>(DateTime.Now, head);
    head = new TypedNode<String>("Today is ", head);
    Console.WriteLine(head.ToString());
}
~~~
```

# ## Generic Type Identity

Sometimes generic syntax confuses developers. After all, there can be a lot of less-than (<) and greater-than (>) signs sprinkled throughout your source code, and this hurts readability. To improve syntax, some developers define a new non-generic class type that is derived from a generic type and that specifies all of the type arguments. For example, to simplify code like this:

```
~~~csharp
List<DateTime> dtl= new List<DateTime>();
~~~
```

Some developers might first define a class like this:

```
~~~csharp
internal sealed class DateTimeList : List<DateTime> {
    // No need to put any code in here!
}
~~~
```

Now, the code that creates a list can be rewritten more simply (without less-than and greater-than signs) like this:

```
~~~csharp
DateTimeList dtl = new DateTimeList();
~~~
```

While this seems like a convenience, especially if you use the new type for parameters, local variables, and fields, you should never define a new class explicitly for the purpose of making your source code easier to read. The reason is because you lose type identity and equivalence, as you can see in the following code:

```
~~~csharp
Boolean sameType = (typeof(List<DateTime>) == typeof(DateTimeList));
~~~
```

When the code above runs, **sameType** will be initialized to **false** because you are comparing two different type objects. This also means that a method prototyped as accepting a **DateTimeList** will *not* be able to have a **List<DateTime>** passed to it. However, a method prototyped as accepting a **List<DateTime>** can have a **DateTimeList** passed to it since **DateTimeList** is derived from **List<DateTime>**. Programmers may become easily confused by all of this.