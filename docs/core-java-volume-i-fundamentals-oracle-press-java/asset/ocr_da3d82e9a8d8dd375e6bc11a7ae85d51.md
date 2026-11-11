+   - `ArrayList<E>()`  
+     constructs an empty array list.
+   - `ArrayList<E>(int initialCapacity)`  
+     constructs an empty array list with the specified capacity.
+   - `boolean add(E obj)`  
+     appends obj at the end of the array list. Always returns true.
+   - `int size()`  
+     returns the number of elements currently stored in the array list. (Of course, this is never larger than the array list’s capacity.)
+   - `void ensureCapacity(int capacity)`  
+     ensures that the array list has the capacity to store the given number of elements without reallocating its internal storage array.
+   - `void trimToSize()`  
+     reduces the storage capacity of the array list to its current size.

# 5.3.2 Accessing Array List Elements

Unfortunately, nothing comes for free. The automatic growth convenience of array lists requires a more complicated syntax for accessing the elements. The reason is that the `ArrayList` class is not a part of the Java programming language; it is just a utility class programmed by someone and supplied in the standard library.

Instead of the pleasant `[ ]` syntax to access or change the element of an array, you use the get and set methods.

For example, to set the ith element, use

```
staff.set(i, harry);
```

This is equivalent to