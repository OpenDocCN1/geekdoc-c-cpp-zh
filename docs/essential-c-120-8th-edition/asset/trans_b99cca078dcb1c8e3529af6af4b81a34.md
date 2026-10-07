

# C# 语法基础 13

语句（statement）由代码将执行的一个或多个操作组成。声明变量、控制程序流和调用方法都是语句的典型用法。

## 高级主题

### 不带分号的语句
C# 中的许多编程元素以分号结尾。其中一个不包含分号的例子是 `switch` 语句。由于 `switch` 语句始终包含大括号，因此 C# 不需要在此语句后加分号。事实上，代码块本身被视为语句（它们也由语句组成），并且它们不需要以分号结束。同样，在某些情况下（例如使用声明时），分号作为后缀出现，但它并不是一个语句。

由于换行符不会分隔语句，你可以将多个语句放置在同一行上，C# 编译器会将该行解释为包含多条指令。例如，列表 1.3 在单行上包含两个语句，它们结合在一起在两个单独的行显示 Up 和 Down。

# 列表 1.3：单行内的多个语句

```
Console.WriteLine("Up"); Console.WriteLine("Down");
```

同样，每个语句都可以放在单独的一行上，如列表 1.4 所示。

# 列表 1.4：每个语句单独占一行

```
Console.WriteLine("Down");
Console.WriteLine("Side");
Console.WriteLine("Up");
```

C# 还允许将一个语句拆分跨多行。同样，C# 编译器会寻找分号来指示语句的结束。例如，在列表 1.5 中，HelloWorld 程序中的原始 `WriteLine()` 语句被分成了多行。

# 14 第 1 章：引入 C#

### 列表 1.5：跨多行的单个语句

```
Console.WriteLine(
  "Hello. My name is Inigo Montoya.");
```

## 引入类和方法

在目前为止所示的列表中，语句独立于任何其他 C# 构造，并且仅在单个文件中以这种方式出现。毕竟，之前的列表是 C# 程序中最简单的程序，即一个 HelloWorld 程序。然而，程序可能会变得非常复杂，可以添加结构来组织代码。最简单的结构是添加方法并将这些方法放在类中。列表 1.6 提供了一个示例。

### 列表 1.6：带有类和方法的 HelloWorld

```
public class Program
{
  public static void Main()
{
    System.Console.WriteLine("Hello. My name is Inigo Montoya.");
  }
}
```

在这个列表中，HelloWorld 语句被放在一个名为 Main 的方法中，该方法又放在一个名为 Program 的类中。

具有 Java、C 或 C++ 编程经验的人会立即看到相似之处。与 Java 一样，C# 从 C 和 C++ 继承了它的基本语法。语法标点（如分号和大括号）、特性（如大小写敏感）和关键字（如 `class`、`public` 和 `void`）对于习惯于这些语言的程序员来说是熟悉的。

- 8. 在创建 C# 时，语言创建者审查了 C/C++ 的规范，字面上划掉了他们不喜欢的特征，并创建了他们喜欢的特征列表。该小组还包括在其他语言方面有深厚背景的设计师。

# C# 语法基础 15

> **注意**
> C# 是一种大小写敏感的语言：错误的大小会导致代码无法成功编译。

## 语言对比：Java—文件名必须与类名匹配

在 Java 中，文件名必须与类名匹配。在 C# 中，这并不是要求的。

## 初学者主题

### 关键字
为了让编译器识别代码，某些词具有特殊状态。作为**关键字**，它们在 C# 中具有特殊含义。在 HelloWorld 程序中，`class`、`static` 和 `void` 是关键字的示例。

编译器使用关键字来识别结构。在 C# 中，某些词在特定位置具有重要性。在这些位置之外，它们没有特殊意义。

# C# 关键字
关键字是另一种语言的构造。表 1.1 显示了关键字。

# 16 第 1 章：引入 C#

| 表 1.1：C# 关键字 | | |
|---|---|---|
| abstract | alias* | async |
| await | base | bool |
| by | byte | break |
| char | checked | class |
| continue | decimal | default |
| else | enum | equals |
| finally | fixed | float |
| foreach | from | for |
| goto | get | get |
| in | init | int |
| internal | into | is |
| let | lock | long |
| namespace | new | not |
| null | object | operator |
| on | override | out |
| private | protected | public |
| record | ref | readonly |
| remove | required | return |
| set | sealed | short |
| stackalloc | static | string |
| switch | this | throw |
| try | typeof | uint |
| unchecked | unsafe | ushort |

* 上下文关键字。括号中的数字表示添加添加的版本。

在 C# 1.0 之后，C# 没有引入新的保留关键字。然而，后续版本的某些构造使用了上下文关键字。在这些指定位置之外，上下文关键字没有特殊意义。9 通过这种方法，即使是 C# 1.0 代码也是兼容的10

# 标识符

与其他语言一样，C# 包含标识符来标识构造。在列表 1.6 中，HelloWorld 和 Main 是标识符的示例。分配给构造的标识符稍后会被引用，因此开发者分配的名称是有意义的而非任意的。

> 注意
> 选择简洁且指示性的名称是优秀程序员的一个重要特征，因为这意味着生成的代码更容易被理解和重用。

清晰性与一致性足够重要，以至于框架设计指南（http://bit.ly/dotnetguidelines）建议不要在标识符名称中使用缩写或复合词。如果一个缩写被广泛接受（例如 HTML），你应该始终使用它。避免在某些情况下写出接受的缩写而在其他情况下不写。通常情况下，将所有缩写包含在术语表中比使用缩写的开销要小

- 9. 例如，在 C# 2.0 的设计中，语言设计者将 `yield` 指定为关键字，微软发布了 C# 2.0 编译器的 Alpha 版本，并将 `yield` 作为关键字提供给数千名开发者。然而，语言设计者最终确定通过使用 `return` 而不是 `yield`，最终可以避免将 `yield` 作为关键字，因为它除了靠近 `return` 之外没有特殊意义。一些罕见且不幸的不兼容性，例如：C# 2.0 要求使用 `using` 语句实现 `IDisposable`，而不是简单地使用 `Dispose()` 方法。

