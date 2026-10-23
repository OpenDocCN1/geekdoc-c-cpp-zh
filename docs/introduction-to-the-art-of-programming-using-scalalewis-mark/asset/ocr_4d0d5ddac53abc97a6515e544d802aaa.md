It is much like a `Semaphore` with only one permit. The main concrete subclass is called `ReentrantLock`, which you can make by calling `new ReentrantLock`.

# 21.4   Parallel Collections

Even working with the concurrency library, parallelism can be hard to do well. For this reason, beginning with version 2.9, Scala has added another layer in the form of parallel collections. These are collections that have their basic operations performed in parallel. Not only do they do their operations in parallel, they have been written in such a way that they will automatically load balance. If one thread finishes its own work load, it will steal work from another thread that has not yet finished. For this reason, if your problem can be solved using parallel collections, you should probably use them. Not only will they be easier to write, they will probably be more efficient than anything you are going to take the time to write yourself.

The structure of the parallel collections largely mirrors the structure of the normal collections with a `scala.collection.parallel` package that has subpackages for `immutable` and `mutable` types. The parallel collections are not subtypes of the normal collections we have used to this point. Instead, they have mutual supertypes that begin with `Gen` for general. The reason for this is that the original collections had an implicit contract to go through their elements in order and in a single thread. A lot of the code we have written did not depend on this, but some of it did. The general types explicitly state that they do not have to preserve that behavior.

The parallel collections have names that begin with `Par`. Not all of the types we used previously have parallel equivalents. This is because some types, for example the `List`, are inherently sequential. If you think back to the last chapter, we saw that there were a whole set of types under the `LinearSeq` type that had linear access behavior. None of those types can be efficiently implemented in parallel because of that. Figure 21.2 shows a Unified Modeling Language (UML) class diagram of the parallel collections.

To convert from a normal collection to a parallel collection call the `par` method on the standard collection. To convert back, call the `seq` method on the parallel collection. These calls are efficient for types that have a parallel equivalent. You can convert a `Range`, a `Vector`, an `Array`, a `HashSet`, or a `HashMap` from sequential to parallel and back in O(1) time. For other types, the conversion will be less efficient as it has to build a completely new collection. Consider the following examples from the REPL.

```
```
scala> 1 to 10 par
res0: scala.collection.parallel.immutable.ParRange = ParRange(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
```
```

```
```
scala> Array(1,2,3,4) par
res1: scala.collection.parallel.mutable.ParArray[Int] = ParArray(1, 2, 3, 4)
```
```

```
```
scala> List(1,2,3,4) par
res2: scala.collection.parallel.immutable.ParSeq[Int] = ParVector(1, 2, 3, 4)
```
```

The first two calls are able to simply wrap the sequential version in a parallel collection. The last one has to convert the `List` over the the `ParVector`. The choice of `ParVector` in this situation is made because preserving immutability is the primary consideration.