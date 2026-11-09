
Sometimes people define a static constructor on a generic type to ensure that the type arguments will meet certain criteria. For example, if you wanted to define a generic type that can be used only with enumerated types, you could do the following:

```csharp
internal sealed class GenericTypeThatRequiresAnEnum<T> {
    static GenericTypeThatRequiresAnEnum() {
        if (!typeof(T).IsEnum) {
            throw new ArgumentException("T must be an enumerated type");
        }
    }
}
```

The CLR has a feature, called constraints, that offers a better way for you to define a generic type indicating what type arguments are valid for it. I'll discuss constraints later in this chapter. Unfortunately, constraints do not support the ability to limit a type argument to enumerated types only, which is why the previous example requires a static constructor to ensure that the type is an enumerated type.

## Generic Types and Inheritance

A generic type is a type, and as such, it can be derived from any other type. When you use a generic type and specify type arguments, you are defining a new type object in the CLR, and the new type object is derived from whatever type the generic type was derived from. In other words, since List<T> is derived from Object, List<String> and List<Guid> are also derived from Object. Similarly, since DictionaryStringKey<TValue> is derived from Dictionary<String, TValue>, DictionaryStringKey<Guid> is also derived from Dictionary<String, Guid>. Understanding that specifying type arguments doesn't have anything to do with inheritance hierarchies will help you to recognize what kind of casting you can and can't do.

For example, if a linked-list node class is defined like this:

```csharp
internal sealed class Node<T> {
    public T m_data;
    public Node<T> m_next;

    public Node(T data) : this(data, null) {
    }

    public Node(T data, Node<T> next) {
        m_data = data; m_next = next;
    }

    public override String ToString() {
        return m_data.ToString() +
            ((m_next != null) ? m_next.ToString() : String.Empty);
    }
}
```

then I can write some code to build up a linked list that would look something like this:

```csharp
private static void SameDataLinkedList() {
    Node<char> head = new Node<char>('C');
    head = new Node<char>('B', head);
    head = new Node<char>('A', head);
    Console.WriteLine(head.ToString());  // Displays "ABC"
}
```

In the Node class just shown, the m_next field must refer to another node that has the same kind of data type in its m_data field. This means the linked list must contain nodes in which all data items are of the same type (or derived type). For example, I can’t use the Node class to create a linked list in which one element contains a Char, another element contains a DateTime, and another element contains a String. Well, I could if I use Node<Object> everywhere, but then I would lose compile-time type safety, and value types would get boxed.

So a better way to go would be to define a non-generic Node base class and then define a generic TypedNode class (using the Node class as a base class). Now, I can have a linked list in which each node can be of a specific data type (not Object), get compile-time type safety and avoid the boxing of value types. Here are the new class definitions:

```csharp
internal class Node {
    protected Node m_next;

    public Node(Node next) {
        m_next = next;
    }
}

internal sealed class TypedNode<T> : Node {
    public T m_data;

    public TypedNode(T data) : this(data, null) {
    }

    public TypedNode(T data, Node next) : base(next) {
        m_data = data;
    }

    public override String ToString() {
        return m_data.ToString() +
            ((m_next != null) ? m_next.ToString() : String.Empty);
    }
}
```

I can now write code to create a linked list in which each node is a different data type. The code could look something like this:

```csharp
private static void DifferentDataLinkedList() {
    Node head = new TypedNode<Char>('A', null);
    head = new TypedNode<DateTime>(DateTime.Now, head);
    head = new TypedNode<String>("Today is ", head);
    Console.WriteLine(head.ToString());
}
```

## Generic Type Identity

Sometimes generic syntax confuses developers. After all, there can be a lot of less-than (<) and greater-than (>) signs sprinkled throughout your source code, and this hurts readability. To improve syntax, some developers define a new non-generic class type that is derived from a generic type and that specifies all of the type arguments. For example, to simplify code like this:

```csharp
List<DateTime> dtl = new List<DateTime>();
```

Some developers might first define a class like this:

```csharp
internal sealed class DateTimeList : List<DateTime> {
    // No need to put any code in here!
}
```

Now, the code that creates a list can be rewritten more simply (without less-than and greater-than signs) like this:

```csharp
DateTimeList dtl = new DateTimeList();
```

While this seems like a convenience, especially if you use the new type for parameters, local variables, and fields, you should never define a new class explicitly for the purpose of making your source code easier to read. The reason is because you lose type identity and equivalence, as you can see in the following code:

```csharp
Boolean sameType = (typeof(List<DateTime>) == typeof(DateTimeList));
```

When the code above runs, sameType will be initialized to false because you are comparing two different type objects. This also means that a method prototyped as accepting a DateTimeList will not be able to have a List<DateTime> passed to it. However, a method prototyped as accepting a List<DateTime> can have a DateTimeList passed to it since DateTimeList is derived from List<DateTime>. Programmers may become easily confused by all of this.

Fortunately, C# does offer a way to use simplified syntax to refer to a generic closed type while not affecting type equivalence at all; you can use the good old using directive at the top of your source code file. Here is an example:

```csharp
using DateTimeList = System.Collections.Generic.List<System.DateTime>;
```

Here, the using directive is really just defining a symbol called DateTimeList. As the code compiles, the compiler substitutes all occurrences of DateTimeList with System.Collections.Generic.List<System.DateTime>. This just allows developers to use a simplified syntax without affecting the actual meaning of the code, and therefore, type identity and equivalence are maintained. So now, when the following line executes, sameType will be initialized to true.

```csharp
Boolean sameType = (typeof(List<DateTime>) == typeof(DateTimeList));
```

As another convenience, you can use C#'s implicitly typed local variable feature, where the compiler infers the type of a method's local variable from the type of the expression you are assigning to it:

```csharp
using System;
using System.Collections.Generic;
...
internal sealed class SomeType {
    private static void SomeMethod() {
        // Compiler infers that dtl is of type
        // System.Collections.Generic.List<System.DateTime>
        var dtl = new List<DateTime>();

        ...
    }
}
```

## Code Explosion

When a method that uses generic type parameters is JIT-compiled, the CLR takes the method's IL, substitutes the specified type arguments, and then creates native code that is specific to that method operating on the specified data types. This is exactly what you want and is one of the main features of generics. However, there is a downside to this: the CLR keeps generating native code for every method/type combination. This is referred to as code explosion. This can end up increasing the application's working set substantially, thereby hurting performance.

Fortunately, the CLR has some optimizations built into it to reduce code explosion. First, if a method is called for a particular type argument, and later, the method is called again using the same type argument, the CLR will compile the code for this method/type combination just once. So if one assembly uses List<DateTime>, and a completely different assembly (loaded in the same AppDomain) also uses List<DateTime>, the CLR will compile the methods for List<DateTime> just once. This reduces code explosion substantially.

The CLR has another optimization: the CLR considers all reference type arguments to be identical, and so again, the code can be shared. For example, the code compiled by the CLR for List<String>'s methods can be used for List<Stream>'s methods, since String and Stream are both reference types. In fact, for any reference type, the same code will be used. The CLR can perform this optimization because all reference type arguments or variables are really just pointers (all 32 bits on a 32-bit Windows system and 64 bits on a 64-bit Windows system) to objects on the heap, and object pointers are all manipulated in the same way.

But if any type argument is a value type, the CLR must produce native code specifically for that value type. The reason is because value types can vary in size. And even if two value types are the same size (such as Int32 and UInt32, which are both 32 bits), the CLR still can't share the code because different native CPU instructions can be used to manipulate these values.
