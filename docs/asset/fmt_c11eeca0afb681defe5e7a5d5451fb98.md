
`stringVar.IndexOf(substring, start)` `stringVar` 是字符串变量或字符串表达式。参数 `substring` 是字符串，参数 `start` 是整数。该方法从 `start` 指定的位置开始到 `stringVar` 的末尾搜索 `stringVar`。如果在 `stringVar` 的该部分找到了 `substring`，则该方法返回其第一次出现的整数位置。如果未找到 `substring`，则方法返回 `-1`。

## 8.2 字符串与字符处理

| 方法 | 说明 |
| --- | --- |
|  | 示例:  
```
// 以下代码显示 "2"
string str = "cocoa beans";
int position = str.IndexOf("co", 2);
if (position != -1)
{
  MessageBox.Show(position.ToString());
}else
  MessageBox.Show("未找到 co.");
``` |

`stringVar.IndexOf(substring, start, count)` `stringVar` 是字符串变量名或字符串表达式。参数 `substring` 是一个字符串，参数 `start` 是一个整数，参数 `count` 也是一个整数。该方法在 `stringVar` 中搜索 `substring`，从 `start` 指定的位置开始，并继续计数 `count` 个字符。如果在 `stringVar` 的这部分找到了 `substring`，则该方法返回其首次出现的整数位置。如果未找到 `substring`，则该方法返回 `-1`。

```c
Example:

// 以下代码显示 "6"

string str = "xx oo oo oo";

int position = str.IndexOf("xx", 3, 8);

if (position != -1)

{

  MessageBox.Show(position.ToString());

}else

  MessageBox.Show("未找到 xx.");

```
`stringVar.IndexOf(ch)` `stringVar` 是字符串变量名或字符串表达式。参数 `ch` 是一个字符。如果在 `stringVar` 中找到了 `ch`，则该方法返回 `ch` 首次出现的位置。如果在 `stringVar` 中未找到 `ch`，则该方法返回 `-1`。

```csharp
Example:

// 以下代码显示 "2"

string str = "chocolate ice cream";

int position = str.IndexOf("o");

if (position != -1)

{

  MessageBox.Show(position.ToString());

}else

  MessageBox.Show("未找到 o.");

```

## 表 8-4 获取字符或子字符串位置的方法（续表）

| 方法 | 说明 |
| --- | --- |
| `stringVar.IndexOf(ch, start)` | `stringVar` 是字符串变量名或字符串表达式。参数 `ch` 是一个字符，参数 `start` 是一个整数。该方法在 `stringVar` 中搜索 `ch`，从 `start` 指定的位置开始直到 `stringVar` 的末尾。如果在 `stringVar` 的此位置找到了 `ch`，则该方法返回其首次出现的整数位置。如果未找到 `ch`，则该方法返回 `-1`。  
示例:  
```csharp
// 以下代码显示 "4"
string str = "chocolate ice cream";
int position = str.IndexOf('o', 3);
if (position != -1)
{
    MessageBox.Show(position.ToString());
}
else
{
    MessageBox.Show("未找到 o.");
}
``` |
| `stringVar.IndexOf(ch, start, count)` | `stringVar` 是字符串变量名或字符串表达式。参数 `ch` 是一个字符，参数 `start` 是一个整数，`count` 也是一个整数。该方法在 `stringVar` 中搜索 `ch`，从 `start` 指定的位置开始并继续计数 `count` 个字符。如果在 `stringVar` 的此位置找到了 `ch`，则该方法返回其首次出现的整数位置。它返回 `-1`。  
示例:  
```csharp
// 以下代码显示 "12"
string str = "chocolate ice cream";
int position = str.IndexOf('e', 10, 4);
if (position != -1)
{
    MessageBox.Show(position.ToString());
}
else
{
    MessageBox.Show("未找到 e.");
}
``` |
| `stringVar.LastIndexOf(substring)` | `stringVar` 是字符串变量名或 `子字符串`。参数 `substring` 也是一个字符串。如果在 `stringVar` 中找到了 `substring`，则该方法返回 `substring` 最后一次出现的整数位置。如果 `stringVar` 中未找到 `substring`，则该方法返回 `-1`。  
示例:  
// 以下代码显示 "11"。  
string str = "blue green blue";  
int position = str.LastIndexOf("blue");  
if (position != -1) {  
    MessageBox.Show(position.ToString());  
} else {  
    MessageBox.Show("未找到 blue.");  
} |
| `stringVar.LastIndexOf(substring, start)` | `stringVar` 是字符串变量名或字符串表达式。参数 `substring` 是一个字符串，参数 `start` 是一个整数。该方法在 `stringVar` 中搜索 `substring`，从 `start` 指定的位置开始向 `stringVar` 的开头反向。如果在 `stringVar` 的这部分找到了 `substring`，则该方法返回其整数位置。如果未找到 `substring`，则该方法返回 `-1`。  
示例:  
```csharp
// 以下代码显示 "6"。
string str = "xx oo xx";
int position = str.LastIndexOf("xx", 10);
if (position != -1) {
    MessageBox.Show(position.ToString());
} else {
    MessageBox.Show("未找到 xx.");
}
``` |

