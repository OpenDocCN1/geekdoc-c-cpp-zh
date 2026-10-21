You can replace the `map/flatten` combination with a call to `flatMap` to produce all the files unwrapped instead of being inside options. In the end, the desired implementations of `fileFind` and `dirFind` are as follows:

```
```scala
// inside class Dir
def fileFind(test: File => Boolean): Option[File] =
  nodes.view.flatMap(_.fileFind(test)).headOption

def dirFind(test: Dir => Boolean): Option[Dir] =
  if test(this) then Some(this) else nodes.view.flatMap(_.dirFind(test)).headOption

// inside class File
def fileFind(test: File => Boolean): Option[File] =
  if test(this) then Some(this) else None

def dirFind(test: Dir => Boolean): Option[Dir] = None
```
```

The expression `nodes.view.flatMap(_.fileFind(test))` produces a (lazily evaluated) collection of files that satisfies the given test, one for each subtree. Invoking `headOption` forces the view to be evaluated until either a file is found or the view has been exhausted without producing a file.

# 11.6 Navigation

A last set of methods in classes `Dir` and `File` deal with navigation inside a file system. You can define a method `cd` to enter subdirectories, which mimics the Unix command by the same name:

```
```scala
// inside class Dir
def cdPath(path: List[String]): Dir = path match
  case Nil => this
  case dirname :: more =>
    nodes
      .find(_.name == dirname)
      .getOrElse(throw FileSystemException(dirname, "cannot change: no such dir"))
      .cdPath(more)
```
```

> ⁸Instead of `if test(this) then Some(this) else None`, the body of `filterFind` in class `File` could be written `Some(this).filter(test)`. There are other places in the code where `filter` could also be applied to options. Although this would illustrate the use of higher-order method `filter`, some code readability might be lost. I chose to stick with `if–then–else` for clarity.