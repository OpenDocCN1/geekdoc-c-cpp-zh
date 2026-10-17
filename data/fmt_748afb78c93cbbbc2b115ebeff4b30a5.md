
- 包含有效对象的数组或用于表示缺失有效对象的 `null` 引用。（此主题在准则 41 中有进一步讨论，“对于返回数组或集合的方法，请返回空数组或集合而不是 `null` 值。”）

带内错误指示要求调用者检查错误情况；然而，这种检查往往会被忽略。未能检查此类情况不仅违反了《CERT® Oracle® Java 安全编码标准》[Long 2012] 中提到的“EXP00-J. 不要忽略方法返回的值”，还会产生一个遗憾的后果，即传播了无效值，这些无效值在随后的计算中可能会被视为有效值。

避免使用带内错误指示。在 Java 核心库中，它们比其他编程语言少得多；尽管如此，它们仍被用于 `java.io` 中的 `read(byte[] b, int off, int len)` 和 `read(char[] cbuf, int off, int len)` 系列方法。

在 Java 中，指示异常情况的最佳方法是抛出异常而不是返回错误代码。异常跨范围传播，并且不像错误代码那样容易被忽略。使用异常时，错误检测和错误处理代码与主控制流分离。

## 不合规代码示例

此不合规代码示例尝试读取字符到字符数组中，并在读取字符后立即在缓冲区中添加一个额外的字符。

```
static final int MAX = 21;
static final int MAX_READ = MAX - 1;
static final char TERMINATOR = '\\';
int read;
char[] chBuff = new char[MAX];
Buffered buffRdr;

// 设置 buffRdr

read = buffRdr.read(chBuff, 0, MAX_READ);
chBuff[read] = TERMINATOR;
```

如果输入缓冲区初始处于文件末尾，`read()` 方法将返回 `-1`，而尝试放置终止符将抛出 `ArrayIndexOutOfBoundsException`。

### 合规解决方案（包装）

此合规解决方案定义了一个 `readSafe()` 方法，它封装了原始的 `read()` 方法并在检测到文件末尾时抛出异常：

```
public static int readSafe(BufferedReader buffer, char[] cbuf,
    int off, int len) throws IOException {
    int read = buffer.read(cbuf, off, len);
    if (read == -1) {
        throw new EOFException();
    } else {
        return read;
    }
}

// ...

BufferedReader buffRdr;

// 设置 buffRdr
```

## 53. 不要在条件表达式中执行赋值

```
try {
  read = readSafe(buffRdr, chBuff, 0, MAX_READ);
  chBuff[read] = TERMINATOR;
} catch (EOFException e) {
  chBuff[0] = TERMINATOR;
}
```

### 适用性

使用带内错误指示可能导致程序员未能检查状态码或使用了错误的返回值，导致意外行为。

鉴于 Java 中带内错误指示出现频率较少，可能会列出所有使用它们的标准库方法列表并自动检测它们的使用。然而，在通用情况下检测带内错误指示的使用是不可行的。

失败时返回可能为 `null` 的对象或成功时返回有效对象是带内错误指示的一个常见示例。尽管通常有更好的方法设计，但在某些情况下，返回一个可能为 `null` 对象是可以接受的。示例参见准则 26，“始终提供关于方法结果结果的反馈”。

### 参考文献

- [API 2013] 类 `Reader`
- [JLS 2013] 第 11 章，“异常”
- [Long 2012] EXP00-J. 不要忽略方法返回的值

## 53. 不要在条件表达式中执行赋值

在条件表达式中使用赋值运算符通常意味着程序员错误，并可能导致意外行为。

作为此准则的例外，当赋值不是条件表达式本身（即赋值是一个子表达式）时，允许在条件表达式中使用赋值运算符，如下合规解决方案所示。

```java
public void assignNontrol(BufferedReader reader)
    throws IOException {
    String line;
    while ((line = reader.readLine()) != null) {
        // 处理 line
    }
}
```

### 参考文献

- [Hatton 1995] §2.7.2, “遗漏与添加错误”

## 54. 为 if、for 或 while 语句体使用大括号

即使语句体只包含一条语句，也要为 `if`、`for` 和 `while` 语句使用大括号。大括号提高了代码的统一性和可读性。

更重要的是，在只包含单个语句的主体内插入额外语句时，很容易忘记添加大括号，因为传统的程序缩进为结构提供了强（但具有误导性的）指导。

## 不合规代码示例

此不合规代码示例使用缺少大括号的 `if` 语句验证用户。

```
int login;
if (invalid_login())
    login = 0;
else
    login = 1;
```

### 54. 对于 if、for 或 while 语句的主体使用大括号

此程序的运行符合预期。然而，维护人员随后可能会添加调试语句或其他逻辑，但忘记了添加左和右大括号：

```java
int login;

if (invalid_login())
  login = 0;
else
  // 在下方添加了调试行
  System.out.println("Login is valid\n");
  // 下行代码始终会被执行
  login = 1;
```

