
```scala
// inside class File
def fileExists(test: File => Boolean): Boolean = test(this)
def dirExists(test: Dir => Boolean): Boolean  = false
```

### 清单 11.5：在通用树上实现 exists 的示例。

方法 `fileExists` 接受一个布尔函数作为参数，如果树中至少有一个文件满足该测试函数，则返回 `true`。也就是说，如果存在一个节点，其中存在这样的文件，则该结果为 `true`。因此，在目录上实现 `fileExists` 时，你可以依赖列表的 `exists` 方法来检查所有节点，并在每个节点上递归调用 `fileExists` 方法本身。对于文件，`fileExists` 只是将测试应用于该文件。

方法 `dirExists` 的实现类似。它接受一个作用于目录而非文件的布尔函数，并先将其应用于当前目录（`test(this)`），然后像之前一样使用 `exists` 检查各个节点。对于文件，此方法始终返回 `false`。

通过利用递归和列表的 `exists` 方法，在树上实现 `fileExists` 和 `dirExists` 各只需两行。同样，你还可以实现树折叠函数，将递归与列表的 `foldLeft`（或 `foldRight`，因为目录中节点的顺序无关紧要）方法结合起来：

```scala
// inside class Dir
def fileFold[A](init: A)(f: (A, File) => A): A =
    nodes.foldLeft(init)((acc, node) => node.fileFold(acc)(f))

def dirFold[A](init: A)(f: (A, Dir) => A): A =
    nodes.foldLeft(f(init, this))((acc, node) => node.dirFold(acc)(f))

// inside class File
def fileFold[A](init: A)(f: (A, File) => A): A = f(init, this)
def dirFold[A](init: A)(f: (A, Dir) => A): A = init
```

### 清单 11.6：在通用树上实现 fold 的示例。

你通过逐个折叠目录的所有子节点来折叠目录。当你折叠处理文件的函数时，子节点的折叠从 `init` 开始；但当你折叠处理目录的函数时，它从 `f(init, this)` 开始，以便在遍历子节点之前先处理当前目录。（清单 11.4 中 `fileCount` 和 `dirCount` 的 0 和 1 背后也是同样的原理。）对于文件节点，`fileFold` 将给定函数 `f` 应用到这个文件，而 `dirFold` 保持折叠累加器不变。

方法 `fileFold` 和 `dirFold` 功能强大，可用于实现各种文件系统查询。例如，如果 `fileCount` 和 `dirCount` 尚未作为 `Dir` 类的方法实现，你可以改用 `fileFold` 和 `dirFold` 来编写它们：

```scala
def fileCount(dir: Dir): Int = dir.fileFold(0)((acc, _) => acc + 1)
def dirCount(dir: Dir): Int = dir.dirFold(0)((acc, _) => acc + 1)
```

你还可以使用 `fileFold` 查找树中最长的文件名：[^5]

```scala
def longestFilename(dir: Dir): String = dir.fileFold("") { (longest, file) =>
  if file.name.length > longest.length then file.name else longest
}
```

同样，你可以使用 `dirFold` 构建文件系统中所有文件名的列表：

```scala
def allFileNames(dir: Dir): List[String] =
  dir.dirFold(List.empty[String])((list, subdir) => subdir.lsFiles ::: list)
```

然而要小心：折叠函数并不适合实现搜索，因为它们总是遍历整棵树，[^6] 即使已经找到元素也是如此。例如，下面这个 `fileFind` 方法的实现是不可取的：

```scala
// DON'T DO THIS!

// inside class Dir
def fileFind(test: File => Boolean): Option[File] =
  fileFold(Option.empty[File]) { (found, file) =>
    found.orElse(if test(file) then Some(file) else None)
  }
```

此方法的缺点是，在找到合适的文件后，它仍会继续遍历树。[^7]

