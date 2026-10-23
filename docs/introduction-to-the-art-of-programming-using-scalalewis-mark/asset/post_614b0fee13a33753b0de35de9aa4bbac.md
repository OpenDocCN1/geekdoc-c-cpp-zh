
function around if you were going to be using it often instead of replacing calls to it with `wordCount("file.txt").keySet` because the counting of the words does extra work that is not needed to produce the set.

A more general use case for maps is using them as a fast way to look up groups of data like case classes by a particular key value. An example of this would be looking up a case class that represents a student by the student's ID or perhaps their unique login number. The real power of the Map type comes from the fact that the key and value types can be anything that you want.

## 20.4 Buffers

The last of the new collection types that we will look at in detail in this chapter is the `Buffer`. The Buffer type is like an `Array` that can change size. As a result, the Buffer type is implicitly mutable. There is no immutable Buffer. If you are using other mutable types, the rule of importing `scala.collection.mutable` and referring to a Buffer as `mutable.Buffer` will still work well and it makes it perfectly clear to anyone reading the code that you are using a mutable type. However, because the Buffer type is only mutable, you could also consider doing an import of `scala.collection.mutable.Buffer` and simply calling it a Buffer in your code.

There are several subtypes of Buffer in the Scala libraries. The two most significant ones are `ArrayBuffer` and `ListBuffer`. One uses an array to store values. The other uses a structure called a linked list. The List type in Scala is also a linked list, though it is not directly used by the ListBuffer because the ListBuffer needs to be mutable. We will use the ArrayBuffer in this chapter. The nature of the ListBuffer and how it is different will become more apparent in chapter 25.

You can create a buffer in exactly the way that you would expect.

```scala
scala> val buf = mutable.Buffer(1,2,3,4,5)
buf: scala.collection.mutable.Buffer[Int] = ArrayBuffer(1, 2, 3, 4, 5)
```

You can also use some of the methods we learned about for `Array` and `List` like `fill` and `tabulate`.

```scala
scala> val rbuf=mutable.Buffer.fill(10)(math.random)
rbuf: scala.collection.mutable.Buffer[Double] = ArrayBuffer(0.061947605764430924,
 0.029870283928219443, 0.5457301708447658, 0.7098206843826819,
 0.8619215922836797, 0.5401420250956313, 0.6249953821782052,
 0.1376217145656472, 0.26995766937532295, 0.8716257556831167)
```

You can index into a buffer and change values the same way you did for an array.

```scala
scala> rbuf(3)
res0: Double = 0.7098206843826819

scala> buf(3)=99
```

```scala
scala> buf
res1: scala.collection.mutable.Buffer[Int] = ArrayBuffer(1, 2, 3, 99, 5)
```

The way in which the Buffer type differs from the `Array` type is that it can easily grow and shrink. There are a whole set of methods that take advantage of this. Here are some of them.

- `+=(elem: A): Buffer[A]` - Append the element to the buffer and return the same buffer.
- `+=:(elem: A): Buffer[A]` - Prepend the element to the buffer and return the same buffer.
- `++=(xs: TraversableOnce[A]): Buffer[A]` - Append the elements in xs to the buffer and return the same buffer.
- `++=:(xs: TraversableOnce[A]): Buffer[A]` - Prepend the elements in xs to the buffer and return the same buffer.
- `-=(elem: A): Buffer[A]` - Remove the element from the buffer and return the same buffer.
- `--=(xs: TraversableOnce[A]): Buffer[A]` - Remove all the elements in xs from the buffer and return the buffer.
- `append(elem: A): Unit` - Append the element to the buffer.
- `appendAll(xs: TraversableOnce[A]): Unit` - Append the elements in xs to the buffer.
- `clear(): Unit` - Remove all the elements from the buffer.
- `insert(n: Int, elems: A*): Unit` - Insert the specified elements at the specified index.
- `insertAll(n: Int, elems: Traversable[A]): Unit` - Insert all the elements in elems at index n.
- `prepend(elems: A*): Unit` - Prepend the elements to this buffer.
- `prependAll(xs: TraversableOnce[A]): Unit` - Prepend all the elements in xs to this buffer.
- `remove(n: Int, count: Int): Unit` - Remove count elements starting with the one at index n.
- `remove(n: Int): A` - Remove the one element at index n and return it.
- `trimEnd(n: Int): Unit` - Remove the last n elements from this buffer.
- `trimStart(n: Int): Unit` - Remove the first n elements from this buffer.

Most of these should be fairly self-explanatory. The only methods that you might question are the ones that involve symbol characters. There are two things of interest here. The first is that they all return the buffer that they are called on. The reason for this is that it allows you to string them together to append or prepend multiple elements in a row. Consider this example with appending.