代码的缩进隐藏了程序的功能，可能导致安全漏洞。

### 合规解决方案

此合规解决方案即使在 `if` 语句的 `if` 和 `else` 部分只有单条语句的情况下，也使用了左、右大括号：

```java
int login;

if (invalid_login())
  login = 0;
} else {
  login = 1;
}
```

## 不合规代码示例

此不合规示例将一个 `if` 语句嵌套在另一个语句中，且没有在 `if` 和 `else` 主体周围使用大括号：

```java
int privileges;

if (invalid_login())
  if (allow_guests())
    privileges = GUEST;
else
  privileges = ADMINISTRATOR;
```

缩进可能会让程序员认为只有在登录有效时，才会授予用户管理员权限。然而，`else` 语句实际上绑定到了内部的 `if` 语句上：

```java
int privileges;
if (invalid_login())
  if (allow_guests())
    privileges = GUEST;
  else
    privileges = ADMINISTRATOR;
```

因此，此缺陷允许未经授权的用户获得管理员权限。

### 合规解决方案

此合规解决方案使用大括号消除了歧义，从而确保了权限被正确分配：

```java
int privileges;
if (invalid_login()) {
  if (allow_guests()) {
    privileges = GUEST;
  } else {
    privileges = ADMINISTRATOR;
  }
}
```

### 适用性

未闭合 `if`、`for` 或 `while` 语句的主体会导致代码容易出错并增加维护成本。

### 参考文献

[GNU 2013] §5.3, "C Construct的规范用法"

## 55. 不要紧跟在 if、for 或 while 条件之后放置分号

不要在 `if`、`for` 或 `while` 条件之后使用分号，因为这通常表示程序员的错误，并可能导致意料之外的行为。

## 56. 使用 break 语句结束与 case 标签关联的所有语句组

## 不合规代码示例

在此不合规代码示例中，分号被紧跟在 `if` 条件之后。

```java
if (a == b); {
/* ... */
}
```

无论条件表达式的结果如何，`if` 语句表观主体中的语句始终会被执行（求值）。

### 合规解决方案

此合规解决方案消除了分号，确保只有在条件表达式为真时才执行 `if` 语句的主体：

```java
if (a == b) {
/* ... */
}
```

### 适用性

在 `if`、`for` 或 `while` 条件之后立即放置分号可能会导致意料之外的行为。

### 参考文献

[Hatton 1995] §2.7.2, "遗漏与添加错误"

## 56. 使用 break 语句结束与 case 标签关联的所有语句组

`switch` 块包含多个 `case` 标签和一个可选但强烈推荐的 `default` 标签。每个 `case` 标签后的语句必须以 `break` 语句结束，负责将控制转移到 `switch` 块的末尾。如果省略，后续 `case` 标签中的语句将被执行。由于 `break` 语句是可选的，省略它不会产生编译器警告。当这种行为并非本意时，它会导致不可的的控制流。

## 不合规代码示例

在此不合规代码示例中，`card` 为 11 的情况缺少 `break` 语句。结果是执行继续处理 `card = 12` 的语句。

## 第 4 章 程序理解

```java
int card = 11;

switch (card) {
/* ... */
case 11:
    System.out.println("Jack");
case 12:
    System.out.println("Queen");
case 13:
    System.out.println("King");
default:
    System.out.println("Invalid Card");
}
```

### 合规解决方案

此合规解决方案使用大括号消除了歧义，从而确保了权限被正确分配：

```java
int card = 11;

switch (card) {
/* ... */
case 11:
    System.out.println("Jack");
    break;
case 12:
    System.out.println("Queen");
    break;
case 13:
    System.out.println("King");
    break;
default:
    System.out.println("Invalid Card");
}
```

### 适用性

未闭合 `if`、`for` 或 `while` 语句的主体会导致代码容易出错并增加维护成本。

## 57. 避免计数器的无意绕回

除非编码得当，否则 循环可能会无限执行，直到计数器绕回并达到其值。此问题可能源于对限制的盲目测试；例如，当计数器小于预期值时无限执行的循环：

```java
int counter = 0;
while (counter < Integer.MAX_VALUE) {
    // ...
    counter++;
}
```

## 不合规代码示例

此不合规代码示例似乎循环了五次。

```java
for (i = 1; i != 10; i += 2) {
  // ...
}
```

然而，循环永远不会终止。`i` 的连续值为 1, 3, 5, 7, 9, 11，以此此类推；与 10 的比较永远不会为真。值达到了最大正整数（`Integer.MAX_VALUE`），然后绕回到第二最小负整数（`Integer.MIN_VALUE + 1`）。它一直运行到 -1，然后 1，按所述方式进行。

## 不合规代码示例

此不合规代码示例会终止，但迭代次数远超预期：

```java
for (i = 1; i != 10; i += 5) {
  // ...
}
```

