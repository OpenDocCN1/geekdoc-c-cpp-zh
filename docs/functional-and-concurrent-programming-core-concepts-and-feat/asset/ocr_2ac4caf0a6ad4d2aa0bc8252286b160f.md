The implementation of this second mkString method is straightforward inside class File. You simply add to the builder a line that consists of the prefix followed by the file name and a newline:

```
// inside class File
def mkString(sep: String, builder: StringBuilder, prefix: String): StringBuilder =
  builder += prefix += name += '\n'
```

Inside the Dir class, the method starts by adding a line for the directory itself. It then proceeds by adding all the nodes (files and subdirectories) inside the directory. This is achieved recursively by calling mkString on all the nodes, using a longer prefix and the same string builder. You can perform these recursive calls by applying higher-order method foreach on the list of nodes:

```
// inside class Dir
def mkString(sep: String, builder: StringBuilder, prefix: String): StringBuilder =
  builder += prefix += name += "/\n"
  val newPrefix = prefix + sep
  nodes.foreach(_ .mkString(sep, builder, newPrefix))
  builder
```

Listing 11.1: Example of using foreach with a mutable string builder.

Method mkString mixes higher-order functions and recursion: The action applied by foreach invokes mkString, which uses foreach to invoke mkString, and so on. This is a consequence of the fact that a node contains a list (hence the use of higher-order functions) of nodes (hence the use of recursion). You will notice how this pattern is used again in other tree functions in this chapter.

As mentioned earlier, method foreach makes sense only when the function being applied has a side effect. Here, the side effect comes from modifying a mutable string builder. Tree users, however, would call only the first mkString method—the only one public in an actual implementation. From their standpoint, the function is pure and produces a string from a tree, without any observable side effects.

# 11.4 Building Trees

The constructor of the Dir class makes it possible to build invalid directories that contain multiple nodes with the same name. In practice, this constructor would not be public. Instead, you would provide public methods to create empty directories and to add files and subdirectories to an existing directory.

Inside the companion object of the Dir class, you can define a function that creates an empty directory: