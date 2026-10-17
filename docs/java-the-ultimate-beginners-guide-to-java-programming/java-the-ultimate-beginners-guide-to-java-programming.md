
# Java 编程初学者指南

## 结论

赠品：预览《SQL 终极新手指南：今天学习 SQL》

再次感谢下载本书！

## 引言

`Java` 被称为世界上最实用、通用的面向对象语言之一，它是你可以学习的最优秀的编程语言之一——即使你只是一个新手，也可以精通它！

现在就开始阅读这本书吧，你将很快学到更多关于 `Java` 的知识！

再次感谢。

# 第 1 章：Java 导论

`Java` 被称为世界上最实用、通用的面向对象语言之一，它是你可以学习的最优秀的编程语言之一——即使你只是一个新手，也可以精通它！

现在就开始阅读这本书吧，你将很快学到更多关于 `Java` 的知识！

再次感谢。

## 历史

`Java` 的历史追溯到 1991 年，当时 `Patrick Houghton`、`Mike Sheridan` 和 `James Gosling` 采用了一种语言。在 1995 年，`Microsystems` 最后发布了 `Java 1.0`，它在通用许可下免费提供。

## 运行时与性能

最初，`Java` 的运行速度没有 `C++` 快，是因为由于所谓的“即时编译”。然而，多年来，它的速度得到了提升并赢得了声誉。

`Java` 运行速度快的另一个原因是它利用了虚拟机，这意味着运行时不会受到程序员选择添加或减少其所尝试创建的内容的影响。

## 语法

当然，你以后会学习更多内容，但你现在需要意识到的是 `Java` 类封装了所有代码。然而，基本数据类型（如字符、布尔值和整数——你将在下一章学习）在此被排除。

你还会注意到用于语法的符号：

- `//` 用于单行注释
- `/* ... */` 用于多行注释

在创建程序时，你应该将文件保存为 `.java`，子页面保存为 `.class`。如果你想将一个子页面（或类）设为私有，只需要将其保存在相同的 `Java` 文件夹中，而不是单独存放，这样其他人无法访问它。

几行 `Java` 语法如下：

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

## 内存

`Java` 运行速度快的另一个原因是它利用了自动内存管理，这意味着运行时不会受到程序员选择添加或减少其所尝试创建的内容的影响。

现在的情况是当某个对象不再被引用时，它将不再被视为程序的一部分，并且不会占用大量内存——这使得整个程序更容易管理。

# 第 2 章：Java 中的八种基本类型

正如前面提到的，`Java` 编程中共有八种基本类型（或原始数据类型）。以下是它们以及你应该了解的知识。

## 字符

字符构成了 `Java` 的第一种基本类型。基本上，这些是在你在创建程序时应该使用的单词。这些还包含了许多内容，它们是……

1. `If`。执行代码，并包括 `else` 和 `elif`
2. `While`。用于真条件，并执行代码块代码。
3. `For`。用于附加代码块。
4. `Try`。由 `except` 处理，并允许为代码块抛出异常。
5. `With`。使用块管理器，帮助打开和关闭文件。
6. `Def`。意味着定义了一个方法或函数。
7. `Class`。执行块代码并用于面向对象编程。
8. `Print` / `Print()`。用于打印。
9. `Import`。用于从其他函数导入模块。
10. `Yield`。用于生成函数值，也用作运算符。
11. `Assert`。用于检查本应应用的语句。
12. `Pass`。用于创建空代码块。

注意，这些关键字不能用作变量！

## 缩进与行

使用的空格和单词数量将决定你的编程是否正确，或者是否会产生错误：

看看下面的两个示例。第一个是正确的，另一个由于最后一行未缩进的 `print` 命令而产生错误。

### 示例 1

```
if True:
    print "True"
else:
    print "False"
```

### 示例 2

```
if True:
    print "Answer"
    print "True"
else:
    print "Answer"
    print "False"
```

## 引号

为了在此程序中创建引号，请注意你可以使用单引号 (`''`)、双引号 (`""`) 或三连引号 (`""""""`) 来表示字符串和字面量字符串。

## 多行语句