| `stringVar.LastIndexOf(ch)` | `stringVar` 是字符串变量名或字符串表达式。参数 `ch` 是一个字符。如果在 `stringVar` 中找到了 `ch`，则该方法返回 `ch` 首次出现的位置。如果在 `stringVar` 中未找到 `ch`，则该方法返回 `-1`。  
示例:  
```csharp
// 以下代码显示 "14"
string str = "chocolate ice cream";
int position = str.LastIndexOf('c');
if (position != -1)
{
    MessageBox.Show(position.ToString());
}else
{
    MessageBox.Show("未找到 c.");
}
``` |
| `stringVar.LastIndexOf(ch, start, count)` | `stringVar` 是字符串变量名或字符串表达式。参数 `ch` 是一个字符，参数 `start` 是一个整数，参数 `count` 也是一个整数。该方法在 `stringVar` 中搜索 `ch`，从 `start` 指定的位置开始反向计数 `count` 个字符。如果在 `stringVar` 的这部分找到了 `ch`，则该方法返回其整数位置。如果未找到 `ch`，则该方法返回 `-1`。  
示例:  
```csharp
// 以下代码显示 "12"
string str = "chocolate cream";
int position = str.LastIndexOf('e', 14, 8);
if (position == -1) {
    MessageBox.Show(position.ToString());
} else {
    MessageBox.Show("未找到 e.");
}
``` |

有时你需要从字符串中提取特定的字符集。例如，假设一个字符串包含一个美国电话号码，如 `"919)555-1222"`，而你感兴趣的是获取区号。你需要一种方法获取位置 `I` 到 `3` 的字符。你可以使用 `Substring` 方法，如表 8-5 所示。注意 `Substring` 方法返回的是字符串。

## 表 8-5 Substring 方法

| 方法 | 说明 |
| --- | --- |
| `stringVar.Substring(start)` | `stringVar` 是字符串变量名或字符串表达式。参数 `start` 是指定 `stringVar` 中位置的整数。该方法返回一个从 `start` 开始、继续计数 `count` 个字符的字符串。 |
| `stringVar.Substring(start,count)` | `stringVar` 是字符串变量名或字符串表达式。参数 `start` 是指定 `stringVar` 中位置的整数，`count` 是指定字符数量的整数。该方法返回一个从 `start` 开始并继续计数 `count` 个字符的字符串。 |

```c
Example:
// 以下代码显示 "beans"
string str = "cocoa beans";
MessageBox.Show(str.Substring(0, 5));
```

# 修改字符串的方法

8-6 描述了字符串对象通过以下方式修改字符串内容的几种方法：

- `Insert` 方法将一个字符串插入到另一个字符串中。
- `Remove` 方法从字符串中删除指定的字符。
- `Lower` 方法将字符串转换为所有小写字母。
- `Trim` 方法删除字符串开头和末尾的空格。（开头空格是指出现在字符串开空格，末尾空格是指出现在字符串末尾的空格。）
- `TrimStart` 方法删除字符串开头的空格。
- `TrimEnd` 方法删除字符串末尾的空格。

需要注意的是，表 8-6 所示的方法实际上并没有修改调用者对象。它们返回的是调用字符串的修改后的副本。例如，看下方的代码，它演示了 `Remove` 方法：

```csharp
string str1 = "sunshine";
string str2 = str1.Remove(3);
MessageBox.Show(str1);
MessageBox.Show(str2);
```

# 表 8-6 修改字符串的方法

| 方法 | 描述 |
| :--- | :--- |
| `stringVar.Insert(start, item)` | `stringVar` 是变量名或字符串表达式。`start` 参数是一个整数，指定 `stringVar` 中的位置，而 `strItem` 是要插入的参数。该方法返回一个包含 `stringVar` 副本的字符串，并在由 `start` 指定的位置插入了 `strItem`。  
示例：  
// 以下将显示 "New York City"。  
string str1 = "New City";  
string str2 = str1.Insert(4, " York ");  
MessageBox.Show(str2); |
| `stringVar.Remove(start)` | `stringVar` 是变量名或字符串表达式。`start` 参数是一个整数，指定 `stringVar` 中的位置。该方法返回一个包含 `stringVar` 副本的字符串，并删除了从 `start` 指定的位置到字符串末尾的所有字符。  
示例：  
// 以下将显示 "blue"。  
string str1 = "blueberry";  
string str2 = str1.Remove(4);  
MessageBox.Show(str2); |
| `stringVar.Remove(start, count)` | `stringVar` 是变量名或字符串表达式。`start` 参数是一个整数，指定 `stringVar` 中的位置，`count` 是一个指定字符数量的整数。该方法返回一个包含 `stringVar` 副本的字符串，从 `start` 指定的位置开始删除了 `count` 个字符。 |
| `stringVar.ToLower()` | 示例：  
// 以下将显示 "jelly doughnuts"。  
string str1 = "jelly filled doughnuts";  
string str2 = str1.Remove(6, 7);  
MessageBox.Show(str2);  
`stringVar` 是字符串变量名或字符串表达式。该方法返回一个包含 `stringVar` 副本的字符串，并已将其转换为小写。  
示例：  
// 以下将显示 "abc"。  
string str1 = "ABC";  
string str2 = str1.ToLower();  
MessageBox.Show(str2); |

