# 12.7  Streams as Infinite Data Structures

Function `hanoi` from Listing 12.7 builds its resulting stream by using “`#::`” and “`#:::`”. These operations are implemented lazily and can build a stream without triggering the evaluation of their stream arguments. In particular, they can be used to define streams that are conceptually infinite:

```
```scala
def countUp(n: Int): LazyList[Int] = n #:: countUp(n + 1)

val naturals = countUp(0) // 0, 1, 2, 3, ...
```
```

At first sight, function `countUp` makes no sense. It seems to violate one of the principles of a good recursive function—namely, to terminate, a function should always define at least one non-recursive branch. Here, `countUp` always invokes `countUp`. Indeed, if you write this function using lists, it will never terminate. On streams, however, the definition is valid. It produces a never-ending stream of numbers. Of course, any attempt to evaluate the entire stream—for example, `naturals.toList`—would result in a non-terminating computation.

You can sometimes use infinite streams to replace mutable data with values of a more functional flavor. For instance, a (mutable) pseudo-random number generator can be replaced with an infinite stream of pseudo-random numbers:

```
```scala
def randomNumbers: LazyList[Float] = Random.nextFloat() #:: randomNumbers
```
```

Infinite streams are often created using generative higher-order functions. For example, the `naturals` and `randomNumbers` streams can be created in this way:

```
```scala
val naturals     = LazyList.iterate(0)(_ + 1)
val randomNumbers = LazyList.continually(Random.nextFloat())
```
```

# 12.8  Iterators

The “3n + 1” problem defines the following sequence: If a natural number n is even, its successor is n ÷ 2; otherwise, it is 3n + 1. This sequence, sometimes known as the Collatz sequence, is conjectured to always reach 1 eventually, for any starting natural number. For instance, if you start with 27, the sequence produces 111 numbers before reaching 1 for the first time (and then continues forever as 4, 2, 1, 4, 2, 1, …):