系统会自动根据命令的结束决定新行的开始，但如果你想继续写自己的行，可以使用反斜杠 (`\`) 来实现，使用括号时除外。

### 示例 1

```
total = item_one + \
    item_two + \
    item_three
```

### 示例 2

```
days = ['Monday', 'Tuesday', 'Wednesday',
'Thursday', 'Friday']
```

## 注释

要创建注释，只需使用井号 (`#`)——这听起来非常适合社交媒体，对吧？例如：

### 示例 1

```
#!/usr/bin/java
```

### 第一条注释

`print "Hello, Java!"` # 第二条注释

### 示例 2

- `# 这是一个注释。`
- `## 这也是一个注释。`
- `## 这也是一个注释。`
- `## 我说过。`

## 等待用户

当你想要创建一个提示来告诉用户你正在等待他的命令时，你可以尝试：

```
#!/usr/bin/java
raw_input("\n\n按键退出。")
```

## 独立语句组

独立语句的组在 `Java` 语言中称为套件（Suite）。基本上，你必须以关键字开始并以冒号 (`:`) 结束，例如：

```
if expression:
    suite
elif expression:
    suite
else:
    suite
```

上述命令将为你提供套件。

## 布尔表达式与逻辑

接下来是布尔逻辑。在其中，值被简化为真（`true`）或假（`false`），并用于二进制系统。简而言之，它们帮助程序做出决策。例如：

```
>>> sensor_on = True
>>> sensor_on
True
```

你需要记住，布尔逻辑决定了确切的结果——你想看到的某些特定内容。例如：

| a | b | a == b | a != b | a and b | a or b | not b |
|---|---|---|---|---|---|---|
| False | False | True | False | False | False | True |
| False | True | False | True | False | True | True |
| True | False | False | True | False | True | False |
| True | True | True | False | True | True | False |

## 逻辑“与” (And)

如你所见，有一个表示 `a` 和 `b` 的表达式。记住，只有当 `a` 和 `b` 都具有相同的值时才会发生，这意味着在所有其他情况下结果都是假的。

这里有一个例子：

```
a and False == False
False and a == False
b and a == a and b
a and True == a
True and a == a
a and a == a
```

## 逻辑等价

逻辑等价或 `a == b` 发生在 `a` 和 `b` 都具有相同真值时，且可以是真也可以是假；否则，它们没有相同的内核。

## 逻辑“或” (or)

接下来，你看到一个表示 `a` 或 `b` 的表格。它测试是否都为真，或者是否只有一个变量为真。当两者都为真时，它也是真。例如：

```
a and False == False
False and a == False
b and a == a and b
a and True == a
True and a == a
a and a == a
```

## 逻辑取反 (Negation)

基本上，逻辑取反会翻转布尔值。如果是真的，它就会变成假的；如果是假的，它就会变成真的。例如：

```
not True == False
not False == True
```

## 类型转换函数

4. `Str(x)`。将 `x` 转换为字符串表示。
5. `Complex(real [, imag])`。这会给你一个复数。
6. `Eval(str)`。这会评估一个字符串并返回一个对象。
7. `Repr(x)`。将 `x` 转换为表示性字符串。
8. `Set(s)`。将 `s` 转换为集合。
9. `List(l)`。将 `l` 转换为列表。
10. `Tuple(t)`。将 `t` 转换为元组。
11. `Frozenset(s)`。将 `s` 转换为不可变集合。
12. `Dict(d)`。这会给你一个字典。
13. `Oct(x)`。将 `x` 转换为八进制字符串。
14. `Hex(x)`。将 `x` 转换为十六进制字符串。
15. `Ord(x)`。这会返回单个字符的整数值。
16. `Unichr(x)`。最后，通过此命令，你将得到一个 Unicode 字符。

## 赋值

等号 (`=`) 在这里很重要，因为你不需要在这里进行显式声明，但你必须确保将变量放在等号之前，并在右侧放置你想要对变量执行的操作。例如：

```java
#!/usr/bin/java

counter = 100      # 整数赋值
miles = 1000.0      # 浮点数
name = "John"      # 字符串
```

```java
print counter
print miles
print name
```

这将给你输出结果：

```
100
1000.0
John
```

## 运算符

然后，你还有 `Java` 运算符。这些运算符处理操作数值，并可以分类为：

1. 算术运算符
2. 赋值运算符
3. 标识运算符
4. 成员运算符
5. 位运算符
6. 逻辑运算符
7. 比较/关系运算符

## 算术运算符

这里是你可以使用的算术运算符：

1. `+` 加法。当然，这会在你的运算符上增加值 (`a + b = 15`)
2. `-` 减法。这从左侧的操作数中减去右侧的操作数 (`a - b = -10`)
3. `/` 除法。这用左侧的操作数除以右侧的内容 (`b / a = 2`)
4. `*` 乘法。将你拥有的任何内容倍乘 (`a * b = 200`)
5. `//` 整除。通过此运算符，你可以得到商的结果，特别是在移除小数点时 (`9 // 2 = 4`) (`9.0 // 2.0 = 4.0`)
6. `**` 幂。这可以帮助你推导出指数表示法 (`a ** b = 5 的 10 次方`)
7. `%` 取模。将左侧的操作数除以右侧并提供余数 (`b % a = 0`)

## 赋值运算符

1. `=` 将右侧的值赋给左侧的操作数 (`c = a + b` 将 `a + b` 的值赋值给 `c`)
2. `-=` 减法并赋值。这从左侧操作数中减去右侧的操作数，并将结果赋值给左侧 (`c -= a` 等于 `c = c - a`)
3. `+=` 加法并赋值。这将右侧的操作数加到左侧，并给出左侧操作数的结果 (`c += a` 等于 `c = c + a`)
4. `/=` 除法并赋值。除左侧操作数并将值赋给左侧 (`c /= a` 等于 `c = c / a`)
5. `*=` 乘法并赋值。将右侧操作数与左侧操作数相乘并将结果赋值给左侧操作数 (`c *= a` 等于 `c = c * a`)
6. `**=` 幂并赋值。推导出指数表示法 (`c **= a` 等于 `c = c ** a`)
7. `%=` 取模并赋值。取两个操作数的模 (`c %= a` 等于 `c = c % a`)
8. `//=` 整除并赋值。通过此运算符，你可以得到商的结果，特别是在移除小数点时 (`c //= a` 等于 `c = c // a`)

## 标识运算符

这些比较两个对象的内存。

1. `is`。确定两侧的变量是否为真；如果不是，运算符指向主体 (`x is y`，如果 `id(x)` 等于 `id(y)`)
2. `is not`。如果两侧的变量为假，运算符指向主体并说真 (`x is not y`，如果 `id(x)` 不等于 `id(y)`)。

## 成员运算符

这些检查是否在序列中。

1. `in`。检查变量是否在指定的序列中 (`x in y`)。
2. `not in`。检查变量不在指定的序列中并评估为真 (`x not in y`)。

## 位运算符

这些按位执行操作。例如：

```
a & b
a | b
a ^ b
~ a
```

## 逻辑运算符

逻辑运算符基本上包含 `and`、`or`、`not`。

## 比较运算符

1. `==`。如果操作数相等，则为真 (`a == b`)
2. `!=`。如果值不相等，则为真 (`a != b`)
3. `<=`。如果左侧操作数小于右侧，则为真 (`a <= b`)
4. `>=`。如果左侧操作数大于右侧，则为真 (`a >= b`)
5. `<`。如果操作数值小于右侧，则为真 (`a < b`)
6. `>`。如果左侧操作数的值大于右侧，则为真 (`a > b`)

## 循环

循环是程序中提供的各种操作。包括：

1. `for` 循环。这帮助你执行语句若干次，并简化代码。
2. `while` 循环。重复你想再次使用的语句或组。
3. 嵌套循环。这意味着你在程序中使用一个或多个循环。
4. `do...while` 循环。这等于一个语句但被程序视为条件。
5. `goto` 语句。跳转已标记的语句。
6. `continue` 语句。这有助于跳过循环体的剩余部分——不需要。
7. `break` 语句。终止 `switch` 和循环，并在你执行之后执行其他语句。

## Switch Case

当然，如果你想测试变量，必须使用 `switch`——也称为 `switch` 语句。你必须遵循某些规则，这些：

1. `switch` 还有默认情况。因此，它们必须出现在 `switch` 的最后，并可以确定程序中的假语句。在这种情况下，你就不需要使用 `break`。
2. 每个 `case` 都不需要 `break`。在没有 `break` 的情况下，你只需要等待通过。
3. 当遇到 `break` 语句时，继续已使用的终止，这样你就可以跳转到下一行。
4. 应该使用常量表达式。这意味着你必须在程序中使用相同的数据类型。
5. 每个 `switch` 包含由冒号分隔的 `case` 语句。
6. 你可以枚举整数 `switch`，这样就可以轻松转换。

对于这一点，你必须记住：

| 表达式 | Case |
| :--- | :--- |
| Case 1 | Block 1 |
| Case 2 | Block 2 |
| Case 3 | Block 3 |

以此类推。简而言之，你可以参考下面的示例：

```c
#include <stdio.h>
int main () {
  /* 局部变量定义 */
  char grade = 'D';
  switch(grade) {
    case 'E' :
      printf("Amazing!\n");
      break;
    case 'D':
      printf("Great Job!\n");
      break;
    case 'C':
      printf("You did well!\n");
      break;
    case 'F':
      printf("Try again next time\n");
      break;
    default:
      printf("Invalid grade\n");
  }

  printf("Your grade is %c\n", grade);

  return 0;
}
```

# 第 3 章：数组和字符串

表达式将由 `Java` 自身解析，并在准备好时返回结果。非常像 `JavaScript` 表达式，所以如果你了解这些，这门语言对你来说就不难。

这意味着 `Java` 表达式是：

1. `Java` 表达式可以包含过滤器——但 `JavaScript` 表达式没有。
2. 不支持异常、循环和坐标。
3. 表达式可以写在 `HTML` 内部。
4. `Java` 表达式也可以是变量、运算符和字面量。

例如：

```html
{{ 10 + 5 }} 或 {{ name + "" + nickname }}
```

这意味着基本的 `Java` 表达式代码看起来如下：

```html
<!DOCTYPE html>
<html>
<script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.4.8/angular.min.js"></script>
<body>
<div ng-app="">
<p>Supergirl Versus Bizzaro: {{ Supergirl + Bizzaro }}</p>
</div>
</body>
</html>
```



通过移除 `ng` 指令，HTML 将无法解析表达式，而只是原样显示，这看起来就像这个一样：

```html
<!DOCTYPE html>
<html>
<script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.4.8/angular.min.js"></script>
<body>
<div ng-app="">
<p>Supergirl Versus Bizzaro: {{ Supergirl + Bizzaro }}</p>
</div>
</body>
</html>
```

另一个例子是在如果你想在 CSS 中更改某些颜色和样式。例如，如果你想将一个框的颜色改为粉色，你可以尝试以下操作：

```html
<div ng-app="" ng-init="myCol=pink">
<input style="background-color: {myCol}" ng-model="myCol" value="{myCol}">
</div>
```

## 数组

它的工作类似于 JavaScript 数组。如果你打算使用 `ng-bind`，它看起来像下面这样：

```html
<div ng-app="" ng-init="points=[2,4,6,8]">
<p>第三个结果是 <span ng-bind="points[2]"></span></p>
</div>
```

但是，如果你去掉 `ng-bind`，它看起来就像下面这样：

```html
<div ng-app="" ng-init="points=[2,4,6,8]">
<p>第三个结果是 {{ points[2] }}</p>
</div>
```

## 字符串

字符串在编程中也能将事物连接在一起。Java 字符串的工作方式也像 JavaScript。它可能有两种方式——只需看下面的示例：

```html
<div ng-app="" ng-init="firstName='Mark';lastName='Ruffalo'">
<p>名字是 <span ng-bind="firstName + ' ' + lastName"></span></p>
</div>
```

或者：

```html
<div ng-app="" ng-init="firstName='Mark';lastName='Ruffalo'">
<p>名字是 {{ firstName + " " + lastName }}/</p>
</div>
```

## 如何格式化 Java 字符串

有些人认为 Java 字符串处理起来极其复杂。然而，你并不真的需要害怕它们。在格式化 Java 字符串时，你需要了解这些……

## 工作字符串

你必须意识的第一点是，某些元素被称为 Java 工作字符串（Working strings）。

Java 工作字符串基本上是带引号的字符。使用这些字符，单引号被认为等于双引号，因此你可以预期：

```python
var1 = 'Hello World!'
var2 = "Java Programming"
```

## 访问值

记住字符类型不被 Java 语言接受。你必须使用方括号 `[]` 来访问子字符串。例如：

```python
#!/usr/bin/java
```

```python
var1 = 'Hello World!'
var2 = "Java Programming"
```

```python
print "var1[0]: "
```

当你输入这些命令时，你会得到结果：

```
var1[0]: H
var2[1:5]: ytho
```

你也可以通过以下方式更新字符串：

```python
#!/usr/bin/java
```

```python
var1 = 'Hello World!'
```

```python
print "Updated String :- ", var1[:6] + 'Java'
```

那将给你以下结果：

```
Updated String :- Hello World
```

## Unicode 字符串

还有 Unicode 字符串或 8 位 ASCII，你可以将其保持为 16 位 Unicode。例如：

```python
#!/usr/bin/java
```

```python
print u'Hello, world!'
```

基本上，这会给你：

```
Hello, world!
```

## 三引号引号

你也可以使用三引号，它可以包含多行、制表符，甚至换行符。例如：

```python
#!/usr/bin/java
```

```python
para_str = """这是一个长字符串，它由
几行和不可打印字符组成，如
制表符 ( \t )，它们在显示时会以这种方式显示。
字符串内的换行符，无论是显式像这样
在括号 [ \n ] 中给出的，还是仅仅是一个换行符，
变量赋值也会出现。"""
```

```python
print para_str
```

当你输入上面的语法时，将得到这个长字符串，它由

几行和不可打印字符组成，如

制表符 ( \t )，它们在显示时会以这种方式显示。

字符串内的换行符，无论是显式像这样

在括号 [ \n ] 中给出的，还是仅仅是一个换行符，变量赋值也会出现。

## 特殊代码和字符

为了编写这些，必须使用特殊字符和代码。这些是：

## 内置字符串方法

- 1. `Center (width, fill)`。配合原始字符串，这将给你一个填充空格的字符串。
- 2. `Capitalize()`。基本上将字符串的首字母大写。
- 3. `Encode (suffix, beg=0, end(string))`。运行字符串的编码版本，用于此。
- 4. `Decode (encoding UTF-8, errors=strict)`。该代码用于编码，你会得到默认代码。
- 5. `Count (str, beg=0, end(string))`。统计字符串出现的次数并开始索引。
- 6. `Find (str, beg=0, end(string))`。检查 `str` 是否在字符串或后续字符串上。
- 7. `Expandtabs(tabsize=8)`。将制表符替换为多个空格。
- 8. `Decimal()`。
- 9. `Zfill (width)`。从左侧填充零。
- 10. `Upper ()`。将小写字母转换为大写。
- 11. `Translate (table, deletechars="")`。将字符串转换为翻译表。
- 12. `Title ()`。将字符串转换为标题格式，意味着大写和反之。
- 13. `Swapcase ()`。字符串中的所有字母反转。
- 14. `Strip ((chars))`。对每个字符串执行 `rstrip()` 和 `lstrip()`。
- 15. `Startswith (str, beg=0, end(string))`。检查字符串是否是字符串本身的子集。
- 16. `Splitlines (num=str.count("n"))`。将每行拆分。
- 17. `Split (sep="", num=str.count(sep))`。将字符串拆分为分隔符。
- 18. `Rjust (width, [,fill(char)])` 填充空格的字符串。
- 19. `Rindex (str, beg=0, end(string))`。这就像 `index` 但是反向的。
- 20. `Replace (old, new, [max])`。替换 `max` 次出现。
- 21. `Max (str)`。返回最大字符字符串。
- 22. `Join (seq)`。合并字符串的表示。

## 格式符号及其功能

- `%X` 十进制整数（大写字母）
- `%x` 十进制整数（小写字母）
- `%u` 无符号十进制
- `%s` 通过 `str()` 转换的字符串
- `%o` 八进制整数
- `%i` 带符号十进制
- `%g` `%f` 和 `%e` 的较短者
- `%G` `%f` 和 `%E` 的较短者
- `%f` 浮点数
- `%d` 带符号十进制
- `%c` 字符

## 其他重要符号

- 1. `m.n`。`m` 是最小宽度，`n` 是小数点后的位数（如果适用）。
- 2. `0`。左侧填充零（而不是空格）。
- 3. `<sp>`。在前面留出空格
- 4. `+`。号
- 5. `*` 指定宽度
- 6. `%`。指定精度
- 7. `%` 十进制变量
- 8. `#` 添加八进制
- 9. `-` 左对齐

## 使用关键字

你还必须记住，简单使用以下内容时，格式化字符串会变得更容易：

- 1. `Auto`。用于定义存储类。例如：

```python
auto int var1;
```

- 2. `Char`。用于指示类型，有时称为字符。

```python
Char variable0
```

- 3. `Switch` 和 `default`。一组表示表达式的语句，可以作为默认。例如：

```python
switch(this area){
case 'A':
// A 时执行某些语句
break;
case 'B':
// B 时执行某些语句
break;
default:
// 默认时执行某些语句;
}
```

- 4. `Break` 和 `continue`。用于封装循环，你可以跳出循环并继续下一个语句。这也用于跳过循环中的某些元素。

```python
for (i=1;i<=1;++i){
if (i==2)
continue;
if (i==8)
break;
}
```

- 5. `Const`。意味着常量，意味着程序中有一个常量值。例如：

```python
const int a=10;
```

- 6. `Double` 和 `Float`。用于指示浮点类型变量，并用于相应的数据。例如：

```python
Float thisvariable
Double thisvariable
```

- 7. `Do` 和 `While`。用于 C 程序的循环。这里有一个示例：

```python
i=7;
while (i<7) {
printf("%d \i",i);
i++;
}
```

那将给你给出以下输出：0 2 4 6 7 9

- 8. `Extern`。表示外部变量并通过不同的函数进行访问和声明。例如：

```python
#include <myfavoriteprogram>
extern i=8;
void print1(){
printf("%d \i",i);
}
int main() {
printf("%d \i",i);
}return 0;
}
```

- 9. `Enum`。正如名称所示，它用于枚举程序中的某些部分。它由常量整数组成。例如：

```python
enum enum_var{
var4;
var5;
var6;
}
```

- 10. `If` 和 `Else`。这两个一起使用，通常用于决策目的。例如：

```c
if (i==2)
    printf("i is 2.")
else
    printf("i is not 2.")
```

11. `Goto`。它用于带标签语句的无条件跳转。例如：

```c
for(i=1;i<6;i++){
    if (i==10) {
        goto error;
    }
    printf("i is not 9");
error:
    printf("Error, count can't be 9");
}
```

12. `For`。它用于循环。这里有一个示例：

```c
for(i=0;i<1;++i) {
    printf("%c",i);
}
```

13. `Short`, `unsigned`。这些主要用于整数，对于这些，你必须注意以下范围：

- 短整数 (`Short int`) -32768 到 32767
- 无符号整数 (`Unsigned int`) 0 到 65535
- 有符号整数 (`Signed int`) -32768 到 32767
- 长整数 (`Long int`) -32768 到 32767

14. `Sizeof`。它用于确定程序中某个对象的大小。这里有一个示例：

```c
#include <stdio.h>
int main() {
    printf("%u bytes.",sizeof(char));
}
```

15. `Return`。终止当前函数的执行并向函数本身返回某些值。例如：

```c
int func() {
    int b=10;
    return c;
}
```

16. `Static`。它用于指示存储类的值，可以一直持续到程序结束。例如：

```c
static int var;
```

17. `Register`。这是一种区分普通变量与快速变量的东西。例如：

`register int var1;`

18. `Typedef`。这帮助你区分简单的数字和整数。例如：

`typedef float ab;`

抽象蝴蝶，翅膀

19. `Struct`。它用于创建结构体以便于管理。例如：

```c
struct contestant {
    char name[1116];
    float marks;
    int age;
    int s2, s3;
};
```

20. `Void`。这意味着你的程序某部分没有值。例如：

```c
void no_return(int a) {

}
```

21. `Union`。联合体是关于处理变量的。这是你需要做的：

```c
union student {
    char name[100];
    float marks;
    int age;
}
```

22. `Volatile`。这意味着你的程序中有一个异常函数。这是你需要做的：

`const volatile number`

你还可以使用一些特殊字符，这些字符是：

`, , . _ ; 0 : $ % # [ ] { } ? & ^ ! * / - ~ +`

对于数字，你可以使用以下数字：

`0123456789`

你也可以使用大写或小写字母字母表。

## 第 4 章：基本类型 VS 引用类型

早些时候你学习了 Java 中的基本类型或独立数据类型。不过，你也必须知道，还有被称为引用类型的东西，和基本类型一样，它们也属于不同的类别，并且可以做很多事情——但必须由基本数据支持。

基本数据类型比引用类中的类型更好吗？并不完全是。虽然基本程序可以独立存在，但引用数据类型可以做某些事情，这些可以让让你尝试制作的程序变得好得多。

这些类型到底是什么？

## 用户数据报协议 (User Datagram Protocol)

它是互联网协议族中的一个重要成员。它提供了无连接的传输，这种方式实际上是不可靠的，并且不会破坏任何方式的网络。它们对于时间敏感的应用是完美的。用户数据报协议包括：

- 1. 能够提供数据报；
- 2. 面向事务并适用于域名系统；
- 3. 单向通信，适用于服务发现和广播信息；
- 4. 适用于实时应用（如 Twitter, Snapchat 等），因为它允许延迟。它也适用于 VOIP 应用（如 Skype）以及某些游戏；
- 5. 适用于大量客户端，且无状态。它适用于流媒体应用；
- 6. 对于引导是完美的。

它也适用于 0 到 4 字节，在某些情况下。

## 传输控制协议 (Transmission Control Protocol)

它提供了错误检查、有序且可靠的字节流，位于各种网络之间。这用于电子邮件以及万维网。它也是无连接的，通过处理已经传输的数据工作。它从 0 到 60 字节包含源端口和目的端口。偏移也是预留的，还有窗口大小、校验和紧急指针。

基本上，你可以记住的是：

- 1. 16 位标识源端口；
- 2. 16 位标识接收端口；
- 3. 32 位指定头部；
- 4. 32 位标识确认号；
- 5. 32 位标识标志位；
- 6. 32 位标识未来使用的数据。

使用这种语言定义其他位。

## 互联网控制消息协议 (Internet Control Message Protocol)

JAVA 的另一个重要协议，它向路由器发送消息并有自己的数字。区别在于它在 IPv4 中进行错误检查。它也工作在 0 到 60 字节，其中：

- 1. 类型 = 控制消息 | 子类型
- 2. 代码 = 控制消息 | 子类型
- 3. 头部剩余 = ICMP 数据
- 4. 校验和 = ICMP头部和数据

## 地址解析协议 (Address Resolution Protocol)

正如名称所示，这是一种使通信应用易于工作的电信协议。它用于映射网络地址，使得消息——甚至视频通话成为可能，还用于 Xerox PARC、DEC Net 等。对于这个，你可以记住：

- 0 –硬件类型 (HTYPE)
- 2 – 协议类型 (PTYPE)
- 4 – 硬件地址 (HLEN) | 协议地址 (PLEN)
- 6 – 操作 (OPER)
- 8 – 发送硬件地址 (SHA)
- 10 – 2 字节
- 12 – 2 字节
- 14 – 发送地址协议 (SAP)
- 16 – 2 字节
- 18 – 目标硬件地址 (THA)
- 20 – 2 字节
- 22 – 2 字节
- 24 – 目标协议地址 (TPA)
- 26 – 2 字节

## 互联网协议 (Internet Protocol)

最后——与 JAVA 密切相关的，互联网协议是关于在网络中提供边界，以及中继互联网到联网的数据报。其结构涉及头部和负载，其中头部被称为主 IP 地址，并借助某些参数连接接口。路由前缀和网络标识也涉及，还有内部或外部网关协议。可靠性取决于端到端协议，但大多数情况下你可以预期框架是这样的：

| 数据应用 | |
| :--- | :--- |
| UDP 头部 | UDP 传输 |
| IP 头部 | IP 数据互联网 |
| 帧头部 | 帧数据 脚链接 |

## 第 5 章：面向对象编程

如果你还记得，早提到 Java 是一种面向对象的编程语言，这意味着它处理数据类型、字符串、数组、列表、数字的创建和使用，所有这些事情都可以让程序变得更好——而不仅仅是你理解的普通字母或数字。

由于 Java 是一种面向对象的语言，你可以预计它由于以下原因而工作：



## 单一来源 (One Source of Truth)

通常被称为“单一数据源”，这意味着整个应用存储在一个树对象中，然后放置在单一存储中。通过这种方式，创建应用变得简单，调试以及内省也变得简单。某些函数——如撤销/重做——变得轻而易举。它使用以下代码：

```javascript
console.log(store.getState())
{
    visibilityFilter: 'SHOW_ALL',
    todos: [
        { text: 'Keep all in a single tree', completed: true },
        { text: 'Consider using Java', completed: false }
    ]
}
/* 打印 */
```

## 只读状态 (Read-Only State)

Java 做的另一件事是确保应用具有这种“只读”状态。通过这种方式，发射动作意味着突变开始发生，这也意味着所有的突变将是集中处理的，你只需要关注按照严格顺序发生的某些竞态条件即可。这种状态对于测试目的也很重要。

它使用以下代码：

```javascript
store.dispatch({
    type: 'SET_VISIBILITY_FILTER',
    filter: 'SHOW_COMPLETED'
});
store.dispatch({
    type: 'COMPLETE_TODO',
    index: 1
});
```

## 纯函数用于更改

为了确保操作通过使用还原器（reducers）来转换对象树，这些还原器是纯函数，它们接收之前的动作类型和状态，然后可以返回列出的下一种状态。

基本上，你可以先处理一个还原器，并在对你的应用进行各种更改时观察数字的增长。为此，必须使用以下代码：

```javascript
function visibilityFilter(state = 'SHOW_ALL', action) {
  switch (action.type) {
    case 'SET_VISIBILITY_FILTER':
      return action.filter;
    default:
      return state;
  }
}

function todos(state = [], action) {
  switch (action.type) {
    case 'ADD_TODO':
      return [
        ...state,
        {
          text: action.text,
          completed: false,
        },
      ];
    case 'COMPLETE_TODO':
      return state.map((todo, index) => {
        if (index === action.index) {
          return Object.assign({}, todo, {
            completed: true,
          });
        }
        return todo;
      });
    default:
      return state;
  }
}

import { combineReducers, createStore } from 'redux'
let reducer = combineReducers({ visibilityFilter, todos })
let store = createStore(reducer)
```

# 第 6 章：如何创建你自己的类

在 Java 中，类非常重要，因为它们通常决定了你的程序会发生什么。因此，在创建 Java 类并确保它们能够实际工作时，有很多元素参与其中这并不意外。基本上，这一切都始于框架。

## Java 类的框架

一个 Java 类的框架由以下部分组成：

1. 程序类型在 `UNODE` 声明之间的文本中描述。
2. 程序信息在 `<HEAD>` 和 `</HEAD>` 之间的文本中提供。
3. 一个 Java 程序在 `<Java>` 和 `</Java>` 之间的文本中描述。
4. 程序的标题在 `<TITLE>` 和 `</TITLE>` 之间的文本中提供。
5. `<h1>` 和 `</h1>` 之间的文本被称为标题。它也适用于 H2、H3、H4 等。
6. 程序的内容——或你在屏幕上看到的内容——位于 `<body>` 和 `</body>` 之间的文本中。
7. 然后，可以在 `<p>` 和 `</p>` 之间的文本中创建段落。

## 标签页

现在，当涉及到标签时，你必须记住它们通常成对出现，如上面的框架所示。左侧是标签的开始（也称为起始标签），结束标签看起来几乎相同——但只有开头有一个斜杠（/）。

以下是你最可能使用的标签：

`<UNICODE...>`

- `NAME` — 涉及页面上的某个部分
- `HREF` — 用于超链接，或用于添加你所引用的 URL 名称
- `onClick` — 这是运行的脚本，使用户户能够点击锚点（例如，对于 google.com 等内容，必须运行此脚本，以便用户在点击后会被重定向到链接）

`<A>` 锚点

- `TITLE` — 这是正在打开的程序的标题
- `MOUSEOUT` — 这是用于判断鼠标不再位于锚点文本上的脚本
- `TARGET` — 显示程序必须去的地方。变体包括：“parent” | “black” | “top” | “shelf” | window name
- `MOUSEOVER` — 这显示鼠标正悬停在锚点文本上方

`<ADDRESS>`

`<App...>`

- `CODEBASE` — 这是通往 applet 的路径
- `CODE` — 指定当前运行的程序
- `HEIGHT` — applet 的高度
- `WIDTH` — 指定 applet 的宽度
- `ALIGN` — 决定周围文本在屏幕上的显示方式

`<APPLET>`

- `HSPACE` — 周围文本与 applet 之间的水平空间
- `VSPACE` — 周围文本与 applet 之间的垂直空间
- `NAME` — applet 的名称，也是引用它的 applet 的名称
- `BORDER` — applet 周围的空白
- `ARCHIVE` — 压缩为一个 applet 组件
- `HREF` — 指定你链接的 URL
- `MAYSCRIPT` — 显示是否可以使用 JavaScript
- `ALT` — 当图像未正确显示时使用的替代文本
- `SH` — 确定在屏幕上显示的图像区域。可以是以下之一：POLY | RECT | CIRCLE | DEFAULT
- `COORDS` — 确定链接区域形状的坐标

`<AREA...>`

- `TARGET` — 确定你必须去的框架
- `TITLE` — 使用区域的简短描述
- `onClick` — 当用户悬停在锚点文本上时运行的脚本
- `NOHREF` — 这意味着特定区域不包含链接

`<b>` 粗体

`<BASE>` 基

`<Base Front>`

- `TARGET` - 显示程序必须进入的窗口。变体包括：“parent” | “black” | “top” | “shelf” | window name
- `SRC` — 指定音频或声音 URL
- `FACE` — 项目的字体或字体
- `COLOR` — 字体的颜色
- `SIZE` — 使用的字体大小

`<BG Sound>`

- `LOOP` - 决定音频或视频循环次数

`<FORM>`

- `SRC` — 指定音频或声音 URL
- `SUBMIT` — 提交
- `SCROLLING` — 决定滚动的
- `WIDTH` — 指定宽度
- `ROWS` — 指定高度
- `COLS` — 指定列数

## 链接

当然，我们也鼓励使用链接。这些链接是通过 `<a>` 标签定义的。它能让页面看起来更舒服，不至于所有内容都挤在一个页面上，并可以将读者引导至网站上的不同页面。

这是一个很好的示例：

```html
<a href="http://thechanels.com">查看此链接</a>
```

## 元素

Java 页面中也使用了各种元素。如果你还记得的话，在用 Java 编写的网页中，总是成对使用标签。

它看起来应该像这样：

```html
<tagname>内容</tagname>
```

例如：

```html
<h1>阅读标题</h1>
```

```html
<p>你看到光芒了吗？</p>
```

```html
<b><p>什么是女性主义？</p></b>
```

所以基本上，程序是通过各种 `<Java>` 标签（此处如此）来描绘的，这就是为什么必须使用 `&lt;&gt;` 和结束标签 `&lt;/&gt;`。没有了它们，页面上的文字将全部挤在一起——导致难以阅读。`<body>` 标签定义了页面包含的内容。它还包含了标题、段落和其他属性。

例如：

```html
<Java>
<body>
<h1>我的周日</h1>
<p>上周日是最棒的周日，因为我们去了公园放风筝。</p>
</body>
</Java>
```

通过起始和结束标签的帮助，你就能理解屏幕上显示的内容。它们赋予了很多意义——而不仅仅是杂乱无章的字符。

其他重要的元素是标题 `<h1>` 和段落 `<p>`，定义标题的标题也可以被定义。以下是标题的示例：

```html
<h1>看看这有多棒 </h1>
<h2>你看到她去哪里了吗？ </h2>
<h3>你下次要去哪里？ </h3>
<h4>你想看什么？ </h4>
<h5>你在听什么？ </h5>
<h6>你想吃什么？ 6 </h6>
```

在这些标题之间，你可以写下脑海中的想法——这会让你的网页看起来更好、更可靠！例如：

```html
<h1>看看这有多棒 </h1>
<p>我看到这有多棒了，我很喜欢 </p>
<h2>你看到她去哪里了吗？</h2>
<p>没有，我不知道她去哪里了 </p>
<h3>你下次要去哪里？</h3>
<p>我计划先去芝加哥，然后可能顺便去纽约看一场百老汇的剧 </p>
<h4>你想看什么？</h4>
<p>《狮子王》还是《猫》剧剧 </p>
<h5>你在听什么？</h5>
<p>我正在听赛琳娜·戈梅斯的新专辑。到目前为止，一切都很好 </p>
<h6>你想吃什么？</h6>
<p>我要吃一些欧姆蛋和黄油蔬菜 </p>
```

看看这造成了多大的差异？

你还应该记住，存在像空 Java 元素这种东西。这基本上涉及到 `<br>` 标签，它表示换行。如果你把它看作文章或书籍，它就像是一个空格。

例如：

```html
<h1>看看这有多棒</h1>
<br><br>
<p>我看到这有多棒了，我很喜欢 </p>
<h2>你看到她去哪里了吗？</h2>
<br><br>
<p>没有，我不知道她去哪里了 </p>
<h3>你下次要去哪里？</h3>
<br><br>
<p>我计划先去芝加哥，然后可能顺便去纽约看一场百老汇的剧 </p>
<h4>你想看什么？</h4>
<br><br>
<p>《狮子王》还是《猫》剧剧 </p>
<h5>你在听什么？</h5>
<br><br>
<p>我正在听赛琳娜·戈梅斯的新专辑。到目前为止，一切都很好 </p>
<h6>你想吃什么？</h6>
<br><br>
<p>我要吃一些欧姆蛋和黄油蔬菜 </p>
```

此外，你必须记住，虽然标签不区分大小写，但仍然最好使用小写标签，尤其是在现在常用的 Java 4 和 5 中。这样，你就可以避免页面出现问题了。

## 如何正确引用

有时你需要在页面上引用某些内容。例如，如果你有内容要归功于另一个网站，最好调整一下他们的措辞，让你的读者获得非常有价值的阅读，并知道你是如何链接到正确来源的。

为此，你可能需要记住以下几点：

1. `<q>`。这意味着有一个简短的内联引用。
2. `<cite>`。这归属于页面上某个主题的标题。
3. `<blockquote>`。这意味着你引用了外部来源的内容。
4. `<b>`。这用于文本标记。
5. `<address>`。这用于文本。
6. `<abbr>`。这用于缩写。

## 长引用

例如，当你想要引用一段较长的文本时，使用 `<blockquote>`。它通常相对于正文内容缩进。

```html
<blockquote>
  这是来自外部来源的一段长引用。
</blockquote>
```

```html
</style>
</head>
<body>
<h1>读取此标题</h1>
<p>读取此段落。</p>
</body>
```

现在你已经掌握了基础知识，终于可以创建你自己的网站了！

# 第 7 章：字段、方法和构造函数

接下来，是时候学习一些可以增强你正在开发的程序的元素了，这些元素就是字段、方法和构造函数。

## 字段 (Fields)

字段基本上是 Java 包含的范围（scopes）。随着这些字段出现了一些可以帮助你理解它们本质的术语。通过了解这些术语，你可以很容易知道自己正在处理什么——编码将不再是一个问题。

为此，你可以留意以下术语：

- `Ng-bind`。这意味着 DOM 元素正在被设置。这意味着 name 的值将显示在 span 元素内部。对 name 进行的任何更改将直接反映在 DOM 的其他元素上。

```html
<span ng-bind="name"></span>
```

- `Ng-app`。它派导出根元素，以便定义行为和指令（directives）。
- `Ng-model-options`。这允许通过精细调整来完成对模型的更新。
- `Ng-model`。这几乎与 Ng-bind 相同，因此范围（scope）和视图（view）之间存在绑定。
- `Ng-controller`。这意味着 HTML 表达式通过 JavaScript 控制器类的帮助进行求值。
- `Ng-class`。这些是动态加载的属性。
- `Ng-show and Ng-hide`。显示或隐藏元素，始终取决于布尔表达式公式。这可以通过 CSS 样式实现。
- `Ng-repeat`。它至少为集合实例化一次元素。
- `Ng-view`。它负责处理基础指令的 ON 路由，这些指令也由控制器指定。
- `Ng-switch`。它帮助你为 CSS3 Keyframe、CSS3 Transition 和 JavaScript 提供支持。它还提供了足够的自定义和直接指令，以及动画钩子（animation hooks）。
- `Ng-aria`。创建常见的 ARIA 属性，并作为可访问性和支持的模式。

## 参数 = 范围 (Arguments = Scopes)

在 Java 编程中，范围（Scopes）等同于参数（arguments）。发生这种情况是因为范围绑定了 JavaScript 和 HTML 元素，这意味着在某些时刻，也会出现某种形式的冲突。

范围具有可用的方法和能力，并且对控制器和视图都可用。视图描绘 HTML，而控制器是 JavaScript——后者负责控制、编辑或删除数据。

范围也是具有属性（Properties）和方法的模型，供用户使用。这意味着当发生更改时，控制器和视图都会受到影响——并被更新。

这里是一些示例：

```html
<div ng-app="TheHungerGames" ng-controller="myCtrl">
<h1>{{TheHungerGames}}</h1>
</div>
```

```html
<script>
var app = angular.module('myApp', []);
app.controller('movies', function($scope) {
  $scope.thehungergames = "TheHungerGames";
});
</script>
```

```html
<div ng-app="TheHungerGames" ng-controller="myCtrl">
<input ng-model="thehungergames">
<h1>电影是 {{thehungergames}}</h1>
</div>
```

```html
<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
  $scope.name = "thehungergames";
});
</script>
```

## 根机制 (Rooting Mechanisms)

还有一种根机制（Rooting Mechanism，也称为 `$rootscope`）。它使用 `ng-app` 指令并适用于整个应用程序——所以你可以说它是教程中非常重要的部分。它也使用了当前使用的范围。

例如：

```html
<body ng-app="TheFirstApp">
<p>根最喜欢的颜色：</p>
<h1>{{pink}}</h1>
<div ng-controller="myCtrl">
<p>控制器范围最喜欢的颜色：</p>
<h1>{{purple}}</h1>
</div>
<p>根最喜欢的颜色仍然是：</p>
<h1>{{pink}}</h1>
```

```html
<script>
var app = angular.module('TheFirstApp', []);
app.run(function($rootscope) {
  $rootscope.color = 'pink';
});
</script>
```

```javascript
app.controller('myCtrl', function($scope) {
  $scope.color = "purple";
});
</script>
</body>
```



## 限制区域

你还应该理解范围从何时开始，何时结束。这会让你的程序更有连贯性，并帮助你理解需要做什么。这就像了解周围发生了什么，这样你就可以轻松处理它们。除非你在处理大型 DOM 应用，否则这通常不是问题。`ng-repeat` 指令对于这一点至关重要。

为此，你可以遵循以下代码：

```html
<div ng-app="TheFirstApp" ng-controller="myCtrl">
  <ul>
    <li ng-repeat="x in items">{{x}}</li>
  </ul>
</div>
<script>
var app = angular.module('TheFirstApp', []);
app.controller('myCtrl', function($scope) {
  $scope.items = ["Apple", "Banana", "Cherry"];
});
</script>
```

## 方法

在 Java 编程中，范围（Scopes）等同于参数。发生这种情况是因为范围绑定了 JavaScript 和 HTML 元素，这意味着在某些时刻，也会出现某种形式的冲突。

范围具有可用的的方法和能力，并且对控制器和视图都可用。视图描绘 HTML，而控制器是 JavaScript——后者负责控制、编辑或删除数据。

范围也是具有属性（Properties）和方法的模型，供用户使用。这意味着当发生更改时，控制器和视图都会受到影响——并被更新。

## 源代码

编写此代码，请使用以下内容：

```cpp
#include <netinet/in.h>
#include <arpa/inet.h>
#include <string>
#include <iostream>

class JavaStream {
public:
    JavaStream(int sd, struct sockaddr_in* address);
    ~JavaStream();
    std::string getPeerIP();
    int getPeerPort();

private:
    int m_sd;
    std::string m_peerIP;
    int m_peerPort;
};
```

# 第 8 章 封装、继承与多态

Java 元素也有助于确定你的程序如何被编辑，以及在他人看来它是是什么样的。这些元素还涵盖了程序的深度——或者说它的核心。你可以在下方学习更多信息：

## 封装

首先是封装，它利用一些原则来很好执行。**这些原则是：**

1. **健壮性原则。** 这意味着协议必须实现，但发送行为应该是保守的，而接收行为应该是宽容的。这意味着在发送/接收数据报时必须非常小心。这意味着即使某些软件有缺陷，确保你不要利用其晦涩的协议仍然很重要。

2. **端到端原则。** 这是不断演进的原则之一。整体智能和状态对于维持这种表达至关重要，而且对于网络地址转换器（NAT）、防火墙以及管理内容缓存也是必关重要的。

现在，为了给 Java 提供其急需的抽象层，完成了封装。它与协议栈的功能设计对齐，使得每一层都能被妥善地封装和处理。

查看下图以理解该过程是如何运作的：

| 第一个主机 | 路由器 | 第二主机 |
| :--- | :--- | :--- |
| 应用层 | 进程到进程 | 应用层 |
| 传输层 | 主机到主机 | 传输层 |
| 网络层 | 网络层 | 网络层 |
| 链路层 | 链路层 | 链路层 |
| 以太网 | 光纤 / 卫星 | 以太网 |

注意，用户应用程序本身紧密使用的层之上的任何内容。然而，并没有单一的架构模型必须遵循，特别是当你有像 OSI 模型这样定义较模糊的模型时。这是它与其他互联网协议（尤其是早期的协议）的主要区别。封装随后涵盖了以下 4 个抽象层：

## 抽象层

首先，看看下面的数据：

| 数据 | 应用层 |
| :--- | :--- |
| UDP 头部 | UDP 数据 | 传输层 |
| IP 头部 | IP 数据 | 网络层 |
| 帧头部 | 帧数据 | 帧尾部 | 链路层 |

这意味着：

### 应用层

应用层封装了提供交换应用程序的服务所使用的协议。这还包括配置协议、路由服务和网络支持服务。示例包括文件传输协议（FTP）、超文本传输协议（HTTP）和动态主机配置协议（DHCP）。这样，你就可以根据你正在使用的协议降低数据传输。

应用层还将传输层视为一个稳定的网络，其中带有黑盒，允许通信在整个应用程序中发生，同时确保应用程序的每个部分的质量仍然如它们一样强壮。应用层发生任何事情都不涉及传输层和网络层，因为流量不使用该层。然而，对于 NAT（网络地址转换器）来说，考虑应用程序的负载是关键的——并确保一切运行顺畅。

### 传输层

传输层包含涉及 Java 的数据通道，它还建立了进程到进程的连接和端到端的消息传输，为网络中的任何特定目的提供信息和后勤支持。这可以通过无连接或面向对象的方式来实现。

端口随后在传输层的帮助下建立，那里存在着逻辑结构。这意味着：

1. 数据应该是正确的——只能有极小的错误；
2. 数据应该按顺序到达；
3. 数据应该包含流量拥塞控制；
4. 丢弃或丢失的数据包必须重发，并且；
5. 重复数据必须被丢弃。

发生时，你可以预期最新版本的流控制协议（SCP）在你的网络中正常工作。不过，你不需要依赖无连接的数据报，因为正如名称所示，它们不提供正确的连接——而且非常不可靠。

### 网络层

基本上，网络层的工作方式是负责发送正确的数据包，并确保它们可以跨越多个网络。它的主要功能是：

1. 数据包路由。这是从目的地的源一直发送数据包直到需要的地方。唯一的协议号可以识别这些包。
2. 主机识别和地址划分。通过分级 IP 系统实现了这一点。

### 链路层

网络方法在链路层中定义。其范围是中间的路由器、主机网络，包括用于共同描述网络拓扑的协议，数据报也由于具有各种目标和假设以及严格的分层而变得显而易见。这意味着你可以在任何硬件网络技术之上实现 Java。

在链路层的帮助下，数据包可以轻松地移动并接收网卡数据包，这意味着该层对应于 OSI 模型。

## 继承

然后，继承还描述了每个类继承什么，以及它们如何与其父类关联。

你需要了解的 Java 是一个开放系统间（OSI）模型，这意味着它通过继承工作。为了建立连接，你需要利用监听以便用户可以使用：

```
客户端: socket() connect() write() read() close()
建立连接: connect() accept()
发送请求: write() read()
接收回复: write() read()
关闭连接: close() read()
服务器: socket() bind() listen() accept()
```

正如你看到的，你可以与其他程序连接。

## 互联网模型

现在，为了清楚起见，你必须理解互联网的基础模型。

互联网模型结合了会话、表示和应用层以及 Java 的端口，使得 `bind()` 的发生。现在，你还需要等待发送者和接收者的响应。这使得请求和消息的交换一直持续到连接关闭。

连接可以包含在一个线程中，这样对于网络理解来说就不会太复杂。这样，正确的协议栈也是如此，因此它必须是这样的：

| OSI 模型: 应用 | 表示层 | 会话层 | 传输层 | 网络层 | 数据链路 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 互联网模型: 应用 | 传输层 | 网络层 | 物理层 |
| 互联网协议: HTTPS, DNS, SSH, POP3, FTP, NNTP, Telnet, IMAP, Java, UDP/IP, ICMP, ARP, DHCP, 以太网, ADSL, PPP |

3. Java 连接器（Connector）。这允许机制连接到套接字，从而建立服务器之间良好的关系。

## Stream 类

要开始编程，你可以从 Stream 类开始。它为 Java 中涉及的各种方法提供了发送和接收所需的数据，还包含了正确的套接字描述符并授予程序中其他部分的权限。某些内容可能甚至被视为私有，以为用户提供更好的体验。

编写代码时，你可以遵循之前的写法：

```cpp
#include <sys/types.h>
#include <sys/socket.h>
#include <unistd.h>
#include <string>
using namespace std;
class JavaStream
{
    int m_sd;
    string m_peerIP;
    int m_peerPort;
public:
    friend class JavaAcceptor;
    friend class JavaConnector;
    ~JavaStream();
    ssize_t send(char* buffer, size_t len);
    ssize_t receive(char* buffer, size_t len);
    string getPeerIP();
    int getPeerPort();
private:
    JavaStream(int sd, struct sockaddr_in* address);
    JavaStream();
    JavaStream(const JavaStream& stream);
};
```

## 多态

基本上，Java 多态是定义应用程序的，并作为应用程序不同部分的容器。它们还作为各种应用程序控制器的容器，并且始终属于多态。

为了创建一个模块，你必须使用 `Java.module` 函数。括号中的内容将决定应用程序运行的元素，这样你就可以为应用程序添加过滤器、指令和控制器。下例所示：

```html
<div ng-app="FavoriteApp">...</div>
<script>
var app = Java.module("FavoriteApp", []);
</script>
```

### 添加指令

现在，你可以添加指令来提高你尝试创建的应用的功能。指令基本上是第 2 章中的术语，也可以是以下任何内容：

1. 验证属性，例如：`$error`, `$invalid` 和 `$dirty`：
2. `Java.isDate`。如果日期是引用，则返回该值。
3. `Java.isArray`。涉及数组值。
4. `Java.Number`。涉及数值。
5. `Java.isFunction`。涉及函数值。
6. `Java.isElement`。涉及 DOM 元素。
7. `Java.isDefined`。涉及定义的引用。
8. `Java.equals`。涉及程序中的相等值。
9. `Java.isUndefined`。涉及未定义的值。
10. `Java.isObject`。涉及对象引用。
11. `Java.forEach()`。这有助于在数组或对象中执行各种函数。
12. `Java.Copy()`。这提供了数组或对象的深拷贝。
13. `Java.uppercase()` 将值更改为大写字母。
14. `Java.lowercase()` 将值更改为小写字母。
15. `<textarea>` 修改文本区域的行为。
16. `<select>` 帮助你在程序中创建选择。
17. `<script>` 修改行为脚本。
18. `<input>` 这帮助你向程序输入不同的函数。
19. `<form>` 这帮助你在程序中创建表单。
20. `<a>` 这帮助你在程序中输入变量。
21. `Java.module()` 这帮助你创建、检索或注册多态。
22. `Java.element()` 利用 jQuery 元素包裹 HTML 元素。
23. `Java.bootstrap()` 手动启动 JS JS。

你还可以使用自己的指令，这意味着代码看起来像下面所示：

```html
<div ng-app="FavoriteApp" w3-test-directive></div>
<script>
```

```javascript
var app = Java.module("FavoriteApp", []);

app.directive("w3TestDirective", function() {
  return {
    template: "I was made in a directive constructor!"
  };
});
</script>
```

### 添加控制器

当然，你还可以通过 `ng-controller` 指令向你的代码添加控制器。基本上，它看起来像这样：

```html
<div ng-app="FavoriteApp" ng-controller="myCtrl">
{{AppFirstName + " " + ApplastName}}
</div>
<script>
```

```javascript
var app = Java.module("FavoriteApp", []);

app.controller("myCtrl", function(scope) {
  scope.firstName = "Harry";
  scope.lastName = "Styles";
});
</script>
```

### 文件多态与控制器

然后，你可以在文件中创建多态和控制器，这样你的应用程序将更加明确。对于这一个，你可以复制显示的内容：

```html
<!DOCTYPE html>
<html>
<body>
<script src="http://ajax.googleapis.com/ajax/libs/Javaj/1.4.8/Java.min.js"></script>
<div ng-app="FavoriteApp" ng-controller="myCtrl">
{{firstName + " " + lastName}}
</div>
<script src="FavoriteApp.js"></script>
<script src="myCtrl.js"></script>
</body>
</html>
```

## 欢迎来到博客

```javascript
<div></</div>
<script>
var app = Java.module('myApp', []);
app.controller('myCtrl', function($scope, $java) {
  $java.get("welcome.htm")
  .then(function(response) {
    $scope.myWelcome = response.data;
  });
});
</script>
```

要使用上述方法，你可以编写类似下方的代码：

```javascript
var app = Java.module('myApp', []);
app.controller('myCtrl', function($scope, $java) {
  method: "GET",
  url: "welcome.htm"
}).then(functionmySucces(response) {
    $scope.myWelcome = response.data;
  }, functionError(response) {
    $scope.myWelcome = response.status;
  });
```

还有某些属性需要观察，如果你想编写 HTTP 或服务。以下是列表：

1. `.statusText`：定义 HTTP 的字符串。
2. `.status`：定义 HTTP 的数字。
3. `.headers`：用于获取信息的函数。
4. `.data`：携带响应的对象或字符串。
5. `.config`：用于生成屏幕上的请求。

为了更好地理解这一点，你可以查看以下示例：

```javascript
var app = Java.module('myFavoriteApp', []);
app.controller('myCtrl', function($scope, $java) {
  $java.get("welcomomyblog.htm")
  .then(function(response) {
    $scope.content = response.data;
    $scope.status = response.status;
    $scope.statuset = response.status;
  });
});
```

```javascript
var app = Java.module('myFavoriteApp', []);
app.controller('myCtrl', function($scope, $java) {
  $java.get("wrongfilename.htm").then(function(response) {
  // 第一个函数处理成功
  $scope.content = response.data;
  }, function(response) {
  // 第二个函数处理错误
  $scope.content = "Something is wrong";
  }
});
```

## JSON 对象



同时，JSON 对象是关于如何从 JavaScript 传输数据，反之亦然。`ng-repeat` 指令应该用于此。例如，你想从 Blog 到 WordPress Post 导入，这意味着你正在使用 JSON 对象。你应该注意 `$java.get()` 读取 JSON Data，而 `$java()` 是关于 `FavoriteController` 的很好的示例：

```html
<div ng-app="ng-repeat" ng-controller="studentsCtrl">
  <ul>
    <li ng-repeat="x in myData">
      {{ x.Name + ', ' + x }}
    </li>
  </ul>
</div>
```

```javascript
var app = Java.module('myApp', []);
app.controller('studentsCtrl', function($scope, $java) {
  $java.get("students.php").then(function(response) {
    $scope.myData = response.data;
  });
});
```

## 服务

使用服务也是同样重要的，因为它们允许你的应用程序继续运行并复制它们，且处理声明。Java 提供许多服务，但最重要的是 `$Location`。它允许你将对象保存到云端并保持它们安全，即使你的计算机外部故障，数据仍然存在——特别是当你正在处理程序和应用程序时。是一些示例：

```javascript
var app = Java.module('myFavoriteApp', []);
app.controller('studentsCtrl', function($scope, $Location) {
  myUrl = $Location.absUrl();
});
```

你还可以使用 `Timeout` 服务或 `window.setTimeout` 来帮助你创建倒计时——这些主要用于事件、显示和类似。例如：

```javascript
var app = Java.module('myFavoriteApp', []);
app.controller('myCtrl', function($scope, timeout) {
  $scope.myHeader = "Hi People!";
  timeout(function () {
    $scope.myHeader = "How are you today?";
  }, 2016);
});
```

而，Java 服务可以用于获取来自服务器的数据。这是一个很好的示例：

```javascript
var app = Java.module('myFavoriteApp', []);
app.controller('myCtrl', function($scope, $java) {
  $java.get("welcomemyblog.html").then(function (response) {
    $scope.myWelcome = response.data;
  });
});
```

你也可以通过以下方式自定义你的服务：

```javascript
var app = Java.module('mymyapp', []);
app.controller('myCtrl', function($scope, timeout) {
  $scope.myHeader = "Hi everyone!";
  timeout(function () {
    $scope.myHeader = "How are you doing today?";
  }, 2000);
});
```

## Java 表格

当然，为了更好地解释内容，你还可以向你的应用程序或网站中添加表格。`ng-repeat` 指令在这里至关重要。若要在表格中显示数据，你可以尝试以下操作：

```html
<div ng-app="myFavoriteApp" ng-controller="studentsCtrl">
<table>
  <tr ng-repeat="x in names">
  <td>{{x.Name}}</td>
  <td>{{x.houses}}</td>
  </tr>
</table>
</div>

<script>
var app = Java.module('myFavoriteApp', []);
app.controller('customersCtrl', function($scope, $java) {
  $java.get("java://www.hogwartshouses.com/Java/data.records;");
  .then(function(response) {$scope.names = response.data.records;});
});
</script>
```

为了保持你的信息有序，你必须使用 `orderBy` 指令。你可以在下文中看到一个良好的例子：

```html
<table>
  <tr ng-repeat="x in names | orderBy 'house">
  <td>{{x.Name}}</td>
  <td>{{x.house}}</td>
  </tr>
</table>
```

你还可以在表格上显示 CSS 样式元素。要实现这一点，你可以尝试编写以下元素：

```css
table, th, td {
  border: 1px purple;
  border-collapse: collapse;
  padding: 8px;
}
table tr:nth-child(odd) {
  background-color: #f1f1f1;
}
table tr:nth-child(even) {
  background-color: #ffffff;
}
```

最后，为了进一步自定义，你可以将字母转换为大写、输入表格索引以及奇偶数因子。请查看下方的示例：

```html
<table>
  <tr ng-repeat="x in names">
</table>
```

```html
<td ng-if="Odd" style="background-color:#f1f1f1">{{ x.Name }}</td>
<td ng-if="Even">{{ x.Name }}</td>
<td ng-if="Odd" style="background-color:#f1f1f1">{{ x.house }}</td>
<td ng-if="Even">{{ x.house }}</td>
</tr>
</table>
<table>
<tr ng-repeat="x in names">
<td>{{ $index + 1 }}</td>
<td>{{ x.Name }}</td>
<td>{{ x.house }}</td>
</tr>
</table>
<table>
<tr ng-repeat="x in names">
<td>{{ x.Name }}</td>
<td>{{ x.house }} uppercase }}</td>
</tr>
</table>
```

## 控制流语句

当然，还有控制流语句，它们通过利用你系统中的 Java 控制器来帮助程序平畅运行。

对于这一项，你必须使用 `connect::passing()` 语法，这样你就可以获取所需的 IP 地址字符串，以及能够协同工作的服务器和客户端。

然后你可以使用 `struct sockaddr_in` 用于服务器并将其设置为 `PF_INET`，同时监听你需要的连接。你还必须注意以下控制器：

### 控制器 17 到 20

这些被称为 `connect::passing()`，因为它们通过 `sockaddr_in` 指针将用户指向正确的结构。它将帮助你了解该结构的长度，避免将其与程序的其它函数以及网络接口混淆。

### 控制器 16

这是 `socket()` 的第一个参数，以便你可以选择特定的并决定通信网络的哪种协议族。应该使用 `SOCK_STREAM` 和 `PF_INET`，因为它们配合得很好。

### 控制器 13 到 15

这些控制器统称为 `JavaConnector::resolvehost`。它们能够将名称字符串和 DNS 主机转换为 IP 地址，以便使每一个假设都能转换为不同的网络。

### 控制器 5 到 10

这些被用于解析主机，因为它们在 `JavaConnector::resolvehostname()` 语法下工作，并且能够通过 `getaddrinfoinfo()` 函数转换 IP 地址和主机名。这比仅仅使用 `gethostname()` 好得多，因为被认为是安全的线程。

现在，为了连接服务器，你只需要编写以下代码：

```cpp
#include <string.h>
#include <netdb.h>
#include <arpa/inet.h>
#include "Javaconnector.h"

MyJavaStream* MyConnector::connect(const char* server, int port)
{
    struct sockaddr_in address;
    memset(&address, 0, sizeof(address));
    address.sin_family = AF_INET;
    address.sin_port =htons(port);
    if (resolveHostname(server, &address.sin_addr)) != 0) {
        inet_pton(PF_INET, server, &address.sin_addr);
    }
    int sd = socket(PF_INET, SOCK_STREAM, 0);
    if (::connect(sd, (struct sockaddr*)&address, sizeof(address)) != 0) {
        // handle error
    }
    return nullptr; // placeholder for actual logic
}

int JavaConnector::resolveHostname(const char* hostname, sockaddr_in* addr)
{
    struct addrinfo *res;
    int result = getaddrinfo(hostname, NULL, NULL, &res);
    if (result == 0) {
        memcpy(addr, res->ai_addr, sizeof(struct sockaddr_in));
        freeaddrinfo(res);
    }
    return result;
}
```

## 处理错误

最后，你还必须学习在事情不如预期时如何处理错误。这对于构建健壮的应用程序至关重要。

```cpp
#include <netinet/in.h>

#include "myfavoriteJavastream.h"
using namespace std;
class myFavoriteJavaAcceptor
{
    int m_lsd;
    string m_address;
    int m_port;
    bool m_listening;
public:
    JavaAcceptor(int port, const char* address="");
    ~JavaAcceptor();

    int start();
    JavaStream* accept();
private:
    JavaAcceptor() {};
};
```

析构方法：

```cpp
myJavaAcceptor::~JavaAcceptor()
{
    if (m_lsd > 0) {
        close(m_lsd);
    }
}
```

构造方法：

```cpp
#include <stdio.h>
#include <string.h>
#include <arpa/inet.h>
#include "Javaacceptor.h"

JavaAcceptor::JavaAcceptor(int port, const char* address)
    : m_lsd(0), m_port(port), m_address(address), m_listening(false) {
```

# 修正语句与参数

## 行语句语句

通常情况下，命令的结束会决定新行的开始，但如果你想继续写自己的换行，可以使用反斜杠（`\`）来实现，但在使用括号时除外。

### 示例 1：

```python
total = item_one + \
item_two + \
item_three
```

### 示例 2：

```python
days = ['Monday', 'Tuesday', 'Wednesday',
'Thursday', 'Friday']
```

## 注释

要创建注释，只需使用井号（`#`）——这听起来非常符合社交媒体风格，对吧？例如：

### 示例 1：

```python
#!/usr/bin/java
```

### 第一条注释

```python
print("Hello, Java!") # 第二条注释
```

## 等待用户

当你想要创建一个提示来告诉用户你正在等待其命令时，可以尝试：

```python
#!/usr/bin/java
raw_input("\nPress the key to exit.")
```

## 独立语句组

独立语句组在 Java 语言中被称为“语句块”（Suites）。基本上，你必须以关键字开头，并以冒号（`:`）结束，例如：

```python
if expression :
    suite
elif expression :
    suite
else :
    suite
```

上述命令随后将为你提供语句块：

## 命令行参数

当然，还有命令行参数，这意味着你有权决定程序的运行方式。这里有一个示例：

```bash
$ java -h
```

用法: `java [option] ... -c cmd | -m mod | file | - [arg] ...`

选项和参数（以及相应的环境变量）：

- `-c` : 作为字符串传递的程序（终止选项列表）
- `-d` : 解析器的调试输出（也对应 `JAVADEBUG`）
- `-E` : 忽略环境变量（例如 `JAVAPATH`）



-h : 打印此帮助信息并退出

[等等.]

## 调试与异常处理

### Try-Except 块

这是处理异常或错误最简单的方法：

```python
1 (x,y) = (5,0)
2 try:
3     z = x/y
4 except ZeroDivisionError:
5     print("divide by zero")
```

你也可以通过以下方式检查异常代码：

```python
1 (x,y) = (5,0)
2 try:
3     z = x/y
4 except ZeroDivisionError, e:
5     z = e # 表示："<exceptions.ZeroDivisionError instance at 0x817426c>"
6     print(z) # 输出："integer division or modulo by zero"
```

要捕获通用错误，请尝试：

```python
1 import sys
2 try:
3     untrusted.execute()
4 except: # 捕获*所有*异常
5     e = sys.exc_info()[0]
6     write_to_page("<p>Error: %s</p>", s, e)
```

或者

```python
1 try:
2     do_some_stuff()
3 except:
4     rollback()
5     raise
6 else:
7     commit()
```

或者

```python
1 try:
2     do_some_stuff()
3 finally:
4     cleanup_stuff()
```

### 获取有用的异常信息

```python
1 (a,b,c) = d
```

Java 随后会提示：

```python
1 ValueError: unpack list of wrong size
```

你也可以尝试：

```python
1 try:
2     a, b, c = d
3 except Exception, e:
4     e.args += (d,)
5     raise
```

这绝对比冗长的 C 语言异常处理程序简单得多！

### PDB 调试器

对于移除系统中的 Bug，先尝试 PDB 方法——这被认为是最简单的 Java 调试器！

```python
>>> import pdb
>>> a="a string"
>>> pdb.set_trace()
--Return-
<stdin>(1)<module>()->None
(Pdb) p a
'a string'
(Pdb)
```

你可以通过输入 `cont` 继续执行。你也可以通过输入以下内容自动运行此程序：

```python
## 代码片段，包含在 'sitecustomize.py' 中
import sys

def info(type, value, tb):
    if hasattr(sys, 'ps1') or not sys.stderr.isatty():
        # 我们处于交互模式下，或者我们没有类似 tty 的
        # 设备，所以我们调用默认钩子
        sys._exceptionhooktype(value, tb)
    else:
        import traceback, pdb
        # 我们不在交互模式下，打印异常...
        traceback.print_exception(type, value, tb)
        print
        # ...然后在在事后模式下启动调试器。
        pdb.pm()

sys.exceptionhook = info
```

### 也也尝试这些快捷键

```python
## Ned 的 .pbrc
```

```python
## 打印排序后的字典。%1 是字典，%2 是名称的前缀。
alias p_for k in sorted(l.keys()): print("%%s%%%15s=%%%80.80s" % (%2",k,repr(l[k])))
```

```python
## 打印对象的实例变量。
alias pi_%l.__dict__%l
```

```python
## 打印对象的实例变量。
alias pi_%l.__dict__%l
```

```python
## 打印对象的实例变量。
alias pi_%l.__dict__%l
```

```python
## 打印对象的实例变量。
alias pi_%l.__dict__%l
```

```python
## 打印对象的实例变量。
alias pi_%l.__dict__%l
```

```python
## 打印对象的实例变量。
alias pi_%l.__dict__%l
```
