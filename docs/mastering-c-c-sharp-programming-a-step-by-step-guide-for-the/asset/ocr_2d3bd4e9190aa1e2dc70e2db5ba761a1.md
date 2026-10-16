```
for (int i = 0; i < sizeof(double); ++i)
    Console.Write("{0:X2} ", *pb++);
    Console.WriteLine();
}
}
}
```

The output depends entirely on the ‘endianness’ or, to us mere mortals, the sequential order the bytes were arranged in numerical values when they were stored in memory.

# Pointer Arrays

We can construct pointer arrays in an unsafe context but we can only apply some of the normal array type conversions on the pointer arrays:

+   - An implicit reference conversion that goes from array_type (any) to System.Array, along with any interface that it may implement. However, if you were to try to access the elements in the array using System.Array or through an implemented interface, an exception is thrown at run time – pointer types cannot be converted to object types.
+   - Implicit and explicit reference conversions from one-dimensional arrays of type S[] to System.Collections.Generic.IList<T> and any of the generic base interfaces. These can never be applied to a pointer array because we cannot use a pointer type as a type argument and we can’t convert from a pointer type to a non-pointer type.
+   - An explicit reference conversion that goes from System.Array and any of its implemented interfaces to any of the array_types can be applied to the pointer array.
+   - Explicit reference conversions between System.Collections.Generic.IList<S> and base interfaces to one-dimensional array types of T[]. This is because we can’t