
```csharp
string str3 = "ONE";
string str4 = "two";
string str5 = "one, too";

if(String.Compare(str1, str2) == 0)
    Console.WriteLine(str1 + " and " + str2 +
        " are equal.");
else
    Console.WriteLine(str1 + " and " + str2 +
        " are not equal.");

if(String.Compare(str1, str3) == 0)
    Console.WriteLine(str1 + " and " + str3 +
        " are equal.");
else
    Console.WriteLine(str1 + " and " + str3 +
        " are not equal.");

if(String.Compare(str1, str3, true) == 0)
    Console.WriteLine(str1 + " and " + str3 +
        " are equal ignoring case.");
else
    Console.WriteLine(str1 + " and " + str3 +
        " are not equal ignoring case.");

if(String.Compare(str1, str5) == 0)
    Console.WriteLine(str1 + " and " + str5 +
        " are equal.");
else
    Console.WriteLine(str1 + " and " + str5 +
        " are not equal.");

if(String.Compare(str1, 0, str5, 0, 3) == 0)
    Console.WriteLine("First part of " + str1 + " and " +
        str5 + " are equal.");
else
    Console.WriteLine("First part of " + str1 + " and " +
        str5 + " are not equal.");

int result = String.Compare(str1, str4);
if(result < 0)
    Console.WriteLine(str1 + " is less than " + str4);
else if(result > 0)
    Console.WriteLine(str1 + " is greater than " + str4);
else
    Console.WriteLine(str1 + " equals " + str4);
}
```

输出如下所示：

```
one and one are equal.
one and ONE are not equal.
one and ONE are equal ignoring case.
one and one, too are not equal.
First part of one and one, too are equal.
one is less than two
```

## 使用 StringComparison 枚举

在表 22-1 中，注意到两个接受 StringComparison 类型参数的 Compare() 方法。这些版本如下所示：

```
public static int Compare(string str1, string str2, StringComparison how)

public static int Compare(string str1, int start1, string str2, int start2,
    int count, StringComparison how)
```

每个版本中，how 参数指定 str1 与 str2 的比较方式。StringComparison 是一个枚举，定义了表 22-2 中显示的值。使用这些值，可以创建满足应用程序特定需求的比较。因此，添加 StringComparison 参数扩展了 Compare() 的功能。

StringComparison 形式的 Compare() 的一个特别好的用途是比较字符串与不变的文件名或密码。例如，想象一种情况，用户必须输入密码 we-23&blx5。无论使用何种文化设置，该密码都相同。因此，您希望比较用户输入的字符串与密码，而不受文化差异的影响。一种方法是

| 值 | 描述 |
|---|---|
| CurrentCulture | 使用当前活动的文化设置执行比较。 |
| CurrentCultureIgnoreCase | 使用当前活动的文化设置执行不区分大小写的比较。 |
| InvariantCulture | 使用不变的（即通用且不变的）文化执行比较。 |
| InvariantCultureIgnoreCase | 使用不变的（即通用且不变的）文化执行不区分大小写的比较。 |
| Ordinal | 使用字符串中字符的序数值执行比较。因此，可能不会得到字典顺序，并且忽略文化约定。 |
| OrdinalIgnoreCase | 使用字符串中字符的序数值执行不区分大小写的比较。因此，可能不会得到字典顺序，并且忽略文化约定。 |

指定 how 参数为 StringComparison.InvariantCulture，在这种情况下所有文化差异都将被避免。这种方法由以下程序演示：

// Compare strings using StringComparison enumeration.
using System;

