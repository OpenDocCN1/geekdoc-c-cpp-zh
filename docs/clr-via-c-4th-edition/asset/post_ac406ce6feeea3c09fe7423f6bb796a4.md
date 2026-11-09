
To drive home the performance benefits of generics, I wrote a program that tests the performance of the generic List algorithm against the FCL's non-generic ArrayList algorithm. In fact, I tested the performance of these two algorithms by using both value type objects and reference type objects. Here is the program itself.

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Diagnostics;

public static class Program {
    public static void Main() {
        ValueTypePerfTest();
        ReferenceTypePerfTest();
    }

    private static void ValueTypePerfTest() {
        const Int32 count = 100000000;

        using (new OperationTimer("List<Int32>")) {
            List<Int32> l = new List<Int32>();
            for (Int32 n = 0; n < count; n++) {
                l.Add(n);                   // No boxing
                Int32 x = l[n];             // No unboxing
            }
            l = null;  // Make sure this gets garbage collected
        }

        using (new OperationTimer("ArrayList of Int32")) {
            ArrayList a = new ArrayList();
            for (Int32 n = 0; n < count; n++) {
                a.Add(n);                   // Boxing
                Int32 x = (Int32) a[n];     // Unboxing
            }
            a = null;  // Make sure this gets garbage collected
        }
    }

    private static void ReferenceTypePerfTest() {
        const Int32 count = 100000000;

        using (new OperationTimer("List<String>")) {
            List<String> l = new List<String>();
            for (Int32 n = 0; n < count; n++) {
                l.Add("X");                 // Reference copy
                String x = l[n];            // Reference copy
            }
            l = null;  // Make sure this gets garbage collected
        }

        using (new OperationTimer("ArrayList of String")) {
            ArrayList a = new ArrayList();
            for (Int32 n = 0; n < count; n++) {
                a.Add("X");                 // Reference copy
                String x = (String) a[n];   // Cast check & reference copy
            }
            a = null; // Make sure this gets garbage collected
        }
    }
}

// This class is useful for doing operation performance timing
internal sealed class OperationTimer : IDisposable {
    private Stopwatch m_stopwatch;
    private String m_text;
    private Int32 m_collectionCount;

    public OperationTimer(String text) {
        PrepareForOperation();

        m_text = text;
        m_collectionCount = GC.CollectionCount(0);

        // This should be the last statement in this
        // method to keep timing as accurate as possible
        m_stopwatch = Stopwatch.StartNew();
    }

    public void Dispose() {
        Console.WriteLine("{0} (GCs={1,3}) {2}", (m_stopwatch.Elapsed),
            GC.CollectionCount(0) - m_collectionCount, m_text);
    }