```scala
scala> buf += 6 += 7
res2: buf.type = ArrayBuffer(1, 2, 3, 99, 5, 6, 7)
```

Here both 6 and 7 are appended in a single line.

The other operations that might seem odd are `+=:` and `++=:`. These operations say that they prepend. What is interesting about them is their usage. Here is an example.

```scala
scala> 0 +=: buf
res3: buf.type = ArrayBuffer(0, 1, 2, 3, 99, 5, 6, 7)
```

The value to be prepended is to the left of the operator and the buffer is on the right. In some ways that makes sense given where it is in the buffer after the prepending. We have seen something like this before as well. The cons operator on a list is `::` and it prepends the element to the list. That operator also ends with a colon. This is one of the more esoteric rules of Scala. Any symbolic operator method that ends in a colon is right associative instead of being left associative the way most operators are. This means that the object the operator works on is to the right of the operator and the operations are grouped going from the right to the left.

## 20.5 Collections as Functions

The different collection types all inherit from PartialFunction, which inherits from the standard function types. This means that you can use collections in places where you would normally be expected to use functions. For example, the `Seq[A]` type will work as an `Int => A`. Similarly, a `Map[A,B]` can be used as an `A => B`.

A simple example usage of this is to take every third element of an array by mapping over a range with the desired indexes and using the array as the function argument.

```scala
val nums = Array.fill(30)(math.random)
val everyThird = (nums.indices by 3).map(nums)
```

In this way, applying map with a collection as the argument gives us the ability to do arbitrary indexing into a collection.

## 20.6 Project Integration

There are quite a few places where we can use these different collections. In the previous chapter the type mutable.Buffer was used in DrawTransform to hold children. This made it easy to include code that adds and removes children. In this section we are going to use the Map type to help with text commands. After that, we will make use of an Array to clean up adding Drawables to a Drawing. This is something we could have done before, but it fits better here when looking at different uses of collections.

### 20.6.1 Commands

The command processor is a part of the code that could be implemented with inheritance. It would be possible to make a type called Command that we have other types inherit from. That type of construct would make logical sense, but might not be what we really need. One of the aspects you want to learn about inheritance is to not use it when it is not required. To know if we need it, we have to do some analysis.

You might wonder why we would want to put a text-based command processor into a drawing program. Perhaps the best analogy for this is why you would want to include a command-line interface in an Operating System (OS) that has a Graphical User Interface (GUI). There are certain operations that simply work better when they are typed in than they would when you have to point and click them. For now we will start with some simple examples that we can use as use-cases for the command tool. There are three commands that we will start with:

- `echo` - prints whatever follows the command,
- `add` - should be followed by a bunch of space separated numbers and prints the sum,
- `refresh` - takes no arguments and causes the drawing to refresh.

So the user might type in “echo Hello, World!”, “add 1 2 3 4 5”, or “refresh”. The first two take arguments and the only result of calling them is that something is displayed in the output. The last one is very different in that it does not take arguments or display anything. Instead, it needs to cause the Drawing object that is displayed to repaint itself.

To make this happen in the code, we will need a listener on the TextField for the user input that reacts to an EditDone event. When that happens, the line that is typed in needs to have the first word identified and based on what it is, appropriate functionality needs to be invoked.

One way to implement this functionality is to have each command include a function of the form `(String,Drawing) => Any`. The first parameter to this function will be the rest of the line after the command. The second parameter is the Drawing object the command was invoked on. This is needed so that a command like refresh can cause something to happen associated with the drawing. The return value is anything we want to give back. For most things this object will be converted to a String and appended to the output.

Having these functions is not quite enough. We also need to have the ability to quickly identify which of these functions should be invoked based on the first word of the input. This is a perfect usage of a Map. More specifically, we want to use a `Map[String, (String,Drawing)=>Any]`. This is a map from each command String to the function that command should invoke.

Using this approach, we can declare an object that contains the command functionality. An implementation that includes the three commands described above might look like the following.

```scala
package scalabook.drawing

/**
 * This object defines the command processing features for the drawing.
 * Use apply to invoke a command.
 */
object Commands {
    private val commands = Map[String,(String,Drawing)=>Any](
        "add" -> ((rest,d) => rest.trim.split(" +").map(_.toInt).sum),
        "echo" -> ((rest,d) => rest.trim),
        "refresh" -> ((rest,d) => d.refresh)
    )

    def apply(input:String,drawing:Drawing):Any = {
        val spaceIndex = input.indexOf(' ')
```