`i` 的连续值为 1, 6 和 11，跳过了 10。`i` 的值随后从接近最大正值绕回到最低负值，并向上增加到 0。然后它变为 2、7 和 12，再次跳过 10。在值从高正侧绕到低负侧另外三次后，它终于到达 0、5 和 10，终止了循环。

### 合规解决方案

一种解决方案是确保计数器在无意绕回之前达到循环终止条件。

```java
for (i = 1; i == 11; i += 2) {
  // ...
}
```

## 57. 避免循环计数器溢出 185

当影响迭代的一个或多个条件需要发生更改时，此解决方案可能是脆弱的。更好的解决方案是使用数值比较运算符（即 `<`, `<=`, `>`, `>=`）来终止循环。

```
for (i = 1; i <= 10; i += 2) {
  // ...
}
```

在迭代条件发生变化时，这种后来的解决方案可能更具健壮性。然而，这种方法绝不应替代对预期和实际迭代次数的审慎考虑。

## 不合规代码示例

测试计数器是否小于或等于 `Integer.MAX_VALUE` 或大于或等于 `Integer.MIN_VALUE` 的循环表达式永远不会终止，因为该表达式始终评估为 `true`。例如，以下循环将永远不会，因为 `i` 永远无法大于 `Integer.MAX_VALUE`：

```
for (i = 1; i <= Integer.MAX_VALUE; i++) {
  // ...
}
```

### 合规解决方案

此合规解决方案中的循环在 `i` 等于 `Integer.MAX_VALUE` 时终止：

```
for (i = 1; i < Integer.MAX_VALUE; i++) {
  // ...
}
```

如果循环旨在遍历 `i` 大于 0 的每一个值（包括 `Integer.MAX_VALUE`），则可以如下所示实现：

```
i = 0;
do {
  i++
  // ...
} while (i != Integer.MAX_VALUE);
```

## 不合规代码示例

此不合规代码示例将循环计数器初始化为 0，然后在每次迭代中增加 2，基本上是枚举了所有的正偶数值。

预期循环在 `i` 大于 `Integer.MAX_VALUE - 1`（一个偶数）时终止。在这种情况下，循环未能终止，因为计数器在达到 `Integer.MAX_VALUE - 1` 之前发生了回绕。

```
for (i = 0; i <= Integer.MAX_VALUE - 1; i += 2) {
  // ...
}
```

### 合规解决方案

此合规解决方案中的循环在计数器 `i` 大于 `Integer.MAX_VALUE` 减去步长时终止，并将其作为循环终止条件。

```
for (i = 0; i <= Integer.MAX_VALUE - 2; i += 2) {
  // ...
}
```

### 适用性

循环错误终止可能导致无限循环、性能低下的、结果错误和其他问题。如果用于终止循环的任何条件可以被攻击者影响，则这些错误可以被利用来导致拒绝服务或其他攻击。

### 参考文献

+ [JLS 2013] §15.20.1, "数值比较运算符 <, <=, >, 和 ="
- [Long 2012] NUM00-J. 检测或防止整数溢出

## 58. 使用括号确定操作优先级

程序员经常在运算符优先级上犯错，因为 `&`、`^`、`<<` 和 `>>` 的低优先级级别并不直观。通过恰当使用括号来避免优先级相关的错误，这也可以提高代码的可读性。按子类顺序的操作优先级列在 Java™ 教程 [Tutorials 2013] 中。

虽然取决于是否使用括号来指定评估顺序，但 Java CERT® Oracle® 安全编码标准 [Long 2012]，“EXP05-J. 不要在一个表达式中对同一个变量写入多次”仅适用于包含侧效应的表达式。

## 58. 使用括号确定操作优先级

## 不合规代码示例

此不合规代码示例中表达式的意图是将变量 `OFFSET` 加到 `x` 与 `MASK` 之间的位与运算结果上。

```
public static final int MASK = 1337;
public static final int OFFSET = -1337;

public static int computeCode(int x) {
  return x & MASK + OFFSET;
}
```

根据运算符优先级指南，该表达式解析为：

x & (MASK + OFFSET)

该表达式的评估方式如下，结果值为 0：

x & (1337 - 1337)

### 合规解决方案

此合规解决方案使用括号来确保表达式按预期进行评估：

```
public static final int MASK = 1337;
public static final int OFFSET = -1337;

public static int computeCode(int x) {
  return (x & MASK) + OFFSET;
}
```

## 不合规代码示例

在此不合规代码示例中，意图是在字符串 "value=" 之后附加 "0" 或 "1"。

```java
public class PrintValue {
  public static void main(String[] args) {
    String s = null;
    // 打印 "1"
    System.out.println("value=" + s == null ? 0 : 1);
  }
}
```

然而，优先级规则导致打印的表达式解析为 ("value=" + s) == null ? 0 : 1。

### 合规解决方案
