

## 54 字符串搜索

```csharp
bool isUppercase = true; // 假设它是全大写的。
foreach(char c in favoriteFood)
{
    if(!char.IsUpper(c)) {
        isUppercase = false; // 证明不是全大写，所以退出。
        break;
    }
}
```

在循环结束时，isUppercase 将为 true 或 false。

正如在上一节关于切换大小写转换（switching case）的最后一个示例所示，你可以使用索引表示法访问字符串中的单个字符。

数组从零开始，所以如果你想要获取第一个字符，就请求 [0]。如果你想要第三个字符，就请求 [2]。

```csharp
char thirdChar = favoriteFood[2]; // "cheesurgers" 中的第一个 'e'
```

## 搜索字符串

如果你需要在字符串内部查找特定的单词或字符，你可能需要它的索引，这样你就可以对其使用 `Substring()`、`Replace()`、`Remove()` 或其他方法。在本节中，你将看到如何查找单个字符或子字符串。（我仍然在使用上一节中的 `favoriteFood` 变量。）

## 我能找到它吗？

简单的方法是使用 `IndexOf()` 查找单个字符：

```csharp
int indexOfLetterS = favoriteFood.IndexOf('s'); // 4.
```

`String` 类还有其他方法用于查找内容，可以是单个字符或子字符串：

- `IndexOfAny` 接收一个字符数组并在字符串中搜索其中任何一个字符，返回找到的第一个字符的索引。

```csharp
char charsToLookFor = { 'a', 'b', 'c' };
int indexOfFirst = favoriteFood.IndexOf(charsToLookFor); // 0.
```

这通常有更简洁的写法：

```csharp
int index = name.IndexOf(new char[] { 'a', 'b', 'c' });
```

- `IndexOf()` 找到不是字符的第一次出现，而是最后一次。

- `IndexOfAny()` 的工作原理与 `IndexOfAny()` ，但从字符串末尾开始。

![](img/36596fb11aa4233d5cab0d6ddd1d82e_79_0.png)

## 从命令行获取输入

- `Contains()` 如果在目标字符串中找到指定的子字符串，则返回 true：

```csharp
if(favoriteFood.Contains("*ee")) // True
```

- 而 `Substring()` 返回该字符串（如果存在）或空（如果不存在）：

```csharp
string sub = favoriteFood.Substring(6, favoriteFood.Length - 6);
```

（我将在本章稍后的部分更详细地介绍 `Substring()`。）

## 我的字符串是空的吗？

你如何判断一个目标字符串是否为空（""）：

```csharp
bool notThere = string.IsNullOrEmpty(favoriteFood); // False
```

注意你是如何调用 `IsNullOrEmpty()` 的：**string.IsNullOrEmpty(s)****

你可以通过两种方式设置空字符串：

```csharp
string name = "";
string name = string.Empty;
```

## 从命令行获取输入

控制台应用程序中的常见任务是，当你向用户提示（例如请求利率或名称）时，获取用户使用的信息。你需要读取以字符串形式传入的信息（来自命令行的所有内容都是字符串）。然后，你需要对输入进行解析，从中提取出数字。有时你还需要处理输入的数字。

## 修剪多余的空白

首先，考虑到在某些情况下，你不想干扰字符串两端的任何空白。“空白”一词指的是通常不在屏幕上显示的字符，例如空格、换行符 (\n) 和制表符 (\t)。你还可能遇到回车符字符 \r。

你可以使用 `Trim()` 方法来修剪字符串的边缘，如下所示：

```csharp
// 去除字符串两端的任何额外空格。
random = random.Trim();
```

## 56 从命令行获取输入

`String` 类还提供了 `TrimFront()` 和 `TrimEnd()` 方法进行更特定的修剪，并且你可以传递一个字符数组，将其与空白一起包含在修剪中。例如，你可能会修剪开头的货币符号，如 '$'。清理字符串可以使解析更容易。修剪方法返回一个新字符串。

## 解析数字输入

程序可以一次从键盘读取一个字符，但你必须担心换行等问题。一种更容易的方法是读取一个字符串并从字符串中解析字符。

从字符串解析字符是另一个我不喜欢提到的话题，因为担心程序员会滥用这种技术。在某些情况下，程序员太急于跳到字符串中间并提取出他们找到的内容。这对于 C++ 程序员来说尤为如此，因为那是他们处理字符串的唯一方法——直到字符串类的加入。

用于从控制台读取的 `ReadLine()` 方法返回一个字符串对象。期望数字输入的程序必须在 `Convert` 类中转换你需要的字符串。该类提供了从字符串到每个内置变量类型的转换方法。因此，这段代码从键盘读取一个数字并将其存储在 `int` 变量中：

```csharp
string s = Console.ReadLine(); // 键盘输入是字符串数据
int n = Convert.ToInt32(s); // 但你知道它应该是一个数字。
```

其他转换方法更明显一些：`ToDouble()`、`ToFloat()` 和 `ToBoolean()`。

`ToInt32()` 指的是32 位整数。`ToInt64()` 指的是 64 位整数。`ToDouble()` 指的是双精度数。`ToFloat()` 指的是单精度数。`ToBoolean()` 指的是布尔值。

用于从控制台读取的 `ReadLine()` 方法返回一个字符串对象。期望数字输入的程序必须在 `Convert` 类中转换你需要的字符串。该类提供了从字符串到每个内置变量类型的转换方法。因此，这段代码从键盘读取一个数字并将其存储在 `int` 变量中：

```csharp
string s = Console.ReadLine(); // 键盘输入是字符串数据
int n = Convert.ToInt32(s); // 但你知道它应该是一个数字。
```

