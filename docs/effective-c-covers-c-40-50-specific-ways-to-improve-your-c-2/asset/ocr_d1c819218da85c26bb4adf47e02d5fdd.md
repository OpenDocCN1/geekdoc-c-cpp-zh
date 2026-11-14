The myType variable is still returned from the Foo3 method. But this time, instead of accessing the data inside the returned value, the object is accessed to invoke a method through a defined interface. You're accessing the MyType object not for its data contents, but for its behavior. That behavior is expressed through the IMyInterface, which can be implemented by multiple different types. For this example, MyType should be a reference type, not a value type. MyType's responsibilities revolve around its behavior, not its data members.

That simple code snippet starts to show you the distinction: Value types store values, and reference types define behavior. Now look a little deeper at how those types are stored in memory and the performance considerations related to the storage models. Consider this class:

```
```csharp
public class C
{
    private MyType a = new MyType();
    private MyType b = new MyType();

    // Remaining implementation removed.
}
```
```

```
```csharp
C cThing = new C();
```
```

How many objects are created? How big are they? It depends. If MyType is a value type, you've made one allocation. The size of that allocation is twice the size of MyType. However, if MyType is a reference type, you've made three allocations: one for the C object, which is 8 bytes (assuming 32-bit pointers), and two more for each of the MyType objects that are contained in a C object. The difference results because value types are stored inline in an object, whereas reference types are not. Each variable of a reference type holds a reference, and the storage requires extra allocation.

To drive this point home, consider this allocation:

```
```csharp
MyType[] arrayOfTypes = new MyType[100];
```
```

If MyType is a value type, one allocation of 100 times the size of a MyType object occurs. However, if MyType is a reference type, one allocation just occurred. Every element of the array is null. When you initialize each element in the array, you will have performed 101 allocations—and 101 allocations take more time than 1 allocation. Allocating a large number of