要让 `fileFind` 在找到文件后停止，同时保持函数式编程风格，并不是一件直截了当的事。鉴于我们使用列表的 `exists` 实现了 `fileExists`，使用列表的 `foldLeft` 实现了 `fileFold`，你可能会想使用列表的 `find` 来实现 `fileFind`。问题是，对子树列表应用 `find` 会产生一棵（如果有的话）可以找到所需文件的树，而不是文件本身。你需要再次使用 `fileFind` 搜索这棵树，才能提取出文件：

```scala
// DON'T DO THIS!

// inside class Dir
def fileFind(test: File => Boolean): Option[File] =
  nodes.find(_.fileExists(test)).map(_.fileFind(test).get)
```

该实现使用 `find` 搜索包含所需文件的节点。如果找到，就对 Option 调用 `map`，在此节点上应用 `fileFind` 以获取实际文件。这是不可取的，因为 Option 中的节点已经被搜索过该文件，而且确实包含它（对 `fileFind` 的调用保证会成功，因此使用 `get` 来获取实际文件）。于是该节点被搜索了两次，而且由于 `fileFind` 的递归性质，内部节点最终会被多次搜索（节点越深，被搜索的次数越多）。

与其使用 `find` 来定位包含合适文件的子树，更好的策略是利用列表的 `map` 方法从每个子树中提取所需文件。表达式 `nodes.map(_.fileFind(test))` 的类型是 `List[Option[File]]`，为每个子树包含一个可接受的文件（如果有的话）。然后可以使用 `find` 方法从列表中找到非空 Option。表达式 `nodes.map(_.fileFind(test)).find(_.nonEmpty)` 会产生所需的文件，但得到的是 `Option[Option[File]]`，可以被展平：

```scala
// DON'T DO THIS!

// inside class Dir
def fileFind(test: File => Boolean): Option[File] =
  nodes.map(_.fileFind(test)).find(_.nonEmpty).flatten
```

这种方法的问题在于，`map` 无论如何都会处理整个节点列表，而且目录中的所有节点都会被搜索，即使已经找到了文件。避免这个问题的标准技术是引入某种形式的惰性求值：

```scala
// OK, but can be improved

// inside class Dir
def fileFind(test: File => Boolean): Option[File] =
  nodes.view.map(_.fileFind(test)).find(_.nonEmpty).flatten
```

通过对 `nodes.view` 而不是 `nodes` 调用高阶方法 `map`，你可以在找到文件后防止继续探索节点。惰性求值将在第 12 章详细讨论。目前，只需知道示例中的实现在找到第一个文件时停下（如果没有找到文件，则遍历整棵树）。

你可以用对 `flatMap` 的调用来替换 `map`/`flatten` 组合，从而生成所有解包后的文件，而不是让它们位于 Option 中。最终，`fileFind` 和 `dirFind` 的期望实现如下：[^8]

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

表达式 `nodes.view.flatMap(_.fileFind(test))` 生成一个（惰性求值的）文件集合，其中包含满足给定测试的文件，每个子树对应一个。调用 `headOption` 会强制对视图进行求值，直到找到文件，或者视图已经穷尽而没有产生文件。

## 11.6 导航

类 `Dir` 和 `File` 中的最后一组方法涉及文件系统内的导航。你可以定义一个 `cd` 方法来进入子目录，它模仿同名的 Unix 命令：

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

[^5]: 该函数体也可以写成 `Seq(file.name, longest).maxBy(_.length)`。

[^6]: 除非抛出异常。抛出（并捕获）异常有时被用作提前终止折叠计算的技术。

[^7]: 尽管所有文件都会被访问，但此实现会在找到文件后停止应用测试函数。这是因为，当 `orElse` 应用于非空 Option 时，作为其参数的表达式不会被求值。这种现象被称为惰性求值或延迟求值，将在第 12 章中探讨。

[^8]: 类 `File` 中 `fileFind` 的函数体可以写成 `Some(this).filter(test)`，而不是 `if test(this) then Some(this) else None`。代码中还有其他地方也可以对 Option 应用 `filter`。虽然这会说明高阶方法 `filter` 的用法，但可能会损失一些代码可读性。为了清晰起见，我选择坚持使用 `if–then–else`。

