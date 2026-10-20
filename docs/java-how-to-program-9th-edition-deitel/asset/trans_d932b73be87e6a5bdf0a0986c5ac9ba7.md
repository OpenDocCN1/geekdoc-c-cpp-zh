

# 字符串、字符和正则表达式

> 亨利·金的致命缺陷
> 是咀嚼细小的线头。
> ——希莱尔·贝洛克

> 有力的写作是简洁的。句子不应包含不必要的词，段落不应包含不必要的句子。
> ——威廉·斯特伦克 Jr.

> 我把这封信写得比平常长，因为我没有时间把它写短。
> ——布莱兹·帕斯卡

## 目标

在本章中你将学习：

- 创建和操作类 String 的不可变字符字符串对象。
- 创建和操作类 StringBuilder 的可变字符字符串对象。
- 创建和操作类 Character 的对象。
- 使用 String 方法 split 将 String 对象分解为标记。
- 使用正则表达式验证输入到应用程序中的 String 数据。

![](img/009e962758dcc71dbc43a493362e6dc0_709_0.png)

- 16.1 引言
- 16.2 字符和字符串的基础
- 16.3 类 String
- 16.3.1 String 构造方法
- 16.3.2 String 方法 length、charAt 和 getChars
- 16.3.3 比较字符串
- 16.3.4 在字符串中定位字符和子字符串
- 16.3.5 从字符串中提取子字符串
- 16.3.6 连接字符串
- 16.3.7 其他 String 方法
- 16.3.8 String 方法 valueOf
- 16.4 类 StringBuilder
- 16.4.1 StringBuilder 构造方法
- 16.4.2 StringBuilder 方法 length、capacity、setLength 和 ensureCapacity
- 16.4.3 StringBuilder 方法 charAt、setCharAt、getChars 和 reverse
- 16.4.4 StringBuilder append 方法
- 16.4.5 StringBuilder 插入和删除方法
- 16.5 类 Character
- 16.6 分词字符串
- 16.7 正则表达式、类 Pattern 和类 Matcher
- 16.8 总结
- 摘要 | 自测练习 | 自测练习答案 | 练习 | 专题：高级字符串操作练习 | 专题：挑战性字符串操作项目 | 做出改变

## 16.1 引言

本章介绍 Java 的字符串和字符处理功能。这里讨论的技术适用于验证程序输入、向用户显示信息以及其他基于文本的操作。它们也适用于开发文本编辑器、文字处理器、页面布局软件、计算机排版系统和其他类型的文本处理软件。我们在前几章中已经介绍了一些字符串处理功能。本章详细讨论了 java.lang 包中的类 String、StringBuilder 和 Character 的功能。这些类为 Java 中的字符串和字符操作提供了基础。

本章还讨论了正则表达式，它们为应用程序提供了验证输入的功能。该功能位于 String 类中，以及位于 java.util.regex 包中的类 Matcher 和 Pattern 中。

## 16.2 字符和字符串的基础

字符是 Java 源程序的基本构建块。每个程序都由一系列字符组成——当这些字符有意义地组合在一起时——Java 编译器会将其解释为一系列用于完成任务的指令。程序可能包含字符字面量。字符字面量是用单引号表示的字符中的整数值。例如，'z' 表示 z 的整数值，'\n' 表示换行的整数值。字符字面量的值是 Unicode 字符集中的字符的整数值。附录 B 提供了 ASCII 字符集中的字符的整数等价物，ASCII 字符集是 Unicode 的子集（在附录 L 中讨论）。

请回顾第 2.2 节，字符串是一系列作为单个单元处理的字符。字符串可能包括字母、数字和各种特殊字符，例如 +、-、*、/ 和 $。

字符串是类 String 的对象。字符串字面量（存储在内存中作为 String 对象）写成双引号中的字符序列，例如：

| "John Q. Doe" | （一个姓名） |
| "9999 Main Street" | （一个街道地址） |
| "Waltham, Massachusetts" | （一个城市和州） |
| "(201) 555-1212" | （一个电话号码） |

字符串可以分配给 String 引用。声明

```
String color = "blue";
```

将 String 变量 color 初始化为引用包含字符串 "blue" 的 String 对象。

## 性能提示 16.1

> 为了节省内存，Java 将具有相同内容的所有字符串字面量视为单个 String 对象，该对象有许多引用指向它。

## 16.3 类 String

类 String 用于在 Java 中表示字符串。接下来的几个小节涵盖了类 String 的许多功能。

### 16.3.1 String 构造方法

类 String 提供了用于以多种方式初始化 String 对象的构造方法。Fig. 16.1 的 main 方法演示了其中四个构造方法。

第 12 行使用类 String 的无参数构造方法实例化一个新的 String 并将其引用分配给 s1。新的 String 对象不包含任何字符（即空

```
1 // Fig. 16.1: StringConstructors.java
2 // String class constructors.
3
4 public class StringConstructors
5 {
6 public static void main( String[] args )
7 {
8 char[] charArray = { 'b', 'i', 'r', 't', 'h', ' ', 'd', 'a', 'y' };
9 String s = new String( "hello" );
10
11 // use String constructors
12 String s1 = new String();
13 String s2 = new String( s );
14 String s3 = new String( charArray );
15 String s4 = new String( charArray, 6, 3 );
16
17 System.out.printf(
18 "s1 = %s\ns2 = %s\ns3 = %s\ns4 = %s\n",
19 s1, s2, s3, s4 ); // display strings
20 } // end main
21 } // end class StringConstructors
```

字符串，也可以用 "" 表示，其长度为 0。第 13 行使用类 String 的接受 String 对象作为参数的构造方法实例化一个新的 String 对象并将其引用分配给 s2。新的 String 对象包含与作为参数传递给构造方法的 String 对象 s 相同的字符序列。

> 软件工程观察 16.1
> 没有必要复制现有的 String 对象。String 对象是不可变的——它们的字符内容在创建后不能更改，因为类 String 不提供允许修改 String 对象内容的方法。

第 14 行使用类 String 的接受 char 数组作为参数的构造方法实例化一个新的 String 对象并将其引用分配给 s3。新的 String 对象包含数组中字符的副本。

第 15 行使用类 String 的接受 char 数组和两个整数作为参数的构造方法实例化一个新的 String 对象并将其引用分配给 s4。第二个参数指定从数组中访问字符的起始位置（偏移量）。请记住，第一个字符位于位置 0。第三个参数指定要在数组中访问的字符数（计数）。新的 String 对象由访问到的字符形成。如果作为参数指定的偏移量或计数导致访问字符数组之外的元素，则会抛出 StringIndexOutOfBoundsException。

> 常见编程错误 16.1
> 访问 String 之外的字符（即索引小于 0 或索引大于或等于 String 的长度）会导致 StringIndexOutOfBoundsException。

### 16.3.2 String 方法 length、charAt 和 getChars

String 方法 length、charAt 和 getChars 分别返回 String 的长度、获取 String 中特定位置的字符以及以 char 数组形式检索 String 中的一组字符。图 16.2 演示了每种方法。

```
1  // Fig. 16.2: StringMiscellaneous.java
2  // This application demonstrates the length, charAt and getChars
3  // methods of the String class.
4
5  public class StringMiscellaneous
6  {
```

Fig. 16.2 | String methods length, charAt and getChars. (Part 1 of 2.)

