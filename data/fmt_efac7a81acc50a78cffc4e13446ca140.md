
```
            }

    }

    Console.WriteLine("After loop");

}

Console.WriteLine("At end of method");
```

## 示例 115 常用表达式：赋值与方法调用
赋值语句 `x=` 是后跟分号的赋值 `x=`。方法调用语句 `M(...);` 是方法表达式 `M(...)`。方法返回的值（如果有）会被丢弃；方法仅为了其副作用而执行。

## 示例 116 变量声明
变量和常量声明语句可以出现在块语句内部任何地方。初始化表达式可以使用已声明的（已初始）变量，可能在同一语句中。

```c
int a;

const int year = 365, week = 7, weekMax = year / week + 1;

int x, y = year, z = 3, ratio = z/y;

const double pi = 3.141592653589;

bool found = false;

var stillLooking = true;
```

# 13.5 选择语句

### 13.5.1 if 语句
if 语句的形式为

```c
if (condition)
    truebranch
```

条件必须是 `bool` 类型，且 `truebranch` 是一个语句，但不是声明语句或标记语句。如果条件求值为真，则执行 `truebranch`；否则不执行。

### 13.5.2 if-else 语句
if-else 语句的形式为

```c
if (condition)
    truebranch
else
    falsebranch
```

条件必须是 `bool` 类型，且 `truebranch` 和 `falsebranch` 都是语句但不是声明语句或标记语句。如果条件求值为真，则执行 `truebranch`；否则执行 `falsebranch`。

### 13.5.3 switch 语句
switch 语句的形式为

```c
switch (expression) {
    case constant: branch1;
    case constant: branch2;
    ...
    default: branch;
}
```

表达式必须是 `byte`、`short`、`ushort`、`int`、`uint`、`long`、`char`、`String`、枚举类型，或者恰好具有一个到这些类型之一的隐式转换的用户定义类型（枚举类型除外）。这被称为 switch 语句的控制类型。每个常量必须是编译时常量。两个常量不能具有相同的值。每个常量的类型必须可以转换为表达式的类型。每个分支之前都有一个或多个 `case` 子句，这些子句可以用 `return`（在方法或构造函数中）或 `continue`（在循环中）或 `goto` 或任何其他确保分支结束永远无法到达的语句组合终止。这由编译器进行检查。`default` 子句可以省略。它可以出现在其他子句中，放在第一个或最后一个都是最明智的选择。switch 语句的执行情况如下：表达式求值为值 `v`。如果执行相应的分支。如果 `v` 不等于任何常量，则执行 `default`；如果没有 `default` 子句，则什么都不执行。一个分支中可以包含 `goto` 语句（见章节 13.7）。

### 示例 117 块语句
所有方法和构造函数体都是块语句。在示例 6 的 `Sum` 方法中，第二个 `if` 语句的 `truebranch` 是一个块语句。示例 12 中的方法 `M` 包含两个块语句，每个语句都包含一个局部于该块语句的变量 `x` 的声明。

### 示例 118 单 if-else 语句
该方法的行为与示例 7 中的 `Absolute`。

```c
static double Absolute(double x) {
  if (x >= 0)
    return x;
  else
    return -x;
}
```

## 示例 119 if-else 语句序列
if-else 语句序列用于查找值所属的区间。

```c
static String AgeGroup(int age) {
  if (age <= 12) return "child";
  else if (age <= 19) return "teenager";
  else if (age <= 45) return "young";
  else if (age <= 60) return "middle-age";
  else
    return "old";
}
```

### 示例 120 switch 语句
方法 `FindCountry` 根据给定的数字缀查找对应的分支。可以使用 if-else 语句序列来实现，但 `switch` 更快且清晰。注意 `default` 情况不需要是最后一个。

```c
static String FindCountry(int prefix) {
  default: return "Unknown";
  case 1: return "North America";
  case 44: return "Great Britain";
  case 45: return "Denmark";
  case 299: return "Greenland";
  case 46: return "Sweden";
  case 7: return "Russia";
}
```

# 13.6 循环语句

### 13.6.1 for 语句
形式如下

```c
for (initialization; condition; step)
body
```

