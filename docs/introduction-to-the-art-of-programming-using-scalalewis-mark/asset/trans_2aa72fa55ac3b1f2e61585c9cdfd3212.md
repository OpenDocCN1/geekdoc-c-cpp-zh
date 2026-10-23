

start processing collisions until all the threads are done identifying the first round because it is possible that the last one found could be the first one you need to process. So all the threads have to finish finding collisions before the first one can be processed. There are schemes for processing collisions in parallel as well that make sure that you do not ever work on two collisions at the same time if they are too close. All collisions have to be processed and all threads have to get to the same point before the other processing can be done.

There are three different types in java.util.concurrent that can help give you this type of behavior. The first one is a type called CountDownLatch. You instantiate a CountDownLatch with new CountDownLatch(count), where count is an integer value. The two main methods of this type are countDown, which decrements the count by one, and await which will block until the count reaches zero. If the count is already at zero, a call to await does nothing.

The second type that can provide this type of behavior is the CyclicBarrier. While the CountDownLatch is only good for one use, the CyclicBarrier can be cycled many times. You make a CyclicBarrier with new CyclicBarrier(parties), where parties is an integer number specifying how many threads should be involved in the barrier. When each thread has finished doing its task, it makes a call to the await method on the CyclicBarrier. Once all “parties” have called await, they are all allowed to proceed forward.

The third type is the Phaser type. This type is more complex than the other two. It is also newer, having been added in Java 1.7. Interested readers should consult the API for usage of this type.

## 21.3.3.2 The Exchange

Imagine a situation where two parties work mostly independently, but they perform calculations that require some information from another party. You do not want to try reading the information at any old time as the value might not contain a valid, final result most of the time. Instead, you need to arrange a point when the parties pause and come together for an exchange.

An example might be a large simulation of a solid body like an airplane. These are often done with finite-element models. Each thread would have a chunk of the plane to work with and it would calculate the stresses on the elements in that chunk as they change over time. The stresses on one chunk will depend on what is happening with all the elements in adjacent chunks that are connected to elements in the first one. In order to do a full calculation, the threads need to meet up to exchange information about the boundary elements. This type of thing can be done with an Exchanger.

You instantiate an Exchanger with new Exchanger[A](), where A is the type of information you want to exchange. When a thread is ready to exchange, it calls exchange(x:A):A on the Exchanger. This method will block for the first thread until the second thread also calls it. At that point, both calls return and each thread gets the value that was passed in by the other one.

## 21.3.3.3 Assembly Line

When you picture humans working in parallel on a task, one way to break things up is the assembly line. Here you have one group of people who do some part of the work and get products to a certain point. Then they pass their results on to others in a different group who do the next step. This continues until the final result is produced. This arrangement has a critical junction at the point where the product moves from one station to the next. Generally, one person in line can not start working on something until the person before

them is done. If there are not any products in the right state, then that person needs to wait until one shows up.

There are two different types in `java.util.concurrent` that will allow you to achieve this behavior, **BlockingQueue**[A] and **BlockingDeque**[A]. The two main methods on both of these types are put and take. The put method will add a new value. Some implementations of these types will have limited space. If there is not space to add the new value, the call will block until space is freed up. The take method will remove a value. If no value is available, then the call will block until one becomes available.

Both of these types are abstract. In the case of **BlockingDeque** there is one implementation provided called **LinkedBlockingDeque**. For the **BlockingQueue** type there are a number of different implementations: **ArrayBlockingQueue**, **DelayQueue**, **LinkedBlockingQueue**, **LinkedTransferQueue**, **PriorityBlockingQueue**, and **SynchronousQueue**. We will talk about queues in general and specific implementations using arrays and linked lists in chapters 24 and 25. After covering that material you might consider revisiting the concept of the **BlockingQueue**.

## 21.3.3.4 Ticked Passengers

