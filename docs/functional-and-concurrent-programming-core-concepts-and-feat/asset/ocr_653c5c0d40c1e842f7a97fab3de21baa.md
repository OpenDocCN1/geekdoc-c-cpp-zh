# # Chapter 12 Lazy Evaluation

This function takes a by-name argument, keeps track of the amount of time needed to evaluate it, and returns the duration in seconds. You can use it without explicitly creating a thunk function:

```
```scala
val seconds: Double = timeOf {
InetAddress.getLocalHost.getHostName // or any code for which you want the duration
}
```
```

The popular Scala library Scalactic defines a times construct, used as follows:

```
```scala
3 times {
println("Beetlejuice!")
}
```
```

Although times looks like a keyword and a language construct, it is actually defined as a regular function. You could implement it as an extension method:

```
```scala
extension (count: Int)
infix def times[U](code: => U): Unit =
  var n = count
  while n > 0 do
    code
    n -= 1
```
```

> Listing 12.4: Control abstraction example: function times.

This method is defined as an extension so it can be called on regular integers. It uses a by-name argument for the code to be repeated: The code is passed unevaluated, and is evaluated by the times method as many times as needed.

As a more elaborate example, let’s define a new looping construct repeat–until:

```
```scala
class Repeat[U](code: => U):
  infix def until(test: => Boolean): Unit =
    code
    while !test do code
def repeat[U](code: => U) = Repeat(code)
```
```

> Listing 12.5: Control abstraction example: repeat–until.

Class Repeat uses a by-name argument in its constructor. The constructor produces an object that implements the repetition in its until method, using a termination test that is also passed by name. You can use this new construct as follows: