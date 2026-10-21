

该语句将数字 123 转换为字符串 ‘123’，然后将字符串值赋给字符串变量 numStr。

## 10.2.6 原始字符串

字符串也可以使用所谓的 verbatim 字符串来创建。Verbatim 字符串是以 @ 符号开头的字符串。该符号告诉编译器字符串应按原样使用，即使它包含转义字符。

```
string s1 = @ "\EBG\Csharp\string.cs";
```

为了在不使用 @ 符号的情况下获得相同的输出，输入字符串应写成如下形式：

```
string s1 = "\\EBG\\Csharp\\string.cs";
```

我们也可以在 @ 引用的字符串中使用转义字符如 n 和 t。它们在输出时不会被处理，并在文本中按原样出现。

请注意，如果普通字符串包含嵌入的 n，则在对字符串进行输出处理时，n 之后的字符串将显示在下一行。

## 10.3 字符串方法

字符串对象是不可变的，这意味着我们不能修改其中包含的字符。然而，由于字符串是通用语言运行时（CLR）中预定义的 System.String 类的别名，因此有许多内置操作可用于处理字符串。所有操作都会产生字符串的修改版本，而不是修改调用该方法所依据的字符串。

表 10.1 列出了可用于各种操作的各种方法，例如比较、追加、插入、转换、复制、索引、连接、拆分、填充、修剪、删除、替换和搜索。我们在上一节中已经使用了一些方法，如 Concat 和 Copy。

### 表 10.1 字符串类方法

| METHOD | OPERATION |
|---|---|
| Compare () | Compares two strings |
| CompareTo () | Compares the current instance with another instance |
| ConCat () | Concatenates two or more strings |
| Copy() | Creates a new string by copying another |
| CopyTo () | Copies a specified number of characters to an array of Unicode characters |
| EndsWith () | Determines whether a substring exists at the end of the string |
| Equals() | Determines if two strings are equal |
| IndexOf () | Returns the position of the first occurrence of a substring |
| Insert () | Returns a new string with a substring inserted at a specified location |
| Join () | Joins an array of strings together |
| LastIndexOf () | Returns the position of the last occurrence of a substring |
| PadLeft () | Left-aligns the strings in a field |
| PadRight () | Right-aligns the string in a field |
| Remove () | Deletes characters from the string |
| Replace () | Replaces all instances of a character with a new character |
| Split () | Creates an array of strings by splitting the string at any occurrence of one |
| StartsWith () | Determines whether a substring exists at the beginning of the string |
| Substring () | Extracts a substring |
| ToLower () | Returns a lower-case version of the string |
| ToUpper () | Returns an upper-case version of the string |
| Trim () | Removes white space from the string |
| TrimEnd () | Removes a string of characters from the end of the string |
| TrimStart () | Removes a string of characters from the beginning of the string |

## 10.4 插入字符串

字符串方法使用我们想要操作的字符串对象调用。程序 10.1 说明了 System.String 类支持的 Insert () 方法和索引器属性的使用。

### 程序 10.1 使用 INSERT () 方法

```
using System;
class StringMethod
{
    public static void Main()
    {
        string s1 = "Lean";
        string s2 = s1.Insert(3,"r");      // s2 = Learn
        string s3 = s2.Insert(5,"er");     // s3 = Learner
        for (int i = 0; i < s3.Length; i++)
            Console.Write(s3[i]);
        Console.WriteLine();
    }
}
```

当语句
    string s2 = s1.Insert(3, "r");
执行时，字符串变量 s2 包含字符串 "Learn"。字符串 "r" 在 s1 的 3 个字符后插入。同样，字符串 "er" 在字符串末尾插入。最后，变量 s3 包含值 "Learner"。

请注意，我们并没有修改给定字符串变量的内容。相反，我们将修改后的值赋给新的字符串变量。例如：
    s1 = s1.Insert(3, "r");
是非法的。我们试图修改不可变的字符串对象 s1。

程序 10.2 从用户处作为字符串接收两个输入，并将 string2 的输入复制到 string5 并检查 string3 是否以 'IDE' 结尾。程序在 string3 以 'IDE' 结尾时显示 true。搜索字符串1 中的字符 'a'。在位置 6 插入 'hello' 到 string6 并显示 string6。

### 程序 10.2
复制、搜索和插入字符串

```
using System;
using System.Collections.Generic;
using System.Text;
namespace SearchString
{
    class Program
    {
        public void Display()
        {
            string str1 = "";
            Console.Write("Enter a string : ");
            str1 = Console.ReadLine();
            string str2 = "";
            Console.Write("Enter another string string : ");
            str2 = Console.ReadLine();
            string str3 = "C# 2005 is developed in Visual Studio 2005 IDE";
            Console.WriteLine("String str3 is : {0}", str3);
            // the string copy method
            string str5 = string.Copy(str2);
            Console.WriteLine("String str5 is copied from str2: {0}", str5);
            Console.WriteLine("\nString str5 is {0} characters long. ", str5.Length);
            Console.WriteLine("The 10th character of string str3 is : {0}", str3[9]);
            // check if a string ends with a set of characters
            Console.WriteLine("String str3:{0}\nEnds with IDE?: {1}\n", str3, str3.EndsWith("IDE"));
            Console.WriteLine("Ends with Studio?: {0}", str3.EndsWith("Studio"));
            // return the index of the substring
            Console.WriteLine("\nThe first time character 'a' occured in string str1 at position : {0}", str1.IndexOf("a")+1);
            string str6 = str2.Insert(6, "hello");
            Console.WriteLine("'hello' is inserted in string str6. String s6 is now : {0}\n", str6);
        }
        static void Main(string[] args)
        {
            Program prg = new Program();
            prg.Display();
        }
    }
}
```

## 10.5 比较字符串

字符串类支持重载的方法和运算符来比较两个字符串是否相等。它们是：

- 重载 Compare() 方法
- 重载 Equals() 方法
- 重载 == 运算符

### 10.5.1 Compare() 方法

重载的静态 Compare 方法有两个版本。第一个接受两个字符串作为参数并比较它们。示例：
int n = string.Compare(s1,s2);

这会执行区分大小写的比较，并根据不同条件返回不同的整数值，如下所示：

- 零整数，如果 s1 等于 s2
- 正整数（1），如果 s1 大于 s2
- 负整数（-1），如果 s1 小于 s2

例如，如果 s1 = "abc" 且 s2 = "ABC"，则 n 将被赋值为 -1。记住，小写字母的 ASCII 值小于大写字母。

我们可以在 if 语句中使用此类比较语句，如：
if ( string.Compare(s1, s2) == 0 )
( Console.WriteLine("They are equal");

Compare 的第二个版本接受一个额外的 bool 类型参数来决定是否忽略大小写。如果 bool 参数为 true，则忽略大小写。示例：
int n = string.Compare(s1, s2, true);

该语句比较字符串 s1 和 s2 忽略大小写，因此当 s1 = "abc" 且 s2 = "ABC" 时返回零，意味着它们相等。

### 10.5.2 Equals( ) 方法

字符串类支持重载的 Equals 方法来测试字符串的相等性。Equals 方法也有两个版本。它们实现如下：

```
bool b1 = s2.Equals(s1);
bool b2 = string.Equals(s2, s1);
```

这些方法如果 s1 和 s2 相等则返回布尔值 true，否则返回 false。

### 10.5.3 == 运算符

测试字符串相等的一种简单自然的方法是使用重载的 == 运算符。

示例：

```
bool b3 = (s1 == s2); //b3 is true if they are equal
```

我们经常在决策语句中使用此类语句，如：

```
if (s1 == s2)
    Console.WriteLine("They are qual");
```

## 10.6 查找子字符串

可以使用 String 类中可用的重载 Substring 方法从给定字符串中提取子字符串。Substring 有两个版本：

- s.Substring(n)
- s.Substring(n1, n2)

第一个从 s 中包含的字符串的第 n 个位置提取子字符串，直到最后一个字符。第二个从 s 中从 n1 位置开始提取子字符串，结束于 n2 位置。示例：

```
string s1 = "NEW YORK";
string s2 = s1.Substring(5);
string s3 = s1.Substring(0,3);
string s4 = s1.Substring(5,8);
```

执行时，字符串变量将包含以下子字符串：

- s2: YORK
- s3: NEW
- s4: YORK

## 10.7 可变字符串

使用 StringBuilder 类可以创建可修改的可变字符串。示例：

```
StringBuilder str1 = new StringBuilder("abc");
StringBuilder str2 = new StringBuilder();
```

字符串对象 str1 以三个字符的初始大小创建，str2 创建为空字符串。它们可以在向其中添加更多字符时动态增长。它们可以无限制增长或增长到可配置的最大值。可变字符串也称为动态字符串。

StringBuilder 类支持许多用于操作动态字符串的方法。表 10.2 列出了一些最常用的方法。

