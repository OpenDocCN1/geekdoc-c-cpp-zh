
Again, no boxing is expected because the array is statically typed to have Int32 elements, and getting elements out of it is a statically typed operation, too, requiring no casts. Time to run all of our tests! Figure 15.13 shows my results.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_743_0.png)

FIGURE 15.13 Execution time and the number of garbage collections.

From this, you can clearly see how the ArrayList has put significant pressure on the heap due to the excessive boxing for the 10 million elements stored in it. In fact, this has triggered no less than 14 gen0 collections and even a handful of gen1 collections, which are more expensive. No wonder the performance of ArrayList is quite terrible compared to raw array accesses.

Use of generics, on the other hand, makes things much better. First, we didn't cause any more garbage collections, and performance got very close to raw arrays. Although there's still a minor performance difference compared to raw arrays, don't forget about the additional value added by generic collections (for example, the capability to dynamically expand the collection when needed).

## Operations on Type Parameters

Let's ask ourselves a quick question: Given a type parameter T, what kind of operations can we carry out over it? Because the type parameter T can be substituted for anything, our generic code can't deal with specifics of a certain type. Nevertheless, a few basic operations can be meaningfully defined.

### Default Values

One operation is to retrieve a default value for a type parameter. For a reference type, the default value is always the null reference, whereas for value types it's a value with all-zero content. This is something the CLR can meaningfully provide as an operation that makes sense for any type parameter used. In C# terms, this is realized using the default keyword:

```
int     zero = default(int);
string  @null = default(string);
T       @default = default(T); // could be null, could be all-zero
```

One place that comes to mind where this can be put to handy use is inside constructors for generic types, initializing fields of a generic parameter type. This is a bit far-fetched, though, because the default behavior is to provide all fields in their default state upon object construction (a hard guarantee made by the runtime). A better example is when we need to clear a field of generic parameter type T outside the constructor (for example, when writing a generic cache mechanism):

```
class Cache<T> {
    private bool _invalidated;
    private T _value;

    // Provide a way to recompute the value, for example, using a delegate.
    // In fact, the BCL has a similar construct called Lazy<T>.

    public void Reset() {
        _invalidated = true;
        _value = default(T);
    }
}
```

Here, we need to reset the cached value by setting the stored value back to its default value. By doing so, for a reference type, the stored object is no longer referenced and can hence be reclaimed by the garbage collector.

### WEAK REFERENCES

In fact, the framework provides a more fundamental mechanism to deal with the situation where an object is handy to have but an application can live with it being collected by the garbage collector (for example, because it can be recomputed if needed). This mechanism is called a weak reference and is exposed through a type in the BCL called (how surprising) WeakReference.

In fact, the garbage collector knows about this special type and knows to give it special treatment. Inside the WeakReference lives a System.Object-typed object that can be accessed through a Target property. A property called IsAlive can be checked to see whether the target object is still there or has been reclaimed because the garbage collector thought there was a better use of memory on the system.

For more information, take a look at the MSDN documentation on the topic.

Let's take a quick look at how the default(T) expression gets realized in IL. In essence, the initobj instruction can deal with any type specified as its operand, turning the referenced location into the type's default value. The first two nontrivial lines of the code take the address of the this._value field, which is then used as an input to initobj to zero out the contents, resulting in either a null reference or an all-zero value type. Figure 15.14 shows the inner workings of default(T).

![](img/a16f85e62ce9bdc527f4b09dbfe26092_745_0.png)

FIGURE 15.14 Default(T) relies on initobj to get its behavior.

### Getting the Type's Reflection Info Object

The other operation that's meaningfully defined on a generic parameter T is the typeof expression that gets the System.Type object describing, at runtime, the type that was supplied for the type parameter T:

```
Type t = typeof(T);
var methods = t.GetMethods();
```

Because you'll be reading a whole chapter about reflection (Chapter 21, “Reflection”), we defer further discussion about System.Type until later. Practically speaking, you should rarely have to use the typeof(T) trick.

## Generic Constraints

So far, you've learned how to declare a generic type and how to use it. Although the latter operation will be your main point of contact with the world of generics, you'll sometimes want to write your own generic type. However, up to this point, we haven't been able to do much with a generic type parameter inside the type definition. Let's take a look from an abstract point of view first. Consider the following piece of code:

```
class Foo<T> {
    public void Bar(T input) {
        // What can we do with T?
    }
}
```

The main question is what we can do with the input received as a parameter on Bar. For one thing, we can take the object and store it somewhere (for example, in a private field). That's precisely what a List<T> does, sticking the received elements in an array with element type T. For example:

```csharp
class Foo<T> {
    private T _field;

    public void Bar(T input) {
        _field = input;
    }
}
```

Similarly, we could read from a field typed as T and give the object back through some means like a method, a property, or an indexer. But maybe we also want to perform certain actions on an object of the parameter type T. Let’s see in Visual Studio what IntelliSense suggests in Figure 15.15.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_746_0.png)

FIGURE 15.15 The compiler doesn’t know about T other than it should be an object. D’oh!

What we’re seeing here is nothing more than the IntelliSense for the instance members on `System.Object`. This really makes sense because T can be substituted for everything, an int, a string, another generic type, whatever. And all of those have nothing in common except that they all derive from `System.Object` at some point.

So can’t we do anything but those operations on an object declared to be of a generic parameter? Luckily, the answer is no. By putting constraints on type parameters, we can enrich the number of operations we can perform. That sounds a little contradictory at first, so let’s examine this further. You’ll see this is nothing but a world of give and take.

Generic constraints are a way to restrict the constructed types that can be created from a generic type definition. In other words, what gets *constrained* is the use site of the generic type. As a result, the declaration site gets more *guarantees* about operations it can perform with objects typed to be of the constrained type parameter. So by *giving more guarantees* about the type parameter to the generic type using it, we’re taking away some of the flexibility as to which constructed generic types can be defined out of it.

### Interface-Based Constraints

An example is in order. Suppose we want to create a collection that can keep elements sorted. To make the collection maximally applicable, we want to declare it as a generic type. However, just creating an `OrderedList<T>` is too permissive because not every type is suitable for sorting purposes. So we want to constrain the flexibility on the type parameter
