The failure case could be handled in any way. Here, the chosen semantics is to return an empty list.

# 13.3 Using Try

Using options can go a long way toward handling errors without exceptions while avoiding the dangers of using special values within the same type. Options, however, are completely silent as to the cause of failure. When you need more information regarding the nature of an error, you can instead use a Try type (also called Result in some languages). It is a type with two alternatives, like Option. The first alternative, Success(value), represents a usable value, similar to Some(value). The second alternative, Failure(error), represents an error and can be used to provide more information than options do with None.

As an example, the list searched by function between could come from a file, and reading that file may fail for a number of reasons: The file is not found, the file is empty, the permissions do not allow reading, and so on. A readFile function that returns an option would hide the cause of the failure entirely. Alternatively, you can define readFile to return a Try:

```
Scala
def readFile(file: Path): Try[List[String]] = ...
```

Like Option, the Try type supports higher-order methods. You can use map to feed the list of strings, if any, to function between. On Try, function map transforms a valid value; failures are left unchanged:

```
Scala
readFile(wordFile).map(between(_, "two", "three")) // Success(List("two", "three"))
readFile(notFound).map(between(_, "two", "three")) // Failure(...)
```

These two expressions have type Try[List[String]]. If file wordFile contains the sequence of words used earlier, the first expression is a success value. If file notFound does not exist, the second expression is the failure returned by readFile, is unchanged by map, and contains the relevant NoSuchFileException.

In Section 10.3, we saw how flatMap can be used to transform optional values with computations that themselves produce options. The same is true of Try:

```
Scala
def compute(list: List[String]): Int = ...
def computeOrFail(list: List[String]): Try[Int] = ...

readFile(...).map(compute) // of type Try[Int]
readFile(...).flatMap(computeOrFail) // of type Try[Int]
```