# 第 8 章 更多关于数据处理

第 1 行声明了一个字符串变量 `str1`，并初始化为字符串 `"sunshine"`。第 2 行调用 `str1.Remove` 方法，并将 `3` 作为参数传递。该方法返回 `str1` 的副本，删除了从位置 `3` 到字符串末尾的所有字符。（该方法返回字符串 `"sun."`）。返回的字符串被赋值给变量 `str2`。第 3 行显示 `str1` 变量，其内容为 `"sunshine"`，第 4 行显示 `str2` 变量，其内容为 `"sun"`。

在教程 8-2 和 8-3 中，我们在格式化和格式化美国电话号码的应用程序中使用我们讨论过的几种字符串方法。

![](img/8a88e1d8c69a687988c05f162ce32cac_500_0.png)

# 教程 8-2：完成电话号码格式化应用程序

美国的电话号码通常格式化为如下形式：

`(XXX) XXX-XXXX`

在该格式中，`x` 代表一个数字。括号内的三个数字是区号。区号后的三个数字是前缀，连字符后的四个数字是线路号码。这里有一个例子：

`(919)555-1212`

虽然括号和连字符让人们更容易阅读，但这些字符对于计算机处理来说是不必要的的。在计算机系统中，电话号码通常存储为一系列未格式化的数字，如下所示：

`91955512212`

处理电话号码的程序有时需要对用户输入的数字进行去格式化。这意味着在将号码存储到文件中或进行其他处理之前，必须移除括号和连字符。此外，程序还需要对数字进行格式化的能力，以便在屏幕上显示或打印到纸上之前包含括号和连字符。

在本教程中，你创建了电话号码格式化应用程序。应用程序的表单已经为你创建好，如图 8-2 所示。应用程序完成后，你将能够向 `numberTextBox` 输入 10 位数字字符串，并点击 `Format` 按钮以看到格式化为电话号码的数字字符串。

> 图 8-2 电话格式化应用程序的表单

![](img/8a88e1d8c69a687988c05f162ce32cac_500_1.png)

# 8.2 字符串与字符处理

**步骤 1**：启动 Visual Studio（或 IDE）。

**步骤 2**：打开名为 `TelephoneFormat` 的项目。

**步骤 3**：打开代码编辑器。输入位于第 20-50 行的 `IsValid` 方法。该方法接受一个字符串作为参数，如果字符串长度为 10 且仅包含数字，则返回 `true`；否则返回 `false`。使用此方法可以确保用户输入的是有效的数字字符串。让我们查看代码：

第 25 行：该语句声明了常量 `VALID_LENGTH`，初始化为 `10`，代表字符串的长度。

第 26 行：该语句声明了一个布尔变量 `valid`，初始化为 `true`。`valid` 用来指示 `str` 是否有效。

第 29 行：如果该语句判断 `str` 有效，则程序继续执行第 32 行。否则，程序跳转到第 42 行的 `else` 子句，第 45 行将 `valid` 置为 `false`。

第 32 行：`foreach` 循环遍历 `str` 参数中的每个字符。如果第 36 行判断字符不是数字，则第 38 行将 `valid` 置为 `false`。

第 49 行：该语句返回 `valid` 的值。

**步骤 4**：输入位于第 52-64 行的 `TelephoneFormat` 方法。`TelephoneFormat` 方法接受一个字符串作为参数（通过引用传递），并在格式 `(XXX)XXX-XXXX` 所示的正确位置插入括号和连字符。让我们仔细查看代码：

第 54 行：注意在变量 `str` 的声明中使用了 `ref` 关键字。

第 57 行：该语句调用 `Insert` 方法在位置 `0` 插入 `"("`。字符串中的所有字符都会自动向右移动一位以容纳插入的字符。

第 60 行：该语句调用 `Insert` 方法在位置 `4` 插入 `")"`，将之前从位置 `4` 开始的字符向右移动一位。

第 63 行：该语句调用 `Insert` 方法在位置 `8` 插入 `"-"`，将之前从位置 `8` 开始的字符向右移动一位。在该语句执行后，所引用的字符串被格式化为 `(XXX)XXX-XXXX`。

**步骤 5**：为 Button 和设计器 `formatButton` 控件创建 Click 事件处理器。这会打开编辑器，你将看到一个名为 `formatButtonClick` 的空事件处理器。通过输入 Program 8-2 中第 68-82 行的代码来完成事件处理器。让我们回顾这段代码：
