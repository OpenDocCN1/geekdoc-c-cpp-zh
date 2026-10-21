If reading the file has failed, both expressions produce a failed value with the exception that caused readFile to fail. If the file can be read, the first expression is a success. The second expression can still be a success or a failure, depending on what is returned by computeOrFail.

If you prefer to ignore the cause of a failure, you can change a Try type into an option:

```
readFile(...).toOption // of type Option[List[String]]
```

The Try type is heavily used in concurrent programming to carry exceptions from one thread to another (several examples are provided in Part II). Contrast this use of a future in Java:

```
future.whenComplete((value, error) -> {
  if (error == null) ... // use value
  else ... // handle error
});
```

with the same program in Scala:

```
future.onComplete {
  case Success(value) => ... // use value
  case Failure(error) => ... // handle error
}
```

Using Try is cleaner and safer than dealing with a pair (value,error) of which one element is always null.

# 13.4 Using Either

The Try type is very much dedicated to handling failures, unlike Option, which you can use for other purposes as well. Another standard, general-purpose type with two alternatives, Either, is also sometimes used in error handling.

While Option is a value or nothing and Try is a value or an exception, Either is a value or another value, possibly of a different type. A value of type Either[A,B] is either a Left[A] or a Right[B]. Conceptually, you can think of Option[A] as Either[None.type,A], and of Try[A] as Either[Throwable,A]. It is customary to use Right to represent the successful path and Left for an alternative. Accordingly, methods like contains, map, and filter work on the inside of the right part.

3This can be changed via a left method: either.left.map(...) will transform the left part of the either value.