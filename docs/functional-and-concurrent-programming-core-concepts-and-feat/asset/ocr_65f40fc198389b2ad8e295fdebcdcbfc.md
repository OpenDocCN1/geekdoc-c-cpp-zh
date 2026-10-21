sometimes, but sometimes fails. It fails when the atomic integer is accessed by another thread between increment and get (first example), or between if and then (the second example). You can make these failures more likely by inserting calls to Thread.yield (see Section 17.5) in the code of function getRank:

```
def getRank(): Int =
  userCount.increment()
  Thread.`yield`()
  userCount.get()

def getRank(): Option[Int] =
  if userCount.get() < 5 then
    Thread.`yield`()
    Some(userCount.incrementAndGet())
  else None
```

With added calls to Thread.yield, the test fails much more frequently. By contrast, adding calls to Thread.yield in a correct program should never break it. It is often a good testing strategy to insert such calls in places where a thread losing control of the CPU is thought to potentially be unsafe; correct code should continue to behave correctly.

# Aside: Example of a Heisenbug

Consider this modified version of Listing 18.2:

```
val shared = ArrayList[String]()

def addStrings(n: Int, str: String): Unit =
  var added = 0
  while added < n do
    if shared.size >= 2 * added then
      shared.add(str)
      added += 1

val t1 = Thread(() => addStrings(5, "T1"), "T1")
val t2 = Thread(() => addStrings(5, "T2"), "T2")

t1.start(); t2.start()
t1.join(); t2.join()

println(shared.size)
```

In this variant, each thread checks that it is not too far ahead of the other thread before adding a value into the shared list. A thread adds a new item to the list