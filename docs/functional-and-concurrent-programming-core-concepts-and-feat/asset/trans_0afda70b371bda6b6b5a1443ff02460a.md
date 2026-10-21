

```scala
def cd(name: String, names: String*): Dir = cdPath(name :: names.toList)

// inside class File
def cdPath(path: List[String]): Dir =
    throw FileSystemException(name, "cannot change: not a directory")
```

正如之前对 mkFile、mkDir 和 rm 所做的那样，方法 cd 是通过一个辅助方法 cdPath 实现的，该方法遍历由名称指定的目录列表。如果名称列表为空，则返回当前目录。否则，使用 find 查找具有指定名称的子目录（如果有）。使用 getOrElse，从 resulting option 中提取目录，或在 option 为空时抛出异常。然后将路径的剩余部分递归地应用于子目录。如果在任何时候路径遇到文件而不是目录，则会抛出异常。

## 11.7 Tree Zipper

方法 cd 可用于向下遍历树。向上返回呢？必须认识到问题不在于在遍历时 somehow 保留对包含树的引用。原因在于树是不可变的，添加或删除文件或子目录会产生一棵新树。在此类修改之后，返回包含子树的树在其修改之前的状态是没有意义的。你需要实现的方法是 up 和 down，使得以下代码产生的与图 11.1 中的文件系统相同：

```scala
Dir("Root").nav
.mkDir("Dir2")
.down("Dir2")
.mkFile("File3")
.up
.mkDir("Dir1")
.down("Dir1")
.mkDir("Dir3")
.mkFile("File2")
.up
.mkFile("File1")
.dir
```

请注意，例如第一次调用方法 up 不能简单地返回到 down("Dir2") 所调用的树，因为该树不包含 File3。换句话说，up 不一定会带你回到之前的树，在某些情况下还需要创建新树。

一种可行的办法是将树类型修改为 zipper。第 5.6 节实现了用于在列表中向左和向右导航的 zipper。相同的思想可用于在树中上下移动。⁹ Zippers 是不可变的。树 zipper 将子树与导致该子树的步骤序列结合起来。这些步骤可以按相反顺序重新应用以向上移动。与返回现有树不同，应用步骤会构建一棵新树，其中包含反映文件系统修改的更新子树。在前面的代码中，调用 nav 将文件系统的类型从树更改为树 zipper，该 zipper 通过其 up 和 down 方法实现导航。最后一次调用 dir 会带你回到常规树。

要向下进入子目录，你创建一个包含父目录名称以及该目录中所有其他节点的步骤。例如，进入图 11.1 中文件系统中的 Dir1 会返回以 Dir1 为根的子树，但也会创建一个包含名称 Root 和除 Dir1 之外的子树列表的步骤：

![](img/74309e2bdd93f68d2e94338a3d73517f_208_0.png)

你可以看到，从子树（标记为 3）、步骤名称（标记为 1）和步骤树（标记为 2a 和 2b）可以重建之前的树以向上移动。如果子树已被更改——即被不同的树替换——通过重新组装向上移动会产生不同的树（相同的 1 和 2 部分，但子树 3 不同）。

zipper 在类 DirNav 中实现：

```scala
final class DirNav (val dir: Dir, steps: List[(String, List[Node])]):
...
```

zipper 由当前目录（dir）和导致它的向下步骤列表（steps）组成。每个步骤是一对，包含父节点的名称作为 String，以及当前目录的兄弟节点列表，类型为 List[Node]。当当前目录是文件系统的根时，步骤列表为空。

zipper 实现两个方法 up 和 down。要向下移动到子目录，方法 down 会产生与之前的 cd 方法相同的子目录，但会在步骤列表中添加一个步骤，以便方法 up 可以通过该步骤逆向向下移动而向上返回：

⁹本节仅考虑上下移动。更复杂的 zipper 可以编写以在兄弟节点之间向左和向右移动。

```scala
// inside class DirNav
def down(dirname: String): DirNav =
    dir.removeByName(dirname) match
    case None =>
        throw FileSystemException(dirname, "cannot change: no such directory")
    case Some((file: File, _)) =>
        throw FileSystemException(dirname, "cannot change: not a directory")
    case Some((subdir: Dir, otherNodes)) =>
        DirNav(subdir, (dir.name, otherNodes) :: steps)

def up: DirNav = steps match
    case Nil => this
    case (name, nodes) :: more => DirNav(Dir(name, dir :: nodes), more)
```

