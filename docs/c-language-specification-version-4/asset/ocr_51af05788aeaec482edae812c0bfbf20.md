```
```csharp
public int Current {
    get { return __current; }
}
object IEnumerator.Current {
    get { return __current; }
}
public bool MoveNext() {
    switch (__state) {
        case 1:
            if (from > to) goto case 2;
            __current = from++;
            __state = 1;
            return true;
        case 2:
            __state = 2;
            return false;
        default:
            throw new InvalidOperationException();
    }
}
public void Dispose() {
    __state = 2;
}
void IEnumerator.Reset() {
    throw new NotSupportedException();
}
```
```

The enumerable class implements both the enumerable interfaces and the enumerator interfaces, enabling it to serve as both an enumerable and an enumerator. The first time the GetEnumerator method is invoked, the enumerable object itself is returned. Subsequent invocations of the enumerable object's GetEnumerator, if any, return a copy of the enumerable object. Thus, each returned enumerator has its own state and changes in one enumerator will not affect another. The Interlocked.CompareExchange method is used to ensure thread-safe operation.

The from and to parameters are turned into fields in the enumerable class. Because from is modified in the iterator block, an additional __from field is introduced to hold the initial value given to from in each enumerator.

The MoveNext method throws an InvalidOperationException if it is called when __state is 0. This protects against use of the enumerable object as an enumerator object without first calling GetEnumerator.

The following example shows a simple tree class. The Tree<T> class implements its GetEnumerator method using an iterator. The iterator enumerates the elements of the tree in infix order.

```
```csharp
using System;
using System.Collections.Generic;
class Tree<T>: IEnumerable<T>
{
    T value;
    Tree<T> left;
    Tree<T> right;
    public Tree(T value, Tree<T> left, Tree<T> right) {
        this.value = value;
        this.left = left;
        this.right = right;
    }
```
```