class StrCmpDemo {
    static void Main() {
        // Note: Never embed a password in real code.
        // This is for demonstration purposes only.
        string pwd = "we-23b1x5";
        string str;

        Console.WriteLine("Enter password: ");
        str = Console.ReadLine();

        // Compare using invariant culture.
        if (String.Compare(pwd, str, StringComparison.InvariantCulture) == 0)
            Console.WriteLine("Password accepted.");
        else
            Console.WriteLine("Password invalid.");
    }
}
```

## 连接字符串

有两种方法可以将两个或多个字符串连接（合并）在一起。首先，您可以使用 + 运算符，如第 7 章所示。其次，您可以使用 String 定义的各种连接方法之一。虽然在许多情况下使用 + 是最简单的方法，但连接方法为您提供了另一种选择。

执行连接的方法称为 Concat()。其中最常用的形式如下所示：

```
public static string Concat(string str1, string str2)
```

该方法返回一个字符串，其中包含连接到 str1 末尾的 str2。另一种形式 Concat()，如下所示，连接三个字符串：

```
public static string Concat(string str1, string str2, string str3)
```

在此版本中，返回一个包含 str1、str2 和 str3 连接的字符串。还有一种形式可以连接四个字符串：

```
public static string Concat(string str1, string str2, string str3, string str4)
```

此版本返回所有四个字符串的连接。接下来显示的 Concat() 版本连接任意数量的字符串：

```
public static string Concat(params string[] strs)
```

为什么存在这些形式。原因是效率；传递最多四个参数比使用可变长度参数列表更高效。

以下程序演示了 Concat() 的可变长度参数版本：

// Demonstrate Concat().

using System;

class ConcatDemo {
    static void Main() {
        string result = String.Concat("This ", "is ", "a ",
            "test ", "of ", "the ",
            "String ", "class.");
        Console.WriteLine("result: " + result);
    }
}
```

输出如下所示：

```
result: This is a test of the String class.
```

还有一些 Concat() 方法的版本接受对象引用，而不是字符串引用。这些方法获取调用它们的对象字符串表示形式，并返回包含这些字符串连接的字符串。（字符串表示形式是通过对对象调用 ToString() 获得的。）这些 Concat() 版本如下所示：

```
public static string Concat(object v1)
public static string Concat(object v1, object v2)
public static string Concat(object v1, object v2, object v3)
public static string Concat(object v1, object v2, object v3, object v4)
public static string Concat(params object[] v)
```

第一个方法仅返回 v1 的字符串等价形式。其他方法返回一个包含其参数连接的字符串。Concat() 的对象形式非常方便，因为它们让您无需在连接之前手动获取字符串表示形式。要了解这些方法有多有用，请考虑以下程序：

// Demonstrate the object form of Concat().

using System;

class MyClass {
    public static int Count = 0;
    public MyClass() { Count++; }
}

class ConcatDemo {
    static void Main() {
```

```
string result = String.Concat("The value is " + 19);
Console.WriteLine("result: " + result);

result = String.Concat("hello ", 88, " ", 20.0, " ",
false, ", ", 23.45M);
Console.WriteLine("result: " + result);

MyClass mc = new MyClass();

result = String.Concat(mc, " current count is ",
MyClass.Count);
Console.WriteLine("result: " + result);
}
```

输出如下所示：

```
result: The value is 19
result: hello 88 20 False 23.45
result: MyClass current count is 1
```

在此示例中，Concat() 连接各种类型数据的字符串表示形式。对于每个参数，都会调用与其关联的 ToString() 方法以获取字符串表示形式。因此，在此对 Concat() 的调用中

```
string result = String.Concat("The value is " + 19);
```

调用 Int32.ToString() 以获取整数值 19 的字符串表示形式。
然后 Concat() 连接字符串并返回结果。

还请注意，用户定义类 MyClass 的对象如何在此对 Concat() 的调用中使用：

```
result = String.Concat(mc, " current count is ",
MyClass.Count);
```

在这种情况下，返回 mc 的字符串表示形式，其类型为 MyClass。默认情况下，这只是其类名。但是，如果您重写 ToString() 方法，则 MyClass 可以返回不同的字符串。例如，尝试在前面的程序中向 MyClass 添加此版本的 ToString()：

```
public override string ToString() {
return "An object of type MyClass";
}
```

当使用此版本时，输出中的最后一行将为

```
result: An object of type MyClass current count is 1
```

## 搜索字符串

String 提供了许多允许搜索字符串的方法。例如，您可以搜索子字符串或字符。您还可以搜索任一的首次或最后出现位置。
