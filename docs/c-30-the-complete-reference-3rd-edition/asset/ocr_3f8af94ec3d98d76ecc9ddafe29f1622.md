```
```csharp
class MyClass {
    // This iterator returns the letters
    // A, B, C, D, and E.
    public IEnumerator GetEnumerator() {
        yield return 'A';
        yield return 'B';
        yield return 'C';
        yield return 'D';
        yield return 'E';
    }
}

class ItrDemo5 {
    static void Main() {
        MyClass mc = new MyClass();

        foreach(char ch in mc)
            Console.Write(ch + " ");

        Console.WriteLine();
    }
}
```
```

The output is shown here:

A B C D E

Inside GetEnumerator(), five yield statements occur. The important thing to understand is that they are executed one at a time, in order, each time another element in the collection is obtained. Thus, each time through the foreach loop in Main(), one character is returned.

# Creating a Named Iterator

Although the preceding examples have shown the easiest way to implement an iterator, there is an alternative: the named iterator. In this approach, you create a method, operator, or accessor that returns a reference to an IEnumerable object. Your code will use this object to supply the iterator. A named iterator is a method with the following general form:

```
```csharp
public IEnumerable itr-name(param-list) {
    // ...
    yield return obj;
}
```
```

Here, *itr-name* is the name of the method, *param-list* specifies zero or more parameters that will be passed to the iterator method, and *obj* is the next object returned by the iterator. Once you have created a named iterator, you can use it anywhere that an iterator is needed. For example, you can use the named iterator to control a foreach loop.

Named iterators are very useful in some circumstances because they allow you to pass arguments to the iterator that control what elements are obtained. For example, you might pass the iterator the beginning and ending points of a range of elements to iterate. This form of iterator can also be overloaded, further adding to its flexibility. The following program