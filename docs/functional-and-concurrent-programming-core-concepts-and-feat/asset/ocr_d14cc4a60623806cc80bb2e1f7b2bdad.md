is used asynchronously, you may even need callbacks within callbacks, which are difficult to write and even more difficult to debug. A better solution would be to bring the non-blocking nature of callbacks into code that maintains a more functional style.

Before we revisit the ad-fetching example in Section 26.5, consider this callback-based function:

```
Scala
def multiplyAndWrite(futureString: Future[String], count: Int): Unit =
  futureString.onComplete {
    case Success(str) => write(str * count)
    case Failure(e)   => write(s"exception: ${e.getMessage}")
  }
```

Somewhere, an input string is being produced asynchronously. It is passed to function multiplyAndWrite as a future. This function uses a callback to repeat the string multiple times and to write the result—in Scala, "A" * 3 is "AAA". This approach requires that you specify in the callback action everything you want to do with the string str * count, which does not exist outside this callback. This is a source of possible complexity and loss of modularity. It could be more advantageous to replace multiplyAndWrite with a multiply function that somehow returns the string str * count and makes it available to any code that needs it.

Within this multiply function, however, the string to multiply may not yet be available—its computation could still be ongoing. You also cannot wait for it because you want to avoid blocking. Instead, you need to return the multiplied string itself as a future. Accordingly, the return type of multiply is not String, but rather Future[String]. The future to be returned can be created using a promise, as in Listing 25.4:

```
Scala
def multiply(futureString: Future[String], count: Int): Future[String] =
  val promise = Promise[String]()
  futureString.onComplete {
    case Success(str) => promise.success(str * count)
    case Failure(e)   => promise.failure(e)
  }
  promise.future
```

You create a promise to hold the multiplied string and a callback action to fulfill the promise. If the future futureString produces a string, the callback multiplies it and fulfills the promise successfully. Otherwise, the promise is failed, since no string was available for multiplication.

Now comes the interesting part. Conceptually, the preceding code has little to do with strings and multiplication. What it really does is transform the value produced by a future so as to create a new future. Of course, we have seen this pattern before—for instance, to apply a function to the contents of an option—in the form of the higher-