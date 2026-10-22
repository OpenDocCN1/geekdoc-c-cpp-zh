Larger data types are more productively implemented as reference types as an assignment to a variable of a reference type only required to write a reference, not the entire data value.

At the same time, there are three kinds of reference types:

+   1. classes
+   2. interfaces
+   3. delegates

Delegates are used to represent individual methods and are beyond the scope of this course.

Variables of a reference type do not need to refer to any data value. In this case, they store a value of null (variables of a value type cannot store null). Any attempt to access a method, property, or another member of a null or to apply an index to it will result in a NullReferenceException.

The fields of classes or structures are stored depending on whether the field is a value type or a reference type. If it is a value type, the value is directed in the field, regardless of whether that field belongs to an object allocated from the stack or the heap. If it is a reference type, it stores either null or a reference to an object allocated from the heap.

The difference between value types and reference types can be illustrated with the following code example:

```
private int[] DoSomething(int i, int j)
{
    Point a = new Point(i, j);
    Point b = a;
    a.X = i + j;
    int[] c = new int[10];
```