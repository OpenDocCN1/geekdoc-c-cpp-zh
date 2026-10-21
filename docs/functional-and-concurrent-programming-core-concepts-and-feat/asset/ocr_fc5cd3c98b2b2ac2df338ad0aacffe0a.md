# 11.7 Tree Zipper

```
```scala
// inside class DirNav
def down(dirname: String): DirNav =
    dir.removeByName(dirname) match
    case None =>
        throw FileSystemException(dirname, "cannot change: no such directory")
    case Some(file: File, _) =>
        throw FileSystemException(dirname, "cannot change: not a directory")
    case Some(subdir: Dir, otherNodes) =>
        DirNav(subdir, (dir.name, otherNodes) :: steps)

def up: DirNav = steps match
    case Nil => this
    case (name, nodes) :: more => DirNav(Dir(name, dir :: nodes), more)
```
```

# Listing 11.8: Navigation methods in a tree zipper (1).

To go down, search the target subdirectory by name and remove it from the list of nodes. If it is not found, or if a file is found by that name instead, throw an exception. Otherwise, if the subdirectory exists (subdirir), create a zipper with it by adding a new step. This step contains the name of the parent directory (dir.name) and all the siblings of subdir (otherNodes). The new step is added at the front of the list of steps, which is used like a stack. To go back up, method up pops the first step from the stack and uses its name and list of nodes to construct a new tree Dir(name, dir :: nodes), which is wrapped in a zipper with the remaining steps.

For convenience, you can also implement a method to go down multiple times and a method to go back to the root of the tree:

```
```scala
// inside class DirNav
def down(dirname1: String, dirname2: String, dirnames: String*): DirNav =
    (dirname1 :: dirname2 :: dirnames.toList).foldLeft(this)(_down(_))
@tailrec
def top: DirNav = if steps.isEmpty then this else up.top
```
```

# Listing 11.9: Navigation methods in a tree zipper (2).

To go down a path made of multiple subdirectories, you use foldLeft with the current directory as the initial value to invoke the single-name variant of method down on all the names in the path, one by one. To move all the way to the top, method top repeatedly applies up until the root of the tree is reached.