其中 `initialization` 是局部变量声明（见 13.4）或可能是空的逗号分隔的方法调用表达式、赋值表达式、对象创建、递增表达式和递减表达式；`condition` 是 `bool` 类型的表达式；`step` 是与 `initialization` 允许的相同的逗号分隔列表；`body` 是一个语句但不是声明语句或标记语句。逗号分隔的列表在求值时从左到右计算。初始化、条件和步骤可以为空。空条件等价于 `true`。因此 `for(;;) body` 意味着“永远执行 body”。

1. 执行初始化。
2. 计算条件。如果为假，循环终止。
3. 如果为真，则：
   (a) 执行 body；
   (b) 执行步骤；
   (c) 继续回到2。

### 13.6.2 foreach 语句
形式为

```c
foreach (type x in expression)
body
```

表达式必须是可枚举的，其枚举器产生的元素可以显式转换为 `type`。`body` 必须是一个语句但不是声明语句或标记语句。如果使用关键字代替 `type`，则编译器将从可枚举表达式的元素类型（见 6.3）推断 `x` 的类型。

首先计算表达式以获取枚举器。然后对枚举器产生的每个元素执行 `body`，并将变量 `x` 绑定到转换元素到类型的结果（可能通过拆箱转换）。如果元素无法转换为 `type`，则抛出 `InvalidCastException`。局部变量 `x` 的作用域是 `body`，且 `body` 是只读的；不能对其赋值或作为引用或输出参数传递。`body` 不应修改枚举器或枚举器下的任何数据。类型 `t` 的表达式在以下情况下是枚举的：

* 特别是类类以及所有数组类型（见 9）实现了 `IEnumerable`，并且当 `T[]` 可隐式转换为 `U[]` 时，数组类型 `T` 实现了 `IList<U>` 和 `IEnumerable<U>`。
* 它实现了一个公共实例方法 `GetEnumerator()`，其返回类型实现了接口 `IEnumerator`（见 27.2）所要求的一个返回 `bool` 的公共实例方法 `Next()` 和一个公共实例属性 `Current`。参见示例 64 和 68。

# 示例 121 使用嵌套 for 打印星号三角形

```csharp
for (int i=1; i<=4; i++) {      // 输出:
    for (int j=1; j<=i; j++) {           // *
        Console.Write("*");                // **
        Console.WriteLine();               // ***
    }                               // ****
```

### 示例 122 循环中的多变量初始化和步进

此方法用于反转一维数组的元素。请注意初始化部分中的多个变量声明，以及循环头步进部分的多个（逗号分隔的）表达式。

```csharp
public static void Reverse(Object[] arr) {
    for (int s=0, t=arr.Length-1; s<t; s++, t--) {
        Object temp = arr[s]; arr[s] = arr[t]; arr[t] = temp;
    }
}
```

# 示例 123 在数组上使用 foreach

此循环拼接数组 arr 中的字符串，并为每个字符串插入两个副本。在 `foreach` 循环中将元素绑定到局部变量 s 涉及到 `String` 类型的隐式转换，因此无论 arr 的类型是 `String[]` 还是 `Object`，示例都可以编译并执行。

```csharp
StringBuilder sb = new StringBuilder();
foreach (String s in arr) {
    sb.Append(s).Append(s);
}
```

### 示例 124 显式使用 IEnumerator 代替 foreach

示例123 中的 `foreach` 循环是使用枚举器的 `while` 循环的语法糖。注意到 `String` 的显式转换；在 `foreach` 语句中它是不可见的但仍然执行了。如果循环体通过 `return` 语句意外终止，`finally` 块将调用枚举器的 `Dispose` 方法（如果存在），这样枚举器就可以立即释放它持有的任何资源。`IDisposable` 接口在第13.10节节描述。

```csharp
StringBuilder sb = new StringBuilder();
IEnumerator enm = arr.GetEnumerator();
try {
    while (enm.MoveNext()) {
        String s = (String)enm.Current;
        sb.Append(s).Append(s);
    }
} finally {
    Console.WriteLine("now in finally block");
    IDisposable disp = enm as System.IDisposable;
    if (disp != null)
        disp.Dispose();
}
```

### 13.6.3 while 语句

`while` 语句的格式如下：

```csharp
while (condition)
  body
```

其中 *condition* 是 `bool` 类型的表达式，而 *body* 是一个语句但不是声明语句或标记语句。`while` 语句的执行过程如下：

