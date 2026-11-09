Sometimes people define a static constructor on a generic type to ensure that the type arguments will meet certain criteria. For example, if you wanted to define a generic type that can be used only with enumerated types, you could do the following:

```
~~~csharp
internal sealed class GenericTypeThatRequiresAnEnum<T> {
    static GenericTypeThatRequiresAnEnum() {
        if (!typeof(T).IsEnum) {
            throw new ArgumentException("T must be an enumerated type");
        }
    }
}
~~~
```

The CLR has a feature, called constraints, that offers a better way for you to define a generic type indicating what type arguments are valid for it. I'll discuss constraints later in this chapter. Unfortunately, constraints do not support the ability to limit a type argument to enumerated types only, which is why the previous example requires a static constructor to ensure that the type is an enumerated type.

# ## Generic Types and Inheritance

A generic type is a type, and as such, it can be derived from any other type. When you use a generic type and specify type arguments, you are defining a new type object in the CLR, and the new type object is derived from whatever type the generic type was derived from. In other words, since List<T> is derived from Object, List<String> and List<Guid> are also derived from Object. Similarly, since DictionaryStringKey<TValue> is derived from Dictionary<String, TValue>, DictionaryStringKey<Guid> is also derived from Dictionary<String, Guid>. Understanding that specifying type arguments doesn't have anything to do with inheritance hierarchies will help you to recognize what kind of casting you can and can't do.

For example, if a linked-list node class is defined like this:

```
~~~csharp
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
~~~
```

then I can write some code to build up a linked list that would look something like this: