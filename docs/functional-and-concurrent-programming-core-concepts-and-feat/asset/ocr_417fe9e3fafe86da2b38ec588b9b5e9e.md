The list of nodes in a directory should never contain two nodes with the same name. The order of nodes in a list is irrelevant: Directories that contain the same files and sub-directories in different orders are considered equivalent. Trees are immutable: Adding or removing files and directories is achieved via functions that produce a new tree.

# 11.2  A Node-Searching Helper Function

Several tree operations need to update a directory’s list of children. This requires finding a node by name in a list, removing it, and possibly replacing it with a new node. The following helper method is defined for this purpose:

```
```scala
// inside class Dir
def removeByName(name: String): Option[Node, List[Node]] =
  nodes.partition(_.name == name) match
    case (Nil, _)             => None
    case (List(found), others) => Some((found, others))
```
```

Higher-order method `partition` is used to partition a list of nodes between those that have a given name (there is at most one) and those that have a different name. If there is no node with the given name, the function returns None. Otherwise, it returns a pair with the node that was extracted and a list of remaining nodes. As an example, if you look for name B in a list of nodes that contains directories/files A, B, C, and D, the method returns the pair: `(B, [A,C,D])`.

# 11.3  String Representation

Both files and directories define a `toString` method that returns their name. To help distinguish between files and directories, a trailing slash is added to directory names:

```
```scala
// inside class Dir
override def toString = name + "/"

// inside class File
override def toString = name
```
```

Directories also define a method `ls` that lists their contents by name, and a method `lsFiles` that only lists the names of files, ignoring subdirectories. You can implement