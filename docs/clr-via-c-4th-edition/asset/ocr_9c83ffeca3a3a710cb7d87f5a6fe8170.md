+   - Widening CLR primitive value types, such as copying elements from an Int32[] to a Double[].

+   - Downcasting elements when copying between array types that can't be proven to be compatible based on the array's type, such as when casting from an Object[] to an IFormattable[]. If every object in the Object[] implements IFormattable, Copy will succeed.

Here's another example showing the usefulness of Copy.

```
// Define a value type that implements an interface.
internal struct MyValueType : IComparable {
    public Int32 CompareTo(Object obj) {
        ...
    }
}


public static class Program {
    public static void Main() {
        // Create an array of 100 value types.
        MyValueType[] src = new MyValueType[100];

        // Create an array of IComparable references.
        IComparable[] dest = new IComparable[src.Length];

        // Initialize an array of IComparable elements to refer to boxed
        // versions of elements in the source array.
        Array.Copy(src, dest, src.Length);
    }
}
```

As you might imagine, the Framework Class Library (FCL) takes advantage of Array's Copy method quite frequently.

In some situations, it is useful to cast an array from one type to another. This kind of functionality is called array covariance. When you take advantage of array covariance, you should be aware of an associated performance penalty. Let's say you have the following code.

```
String[] sa = new String[100];
Object[] oa = sa;    // oa refers to an array of String elements
oa[5] = "Jeff";      // Perf hit: CLR checks oa's element type for String; OK
oa[3] = 5;           // Perf hit: CLR checks oa's element type for Int32; throws
                     // ArrayTypeMismatchException
```

In the preceding code, the oa variable is typed as an Object[]; however, it really refers to a String[]. The compiler will allow you to write code that attempts to put a 5 into an array element because 5 is an Int32, which is derived from Object. Of course, the CLR must ensure type safety, and when assigning to an array element, the CLR must ensure that the assignment is legal. So the CLR must check at run time whether the array contains Int32 elements. In this case, it doesn't, and the assignment cannot be allowed; the CLR will throw an ArrayTypeMismatchException.