- 1. 求值 *condition*。如果为假，则循环终止。
- 2. 如果为真，则：
  (a) 执行 *body*；
  (b) 继续执行第1步。

无限循环可以写为 *while (true) body*，这可能比13.6.1节中所示的“永远”惯用写法 `(;;) *body` 更清晰。

### 13.6.4 do–while 语句

`do–while` 语句的格式如下：

```csharp
do
  while (condition);
```

其中 *condition* 是 `bool` 类型的表达式，而 *body* 是一个语句但不是声明语句或标记语句。`do-while` 语句的执行过程如下：

- 1. 执行 *body*。
- 2. 求值 *condition*。如果为假，则循环终止。
- 3. 如果为真，继续执行第1步。

*body* 至少执行一次，因为 *condition* 是在执行 *body* 之后才进行测试的。这意味着 *condition* 并无法建立保证 *body* 成功执行的前置条件。通常使用 `while` 循环或 `for` 循环更安全且更合适，因为它们在执行 *body* 之前会测试 *condition*。

## 示例 125 使用 while 循环搜索数组

此方法通过搜索星期名称数组，将星期几（例如周四）转换为数字（例如4）。请注意，在 `while` 循环之后，循环条件的取反将成立。因此，如果循环后 `i < wdays.Length`，则必须满足 `wday == wdays[i]`。

```csharp
static int WeekDayNo(String wday) {
    int i=0;
    while (i < wdays.Length && wday != wdays[i]) {
        // if i >= wdays.Length or wday == wdays[i]
        if (i < wdays.Length) return i++;
        else return -1;
    }
    static readonly String[] wdays = {
    "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday" };
}
```

### 示例 126 搜索子字符串

如果 `q` 作为子字符串出现在 `t` 中，调用 `Substring(q,t)` 返回 `true`。外层循环考虑 `t` 中所有可能出现 `q` 的点，内层循环将这些点的字符与 `q` 进行比较。

```csharp
static bool Substring(String query, String target) {
    for (int j=0, n=target.Length-query.Length; j<=n; j++) {
        int k=0, m=query.Length;
        while (k<m && target[j+k] == query[k]) {
            // Now if k==m (and target[j..j+m-1] == query[0..m-1])
            k++;
        }
    }
    return false;
}
```

## 示例 127 因为分号位置错误导致的无限循环

位置错误的分号（;)导致循环无限运行。

```csharp
int i=0;
while (i++)
i++;
```

### 示例 128 使用 do-while

此处使用了 `do-while` 语句：

```csharp
int sum = 0;
do {
    sum++;
} while (sum < 5);
```

# 13.7 返回、退出和跳转

### 13.7.1 return 语句

最形式的 `return` 语句（不带参数）是：

```csharp
return;
```

`return` 语句将控制权返回给调用者。如果方法有返回值，`return` 语句必须返回该类型的值。如果方法是 `void`，则 `return` 语句不能有任何参数。

```csharp
public void Print(String s) {
    Console.WriteLine(s);
    return;
}
```

`return` 语句将控制权返回给调用者。如果方法有返回值，`return` 语句必须返回该类型的值。如果方法是 `void`，则 `return` 语句不能有任何参数。

```csharp
public int Add(int a, int b) {
    return a + b;
}
```

或者，可以使用 `return` 语句提前退出方法：

```csharp
public void Print(String s) {
    if (s == null)
        return; // 提前退出方法
    Console.WriteLine("String is " + s);
}
```

### 13.7.2 break 语句

`break` 语句只能在 `switch` 或循环内部使用；其格式为：

```csharp
break;
```

`break` 语句终止最内层循环，并在循环之后继续执行。

```csharp
for (int i=0; i<10; i++) {
    if (i == 5)
        break;
}
```

### 13.7.3 continue 语句

`continue` 语句只能在循环内部使用；其格式为：

```csharp
continue;
```

`continue` 语句终止循环的当前迭代，并在循环的下一次迭代中继续执行。

```csharp
for (int i=0; i<10; i++) {
    if (i == 5)
        continue;
    Console.WriteLine(i);
}
```

### 13.7.4 标签语句 (The Labeled Statement)

标签语句将标签声明为语句；其形式如下：

```
label : statement
```
