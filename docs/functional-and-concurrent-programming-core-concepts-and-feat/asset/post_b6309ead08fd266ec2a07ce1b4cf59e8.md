
## Chapter 10 Standard Higher-Order Functions

Similarly,

```
for load <- loads do load.reduce()
```

was used to update a list of mutable objects. It is compiled into

```
loads.foreach(load => load.reduce())
```

When for-do and for-yield use conditions, a filtering step is inserted by the compiler. The expression

```
for load <- loads if load.weight != 0 yield load.reduced
```

is compiled into

```
loads.withFilter(load => load.weight != 0).map(load => load.reduced)
```

Listing 10.8 added a method foreach to binary trees. As a result, you can now process trees using for-do:

```
val tree: BinTree = ...
```

```
for x <- tree do println(x) // prints all the values in the tree, in order
```

The for-do expression is compiled into tree.foreach(println).

Many libraries implement foreach, map, flatMap, and filter functions, but few programming languages define a for-comprehension syntax identical to Scala’s. Some constructs, though, are similar, like Python’s list comprehensions. The Python code

```
[round((temp - 32) / 1.8) for temp in temps if temp > 75]
```

corresponds to the following Scala code:

```
for temp <- temps if temp > 75 yield ((temp - 32) / 1.8f).round
```

Method withFilter is semantically equivalent to filter, but uses a form of delayed evaluation to avoid the creation of an intermediate list (see the discussion of views and lazy evaluation in Section 12.9).

In Java, which has higher-order functions only, you need to use filter and map directly:

```
Java
IntStream temps = ...
temps.filter(temp -> temp > 75).map(temp -> Math.round((temp - 32) / 1.8f))
```

### NOTE

Given my intent to prepare developers for a variety of languages, I often use higher-order functions in code examples instead of for-do or for-yield, especially outside of case studies. This is a choice I made for pedagogical reasons, to better emphasize the similarities of patterns across languages, but it tends to result in Scala code that is not always idiomatic. Readers with Scala experience will forgive me.

## 10.10 Summary

- The functions presented in this chapter form a core set of higher-order functions commonly found in functional libraries. They are often available on many types, such as streams and collections, but also options and futures.
- Several functions use a predicate—a Boolean function—as their argument. They are used to find, count, filter, or assert the existence of elements that satisfy this predicate.
- Function map is used to apply an arbitrary transformation to elements within a structure and produces a new structure that contains the transformed values. If an operation is applied to elements for the purpose of side effects only, and no resulting structure is needed, function foreach can be used instead of map.
- Function flatMap is similar to map but takes care of “flattening” nested structures, like lists of lists or options of options. This function is powerful and can be used to apply a computation with optional output to an optional input (to avoid an option of option), or to handle an event that triggers a new stream of events (to avoid a stream of stream), or to asynchronously transform a value that is itself calculated asynchronously (to avoid a future of future).
- Fundamentally, foreach, map, flatMap, and filter (or withFilter) are used to transform the contents of a structure (e.g., list, option, future) from outside the structure. This common pattern is sometimes supported by syntax at the language level, like Scala’s for-comprehension or Python’s list comprehension.
- Folding functions are used to reduce the elements of a structure into a single value using a combining operator. Many computations that would process the elements of a collection iteratively can be implemented in terms of a folding function.
- Conversely, higher-order functions can be used to generate a collection of elements. Functions iterate and unfold, for instance, rely on an initial seed and the repeated application of a function to generate a sequence of values.
- Calculations such as minimum, maximum, and sorting, which require element comparison, need to be parameterized by the criterion used to compare values. Higher-order variants often use a comparison function (e.g., `sortWith`) or a mapping into an existing ordered type (e.g., `sortBy`, `maxBy`).
- As an alternative to a comparison criterion for sorting or for minimum/maximum calculation, a grouping criterion is sometimes used to collect related elements (e.g., `groupBy`).
- Many other higher-order functions exist beside this fundamental core group. For instance, the `Observable` class of the RxJava reactive library has more than a hundred higher-order methods, some of which deal with error handling, threading, or real time, in addition to the core functional transformations discussed in this chapter.

The list of nodes in a directory should never contain two nodes with the same name. The order of nodes in a list is irrelevant: Directories that contain the same files and sub-directories in different orders are considered equivalent. Trees are immutable: Adding or removing files and directories is achieved via functions that produce a new tree.

## 11.2 A Node-Searching Helper Function

Several tree operations need to update a directory’s list of children. This requires finding a node by name in a list, removing it, and possibly replacing it with a new node. The following helper method is defined for this purpose:

```
// inside class Dir
def removeByName(name: String): Option[Node, List[Node]] =
  nodes.partition(_.name == name) match
    case (Nil, _)             => None
    case (List(found), others) => Some((found, others))
```

Higher-order method `partition` is used to partition a list of nodes between those that have a given name (there is at most one) and those that have a different name. If there is no node with the given name, the function returns None. Otherwise, it returns a pair with the node that was extracted and a list of remaining nodes. As an example, if you look for name B in a list of nodes that contains directories/files A, B, C, and D, the method returns the pair: `(B, [A,C,D])`.

## 11.3 String Representation

Both files and directories define a `toString` method that returns their name. To help distinguish between files and directories, a trailing slash is added to directory names:

```
// inside class Dir
override def toString = name + "/"

// inside class File
override def toString = name
```

Directories also define a method `ls` that lists their contents by name, and a method `lsFiles` that only lists the names of files, ignoring subdirectories. You can implement

ls by using the higher-order method map to produce a list of strings from a list of nodes. For lsFiles, you use flatMap to keep the names of files and skip subdirectories:

```
// inside class Dir
def ls: List[String] = nodes.map(_.toString)

def lsFiles: List[String] = nodes.flatMap {
  case file: File => List(file.toString)
  case _ => Nil
}
```

In addition to ls and lsFiles, you may want to build a string that represents the entire contents of the directory, including subdirectories. To emphasize the tree structure, file and directory names are indented according to their depth. Figure 11.1 shows a file system tree and its string representation.

![](img/74309e2bdd93f68d2e94338a3d73517f_197_0.png)

# Figure 11.1 A file system tree and its string representation.

To implement this method efficiently, you can create a string builder and use recursion to add lines to it, one line for each file and directory in the tree. To achieve indentation, each line starts with a prefix that consists of a repetition of a separator (the separator is a single dot in Figure 11.1). A method mkString allocates a string builder and an empty prefix and delegates the recursion to another method, also named mkString, whose responsibility is to add lines to the builder:

```
// inside trait Node
def mkString(sep: String): String = mkString(sep, StringBuilder(), "").result()
def mkString(sep: String, builder: StringBuilder, prefix: String): StringBuilder
```

Method flatMap is used here to combine filtering (keep files, ignore directories) and mapping (transform files into their names). Alternatively, lsFiles could be written in terms of filter and map.

This is similar to the tree command often found on Unix systems.
