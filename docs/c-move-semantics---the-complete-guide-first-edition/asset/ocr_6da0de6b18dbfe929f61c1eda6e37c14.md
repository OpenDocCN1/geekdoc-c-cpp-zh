In the program, we declare process() with a parameter as a universal reference to a collection (container, string, etc.). As usual for universal references, we can pass strings of all possible value categories.

Inside process(), we can still have different behavior depending on whether or not the argument is const. In this case, we call begin() and end() for the passed collection to pass them as a half-open range to a function that iterates over all elements:

```
    template<typename T>
    void process(T&& coll)
    {
        iterate(coll.begin(), coll.end());
    }
```

However, we have called different implementations of the function iterate(): one for iterators (able to modify the elements), and one for const_iterators (not able to modify the elements). Because universal references preserve whether a const object was passed, we call the iterate() that matches the constness of the passed collection.

Note that we do not use (perfect) forwarding inside process(). We just want to refer universally to both const and non-const objects. We might even use coll after iterating over all elements.

You might argue that we should know whether we modify elements when iterating over them. However, assume that this generic function also allows us to pass the operation we call for each element. It might read or modify the elements and for that, const correctness is important.

Note that using std::forward<>() here is at least questionable:

```
    template<typename T>
    void process(T&& coll)
    {
        iterate(std::forward<T>(coll).begin(), std::forward<T>(coll).end());  // ???
    }
```

Claiming at two different locations that the same object is no longer needed is a source of trouble because then both locations might interpret this as reason to steal the value from the object. Therefore, the location that steals last might not use the right value. You should never use std::move() or std::forward<>() twice for the same object (unless the object was reinitialized before the second use).

Using std::forward<>() only once here is also a source of trouble because we have no guaranteed evaluation order for arguments of function calls:

```
    template<typename T>
    void process(T&& coll)
    {
        iterate(coll.begin(), std::forward<T>(coll).end());  // ???
    }
```

In this particular example, using std::forward<>() once or twice might work because begin() and end() do not steal/modify the value from the passed object. However, in general, it is an error unless you know exactly how this information is used.