Some types of work are limited by resources. If you are building a house the number of people involved in driving nails will be limited by the number of hammers that you have. If you are transporting people on a plane, there are a limited number of seats. On a computer, there might be limits to how many threads you want involved in activities that deal with hardware, like reading from the network. There might be some types of processing that are particularly memory intensive for which you need to limit the number of threads doing them at any given time. For these types of situations, the **Semaphore** provides a way to limits how many threads can get to a certain region of code at a given time. Unlike the monitors described with synchronized, the **Semaphore** is more flexible than just allowing one thread in at a time.

You can instantiate a **Semaphore** with new **Semaphore(permits)**, where permits is an Int specifying how many of the resource you have. The main methods for the **Semaphore** are acquire and release. The acquire method will get one of the permits. If none are available, it will block until a different thread calls release to make one available. There is also a tryAcquire method that returns a Boolean that does not block. If a permit was available, it takes it and returns true. Otherwise it simply returns false.

## 21.3.3.5 Other Threadsafe Types

Various types in `java.util.concurrent` for working in applications with multiple threads. These types all begin with Concurrent. If you are using mutable data types from the Scala libraries, you can mix-in the proper synchronized traits, but because that gives you types where all methods are synchronized, the concurrent versions can provide better performance.

For example, if you are dealing with a mutable map, the Scala libraries would let you do the following.

```
val smap = new mutable.HashMap[String,Data] with mutable.SynchronizedMap[String,Data]
```

This would give you a mutable map that uses a String for the key with some type called Data for the values where all the methods are synchronized so that it can be safely used across threads. Alternately, you could use the Java libraries and get a ConcurrentHashMap like this.

It is much like a `Semaphore` with only one permit. The main concrete subclass is called `ReentrantLock`, which you can make by calling `new ReentrantLock`.

## 21.4 Parallel Collections

Even working with the concurrency library, parallelism can be hard to do well. For this reason, beginning with version 2.9, Scala has added another layer in the form of parallel collections. These are collections that have their basic operations performed in parallel. Not only do they do their operations in parallel, they have been written in such a way that they will automatically load balance. If one thread finishes its own work load, it will steal work from another thread that has not yet finished. For this reason, if your problem can be solved using parallel collections, you should probably use them. Not only will they be easier to write, they will probably be more efficient than anything you are going to take the time to write yourself.

The structure of the parallel collections largely mirrors the structure of the normal collections with a `scala.collection.parallel` package that has subpackages for `immutable` and `mutable` types. The parallel collections are not subtypes of the normal collections we have used to this point. Instead, they have mutual supertypes that begin with `Gen` for general. The reason for this is that the original collections had an implicit contract to go through their elements in order and in a single thread. A lot of the code we have written did not depend on this, but some of it did. The general types explicitly state that they do not have to preserve that behavior.

The parallel collections have names that begin with `Par`. Not all of the types we used previously have parallel equivalents. This is because some types, for example the `List`, are inherently sequential. If you think back to the last chapter, we saw that there were a whole set of types under the `LinearSeq` type that had linear access behavior. None of those types can be efficiently implemented in parallel because of that. Figure 21.2 shows a Unified Modeling Language (UML) class diagram of the parallel collections.

To convert from a normal collection to a parallel collection call the `par` method on the standard collection. To convert back, call the `seq` method on the parallel collection. These calls are efficient for types that have a parallel equivalent. You can convert a `Range`, a `Vector`, an `Array`, a `HashSet`, or a `HashMap` from sequential to parallel and back in O(1) time. For other types, the conversion will be less efficient as it has to build a completely new collection. Consider the following examples from the REPL.

```
scala> 1 to 10 par
res0: scala.collection.parallel.immutable.ParRange = ParRange(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
```

```
scala> Array(1,2,3,4) par
res1: scala.collection.parallel.mutable.ParArray[Int] = ParArray(1, 2, 3, 4)
```

```
scala> List(1,2,3,4) par
res2: scala.collection.parallel.immutable.ParSeq[Int] = ParVector(1, 2, 3, 4)
```

The first two calls are able to simply wrap the sequential version in a parallel collection. The last one has to convert the `List` over the the `ParVector`. The choice of `ParVector` in this situation is made because preserving immutability is the primary consideration.