列表 11.8：树 zipper 中的导航方法（1）。

要向下移动，按名称搜索目标子目录并将其从节点列表中移除。如果未找到，或按该名称找到文件而不是目录，则抛出异常。否则，如果子目录存在（subdir），则通过添加新步骤创建包含它的 zipper。此步骤包含父目录的名称（dir.name）和 subdir 的所有兄弟节点（otherNodes）。新步骤添加到步骤列表的前面，该列表像栈一样使用。要向上返回，方法 up 从栈中弹出第一个步骤，并使用其名称和节点列表构造一棵新树 Dir(name, dir :: nodes)，该树被包装在具有剩余步骤的 zipper 中。

为了方便，你还可以实现一个方法用于多次向下移动，以及一个方法用于返回到树的根：

```scala
// inside class DirNav
def down(dirname1: String, dirname2: String, dirnames: String*): DirNav =
    (dirname1 :: dirname2 :: dirnames.toList).foldLeft(this)(_.down(_))
@tailrec
def top: DirNav = if steps.isEmpty then this else up.top
```

列表 11.9：树 zipper 中的导航方法（2）。

要向下移动由多个子目录组成的路径，你使用 foldLeft 并以当前目录作为初始值，对路径中的所有名称逐一调用单名称变体的 down 方法。要一直移动到顶部，方法 top 反复应用 up 直到到达树的根。

类 DirNav 的所有其他方法都是通过转发调用到类 Dir 中的对应方法实现的，除了创建方法（添加和删除文件和子目录）需要返回可导航的目录而不是普通目录：

```scala
// inside class DirNav
override def toString = dir.toString

def mkFile(name: String, names: String*): DirNav =
    DirNav(dir.mkFile(name, names*), steps)

def mkDir(name: String, names: String*): DirNav =
    DirNav(dir.mkDir(name, names*), steps)

def rm(name: String, names: String*): DirNav =
    DirNav(dir.rm(name, names*), steps)

export dir.{
    mkString, ls, lsFiles,
    dirCount, dirExists, dirFold, dirFind, fileCount, fileExists, fileFold, fileFind
}
```

最后，一个方法 nav 被添加到类 Dir 以使普通目录可导航：

```scala
// inside class Dir
def nav: DirNav = DirNav(this, List.empty)
```

## 11.8 Summary

在本章中，文件系统表示为文件和目录的树。目录的内容存储为节点列表，并使用列表的高阶方法有效地处理这些节点。树还定义了自己的高阶方法。它们是递归实现的，并且对子目录的递归调用使用列表的高阶方法在目录的内容上执行。最后，树被扩展为 zippers 以便可导航，具有向下进入子目录和向上返回父目录的方法。总计（包括许多脚注），本文件系统案例研究使用和/或重新实现了标准高阶方法 exists、find、flatMap、foldLeft、foreach、filter、map、maxBy 和 partition。

## Chapter 12

## Lazy Evaluation

通过将函数用作值，可以用计算该数据的函数替换数据。通过这种方法，可以推迟参数的求值直到需要时，从而可以将未求值的代码传递给方法和函数。结合语言的语法帮助，可以从编程语言内部定义额外的控制结构，从而可能定义内部领域特定语言。函数也可以存储在数据结构中以推迟该结构部分求值。流是经典的函数式编程结构，实现延迟求值的序列。除了未求值参数和延迟数据结构之外，延迟求值还可以采用其他几种形式，例如延迟高阶函数求值的视图以及变量延迟初始化的机制。

我们已经看到高阶函数可以接受本身就是函数的参数。通过用计算该参数的函数替换显式参数，例如字符串，可以推迟字符串的计算直到其值需要时。

```scala
val logger: Logger = ...

logger.info("incoming request from ${ip.getHostName} (${ip.getAddress})")
```

这种方法的缺点是字符串参数总是被构建，即使在 INFO 级别日志被禁用时也是如此。在此示例中，如果日志设置为 WARNING 级别，仍然会进行可能代价高昂的主机名查找来创建随后立即丢弃的字符串。

Java 8 为 Logger 类引入了第二个 info 方法。它用返回字符串的函数替换字符串参数：

```scala
logger.info(() => "incoming request from ${ip.getHostName} (${ip.getAddress})")
```

