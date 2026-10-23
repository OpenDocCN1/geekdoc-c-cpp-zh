
![](img/157fcf510c119278e4b1267c62717fa8_673_0.png)

FIGURE 24.2: This figure shows a graphical representation of an array-based stack and how it changes over several operations. The stack stores data in the array and uses an integer index to keep track of the position of the top.

This trait effectively defines the ADT in Scala. Once we have it, we can work on a class that extends the trait and provides concrete implementations of the methods. Before we show the code for such an implementation, we should pause to think about how it might work and what it would look like in memory. A possible view of this is shown in figure 24.2. For illustration purposes, this stack stores Ints. We have an array that stores the various values as well as an integer value called top that stores the index where the next element should be placed in the stack. Each time a value is pushed, it is placed in the proper location and top is incremented. When a value is popped, top is decremented and the value at that location is returned.

Though this figure does not show it, we also need to handle the situation where enough elements have been pushed that the array fills. In this situation, a larger array needs to be allocated and the values should be copied over so that we have room for more elements.

Code that implements this view of a stack can be seen here.

```
package scalabook.adt

class ArrayStack[A : Manifest] extends Stack[A]{
  private var top = 0
  private var data = new Array[A](10)
```

|  | data.length*2 |  | data.length+10 |  |
|---|---|---|---|---|
| Resize Event | Size | Total Work | Size | Total Work |
| 1 | 10 | 10 | 10 | 10 |
| 2 | 20 | 30 | 20 | 30 |
| 3 | 40 | 70 | 30 | 60 |
| 4 | 80 | 150 | 40 | 100 |
| 5 | 160 | 310 | 50 | 150 |
| 6 | 320 | 630 | 60 | 210 |
| ... | ... | ... | ... | ... |
| m | 10 × 2^m | 10 × (2^{m+1} − 1) | 10m | 5m(m + 1) |

To get the amortized cost, we divide the total work by the size because we had to call push that number of times to get the stack to that size. For the first approach we get

```
\frac{10 \times (2^{m+1} - 1)}{10 \times 2^{m}} = \frac{2^{m+1} - 1}{2^{m}} = 2 - \frac{1}{2^{m}} \approx 2 \in O(1).
```

For the second approach we get

```
\frac{5m(m + 1)}{10m} = \frac{m + 1}{2} \in O(m).
```

Neither the multiple of 2, nor the addition of 10 is in any way magical. Growing the array by a fixed multiple greater than one will lead to amortized constant cost. Growing the array by any fixed value will lead to an amortized linear cost. The advantage of the fixed multiple is that while the copy events gets exponentially larger, they happen inversely exponentially often.

## Manifests (Advanced)

To understand Manifests, it helps to have some understanding of the history of Java as the nature of the Java Virtual Machine (JVM) plays a role in their existence. The parallel to Scala type parameters in Java is generics. Generics did not exist in the original Java language. In fact, they were not added until Java 5. At that point, there were a huge number of JVMs installed around the globe and it was deemed infeasible to make changes that would invalidate all of them. For that reason, as well as a motivation to keep the virtual machine fairly simple, generics were implemented using erasure. What this means is that the information for generics was used at compile time, but was erased in the compiled version so that at runtime it was impossible to tell what the generic type had been. In this way, the code that was produced looked like what would have been produced before generics were introduced.

This has quite a few effects on how Java programs are written. It comes through in Scala as a requirement for having a manifest on certain type parameters. The manifest basically holds some of the type information so that it is available at runtime. To understand why we need this, we should go back to the expression that was responsible for us needing a manifest: new Array[A](10). This makes a new Array[A] with 10 elements in it and sets the 10 elements to appropriate default values. It is the last part that leads to the requirement of having a manifest. For any type that is a subtype of AnyRef, the default value is null. For the subtypes of AnyVal, the default varies. For Int, it is 0. For Double it is 0.0. For Boolean it is false. In order to execute that expression, you have to know enough at least enough about the type to put in

proper default values.¹ Type erasure takes away that information from the runtime. The manifest allows Scala to get back access to it.

It is also worth noting that our implementation of the stack technically does not actually remove the value from the array when pop() is called. This remove is not really required for the stack to execute properly. However, it can improve memory usage and performance, especially if the type A is large. Unfortunately, that would require having a default value to put into the array in that place, which we have just discussed it is hard from a completely general type parameter.

## 24.6 Array-Based Queue

Like the stack, the code for the array-based queue begins by setting up the ADT as a completely abstract trait. This trait, which takes a type parameter so that it can work with any type, is shown here.

```
package scalabook.adt

/**
 * This trait defines a mutable Queue ADT.
 * @tparam A the type of data stored
 */
trait Queue[A] {
  /**
   * Add an item to the queue.
   * @param obj the item to add
   */
  def enqueue(obj:A)

  /**
   * Remove the item that has been on the longest.
   * @return the item that was removed
   */
  def dequeue():A

  /**
   * Return the item that has been on the longest without removing it.
   * @return the most recently added item
   */
  def peek:A

  /**
   * Tells whether this queue is empty.
   * @return true if there are no items on the queue, otherwise false.
   */
  def isEmpty:Boolean
}
```

¹You also need other information such as how big a memory block should be reserved. For example, Int requires 4-bytes while Double requires 8.

![](img/157fcf510c119278e4b1267c62717fa8_677_0.png)

FIGURE 24.3: This figure shows a graphical representation of an array-based queue and how it changes over several operations. The queue stores data in the array and uses integer indexes to keep track of the front and back.

As with the stack, this has only the signatures of the methods along with comments describing what they do.

The queue ADT can also be implemented using an array. Figure 24.3 shows how this might look for several operations. Unlike the stack, the queue needs to keep track of two locations in the array: a front and a back. The back is where new elements go when something is added to the queue and the front is where values are taken from when they are removed. Both indexes are incremented during the proper operations. When an index moves beyond the end of the array, it is wrapped back around to the beginning. This allows us to continually add and remove items without having to grow the array or copy elements around. Both of those would require O(n) operations and prevent our total performance from being O(1).

This figure does not show what happens when the queue gets full. At that point a bigger array is needed and values need to be copied from the old array into the new one. The details for the queue are not quite as straightforward as they were for the stack. Figure 24.4 demonstrates the problem and a possible solution. Doing a direct copy of elements is not appropriate because the wrapping could have resulted in a situation where the front and back are inverted. Instead, the copy needs to shift elements around so that they are contiguous. The values of front and back need to be adjusted appropriately as well. There

![](img/157fcf510c119278e4b1267c62717fa8_678_0.png)

FIGURE 24.4: This figure shows a graphical representation of an array-based queue when it needs to grow on an enqueue. The queue is seen as empty if front==back. For that reason, the grow operation should happen when the last slot will be filled. In addition to growing a bigger array, the copy operation needs to move elements of the array around and alter the location of front and back.

are many ways that this could be done. Figure 24.4 demonstrates the approach that we will take in the code here where the front is moved back to the beginning of the array.

This graphical description of implementing an array-based queue can be implemented in code like the following.

```
package scalabook.adt

class ArrayQueue[A : Manifest] extends Queue[A] {
    private var front,back = 0
    private var data = new Array[A](10)

    def enqueue(obj:A) {
        if((back+1)%data.length==front) {
            val tmp = new Array[A](data.length+2)
            for(i <- 0 until data.length-1) tmp(i) = data((i+front)%data.length)
            front = 0
            back = data.length-1
            data = tmp
        }
        data(back) = obj
        back = (back+1)%data.length
    }

    def dequeue():A = {
        assert(!isEmpty,"Dequeue called on an empty queue.")
```