    private static void PrepareForOperation() {
        GC.Collect();
        GC.WaitForPendingFinalizers();
        GC.Collect();
    }
}
```

When I compile and run a release build (with optimizations turned on) of this program on my computer, I get the following output.

```
00:00:01.6246959 (GCs=  6) List<Int32>
00:00:10.8555008 (GCs=390) ArrayList of Int32
00:00:02.5427847 (GCs=  4) List<String>
00:00:02.7944831 (GCs=  7) ArrayList of String
```

The output here shows that using the generic List algorithm with the Int32 type is much faster than using the non-generic ArrayList algorithm with Int32. In fact, the difference is phenomenal: 1.6 seconds versus almost 11 seconds. That's ~7 times faster! In addition, using a value type (Int32) with ArrayList causes a lot of boxing operations to occur, which results in 390 garbage collections. Meanwhile, the List algorithm required 6 garbage collections.

The result of the test using reference types is not as momentous. Here we see that the times and number of garbage collections are about the same. So it doesn't appear that the generic List algorithm is of any benefit here. However, keep in mind that when using a generic algorithm, you also get cleaner code and compile-time type safety. So although the performance improvement is not huge, the other benefits you get when using a generic algorithm are usually an improvement.

> **Note** You do need to realize that the CLR generates native code for each method the first time the method is called for a particular data type. This will increase an application's working set size, which will hurt performance. I will talk about this more in the "Generics Infrastructure" section of this chapter.

## Generics in the Framework Class Library

Certainly, the most obvious use of generics is with collection classes, and the FCL defines several generic collection classes available for your use. Most of these classes can be found in the System.Collections.Generic namespace and the System.Collections.ObjectModel namespace. There are also thread-safe generic collection classes available in the System.Collections.Concurrent namespace. Microsoft recommends that programmers use the generic collection classes and now discourages use of the non-generic collection classes for several reasons. First, the non-generic collection classes are not generic, and so you don't get the type safety, cleaner code, and better performance that you get when you use generic collection classes. Second, the generic classes have a better object model than the non-generic classes. For example, fewer methods are virtual, resulting in better performance, and new members have been added to the generic collections to provide new functionality.

The collection classes implement many interfaces, and the objects that you place into the collections can implement interfaces that the collection classes use for operations such as sorting and searching. The FCL ships with many generic interface definitions so that the benefits of generics can be realized when working with interfaces as well. The commonly used interfaces are contained in the System.Collections.Generic namespace.

The new generic interfaces are not a replacement for the old non-generic interfaces; in many scenarios, you will have to use both. The reason is backward compatibility. For example, if the List<T> class implemented only the IList<T> interface, no code could consider a List<DateTime> object an IList.

I should also point out that the System.Array class, the base class of all array types, offers many static generic methods, such as AsReadOnly, BinarySearch, ConvertAll, Exists, Find, FindAll, FindIndex, FindLast, FindLastIndex, ForEach, IndexOf, LastIndexOf, Resize, Sort, and TrueForAll. Here are examples showing what some of these methods look like.

```csharp
public abstract class Array : ICloneable, IList, ICollection, IEnumerable,
   IStructuralComparable, IStructuralEquatable {

   public static void Sort<T>(T[] array);
   public static void Sort<T>(T[] array, IComparer<T> comparer);

   public static Int32 BinarySearch<T>(T[] array, T value);
   public static Int32 BinarySearch<T>(T[] array, T value,
      IComparer<T> comparer);
   ...
}
```

## Open and Closed Types

In various chapters throughout this book, I have discussed how the CLR creates an internal data structure for each and every type in use by an application. These data structures are called *type objects*. Well, a type with generic type parameters is still considered a type, and the CLR will create an internal type object for each of these. This applies to reference types (classes), value types (structs), interface types, and delegate types. However, a type with generic type parameters is called an *open type*, and the CLR does not allow any instance of an *open type* to be constructed (similar to how the CLR prevents an instance of an interface type from being constructed).

When code references a generic type, it can specify a set of generic type arguments. If actual data types are passed in for all of the type arguments, the type is called a *closed type*, and the CLR does allow instances of a closed type to be constructed. However, it is possible for code referencing a generic type to leave some generic type arguments unspecified. This creates a new open type object in the CLR, and instances of this type cannot be created. The following code should make this clear.

```csharp
using System;
using System.Collections.Generic;

// A partially specified open type
internal sealed class DictionaryStringKey<TValue> :
    Dictionary<String, TValue> {
}

public static class Program {
    public static void Main() {
        Object o = null;

        // Dictionary<,> is an open type having 2 type parameters
        Type t = typeof(Dictionary<,>);

        // Try to create an instance of this type (fails)
        o = CreateInstance(t);
        Console.WriteLine();

        // DictionaryStringKey<> is an open type having 1 type parameter
        t = typeof(DictionaryStringKey<>);

        // Try to create an instance of this type (fails)
        o = CreateInstance(t);
        Console.WriteLine();

        // DictionaryStringKey<Guid> is a closed type
        t = typeof(DictionaryStringKey<Guid>);

        // Try to create an instance of this type (succeeds)
        o = CreateInstance(t);

        // Prove it actually worked
        Console.WriteLine("Object type=" + o.GetType());
    }

    private static Object CreateInstance(Type t) {
```
