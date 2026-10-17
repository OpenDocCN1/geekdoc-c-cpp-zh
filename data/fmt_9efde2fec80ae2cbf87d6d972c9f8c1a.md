
- radar

- deified

- kayak

- deified

- able I ere saw Elba

## 5.4 while 语句

注意，有些回文具有偶数个字符，而另一些具有奇数个字符。`PalindromeTester` 5.9 测试字符串是否为回文。用户可以测试许多字符串。`PalindromeTester` 的代码中包含了两个循环，外层循环控制测试多少字符串，内层循环

列表 5.9

************************************

// 展示了嵌套循环的使用。

// 作者：Lewis

************************************

```java
import java.util.Scanner;

public class PalindromeTester {

    //------------------------------------------------------

    // 测试字符串是否为回文。

    //------------------------------------------------------

    public static void main(String[] args) {

        Scanner scan = new Scanner(System.in);

        System.out.print("Test another (y/n)? ");

        var another = scan.nextLine();

        if (another.equalsIgnoreCase("y")) {

            System.out.print("Enter string: ");

            String str = scan.nextLine();

            int left = 0;

            int right = str.length() - 1;

            boolean isPalindrome = true;

            while (left < right) {

                if (str.charAt(left) != str.charAt(right)) {

                    isPalindrome = false;

                    break;

                }

                left++;

                right--;

            }

            if (isPalindrome) {

                System.out.println("That string IS a palindrome.");

            } else {

                System.out.println("That string is NOT a palindrome.");

            }

            System.out.print("Test another (y/n)? ");

            another = scan.nextLine();

        }

    }

}
```

通过逐个字符遍历每个字符串，直到确定字符串是否为回文。`left` 和 `right` 变量存储字符的索引。它们最初指向字符串的两端。内层循环的每次迭代比较 `left` 和 `right` 指向的字符。当字符不匹配（意味着字符串不是回文）或者 `left` 的值等于或大于 `right` 的值（意味着整个字符串已测试完毕且它是回文）时，我们退出内层循环。注意以下短语不是回文：

- A man, a plan, a canal, Panama.

- Dennis and Edna sinned.

- Rise to vote, sir.

- Doom an evil deed, in a mood.

- Go hang a salami; I am a lasagna hog.

这些字符串因为空格、标点符号和大小写的变化而不符合我们的回文标准。然而，如果删除或忽略这些特征，这些字符串正读反读都是相同的。考虑如何更改程序以处理这些情况。这些修改包含在章节末尾的编程项目中。

# break 和 continue 语句

Java 包含了两个影响判断和循环处理的语句。当执行 `break` 语句时，执行将立即转移到控制当前流的语句之后。例如，如果在循环体内部执行 `break` 语句，循环的执行将停止，并执行循环后的语句。它“跳出”循环。

在第 6 章中，我们将看到编写 `switch` 时使用 `break` 语句通常是必要的。然而，在循环中永远不需要 `break` 语句。可以使用等效代码代替。由于 `break` 语句会导致程序从一个地方跳转到另一个地方，在循环中使用 `break` 不是好做法。你可以避免在循环中使用 `break` 语句。

`continue` 语句对循环处理有类似的影响。`continue` 语句类似于 `break`，它会再次评估循环条件，如果仍然为真，则执行循环体。与 `break` 语句一样，`continue` 语句在循环中总是可以避免的，出于同样的原因应该避免。

# 自我复题（答案见附录 N）

SR 5.17 什么是无限循环？具体是什么导致了无限循环？

SR 5.18 下列代码片段产生什么输出？

```java
int low = 0; high = 10;
while (low < high)
{
    System.out.println(low);
    low++;
}
```

SR 5.19 下列代码片段产生什么输出？

```java
int low = 10; high = 0;
while (low <= high)
{
    System.out.println(low);
    low++;
}
```

SR 5.20 下列代码片段产生什么输出？

```java
int low = 0; high = 10;
while (low <= high)
{
    System.out.println(low);
    high = high - low;
}
```

SR 5.21 下列代码片段产生什么输出？

```java
int low = 0; high = 10, mid;
while (low <= high)
{
    mid = low;
    while (mid <= high)
    {
        System.out.print(mid + " ");
        mid++;
    }
    System.out.println();
    low++;
}
```

SR 5.22 假设 int 变量 `value` 已初始化为一个正整数。编写一个 while 循环，打印 `value` 的所有正因数。例如，如果 `value` 为 28，它将打印：

- 1

- 2

- 4

- 7

- 14

- 28

SR 5.23 假设 int 变量 `value` 已初始化为一个正整数。编写一个 while 循环，打印从 1 到 `value` 之间所有数字的正因数。例如，如果 `value` 为 4，它将打印：

- 1

- 2

- 3

- 4

## 5.5 迭代器 (Iterators)

迭代器是一个允许你逐个处理集合项的对象。也就是说，迭代器让你遍历每个项目并根据需要与其进行交互。你的目标可能是计算每个成员的值，或者打印 URL 的不同部分。

Java 标准库中有几个类定义了迭代器对象。其中之一是 `Scanner`，我们已经多次使用它来帮助从键盘读取数据。`Scanner` 类的 `hasNext` 方法返回 `true`，表示至少还有一个待处理的项，而且正如我们之前看到的，它有一个方法可以将下一个输入作为字符串返回。因此，`hasNext` 方法可以作为条件来控制对每个项的处理。

> 核心概念

> 从技术上说，Java 中的迭代器对象是使用 `Iterator` 接口定义的，该接口将在第 7 章中讨论。目前，知道此类对象的存在以及它们可以使集合的处理变得简单是有帮助。

# 读取文本文件

假设我们有一个名为 `urls.inp` 的输入文件，其中包含我们想要以某种方式处理的 URL 列表：

```
www.google.com
www.linux.org/info.html
thelyric.com/calendar/
www.cs.vt.edu/undergraduate/
youtube.com/watch?v=EHRimwRGLs
```

列表 5.10 中的程序从该文件中读取 URL 并对其进行剖析，以显示路径的不同部分。它使用 `Scanner` 对象来处理输入。事实上，它使用了多个 `Scanner` 对象——一个用于读取数据文件的行，另一个用于处理每个 URL 字符串。

```
列表 5.10
********************************************************************
// URLDissector.java      作者: Loftus

// 演示如何使用 Scanner 读取文件输入并使用
// 替代分隔符对其进行解析。
********************************************************************

import java.util.Scanner;
import java.io.*;

public class URLDissector
{
    // 从文件读取 urls 并打印它们的路径组件。
    public static void main(String[] args) throws IOException
    {
        // ... 代码继续 ...
    }
}
```

# 列表 5.10 续

```java
String url;
Scanner fileScan, urlScan;

fileScan = new Scanner(new File("urls.inp"));

// 读取并处理文件的每一行
while (fileScan.hasNext()) {
    url = fileScan.nextLine();
    System.out.println("URL: " + url);

    urlScan = new Scanner(url);
    urlScan.useDelimiter("/");

    // 打印 url 的每个部分
    while (urlScan.hasNext()) {
        System.out.println(" " + urlScan.next());
    }
    System.out.println();
}
```

### 输出

```
URL: www.google.com
www.google.com

URL: www.linux.org/info.html
www.linux.org
info
gnu.html

URL: thelyric.com/calendar/
thelyric.com
calendar

URL: www.cs.vt.edu/undergraduate/
www.cs.vt.edu
undergraduate
about

URL: youtube.com/watch?v=EHRimwRGLs
youtube.com
watch?v=EHRimwRGLs
```

# 第 5 章 条件与循环

此程序中有 while 循环，一个嵌套在另一个内部。外层循环处理文件中的每一行，内循环处理当前行中的每个标记（token）。

变量 `fileScan` 被创建为在输入文件 `urls.inp` 上操作的扫描器。与其传递 `System.in`，而是实例化代表输入文件的 `File` 对象，并将其传递到 `Scanner` 构造函数中。此时，`fileScan` 对象准备好读取并处理来自输入文件的输入。

如果由于某种原因无法找到或打开输入文件，创建 `File` 对象的尝试将抛出 `IOException`，这就是为什么我们在方法头部中添加了 `throws IOException` 子句。（I/O 异常的处理将在第 11 章进一步讨论。）

只要输入文件扫描器的 `hasNext` 方法返回，外层循环的体体就会执行——也就是说，只要数据文件中还有更多待处理的输入。循环的每次迭代都会从输入文件中读取一行（URL）并打印出来。

对于每一行，都会设置一个新的 `Scanner` 对象来解析 URL 字符串的各个部分，该字符串在实例化 `urlScan` 时传递给 `Scanner` 构造函数。内层 `while` 循环在单独的行上读取 URL 的每个标记。

## 5.6 ArrayList 类

既然我们已经在编程语句的数组中使用了循环，让我们来引入一个用于管理一组对象的非常有用的类。`ArrayList` 类是 Java 标准类库中 `util` 包的一部分。`ArrayList` 对象存储一个对象列表，并允许你通过整数索引值来引用每一个对象。我们经常使用循环来扫描列表中的对象，并以某种方式处理它们。

在内部，`ArrayList` 使用一种名为数组（array）的编程结构（名称）来管理列表。数组将在第 8 章中详细讨论，但为了使用 `ArrayList` 类，我们不需要了解数组的细节。`ArrayList` 类是 Java 集合 API 的一部分，这是一组用于组织和管理其他对象的类。我们将在第 13 章中讨论集合类。

> 核心概念

> ArrayList 对象存储一个对象列表，并允许你使用整数索引访问它们。

图 5 列出了 `ArrayList` 的几种方法。你可以通过各种方式添加和删除元素、判断列表是否为空以及获取列表中的元素数量等其他操作。

请注意，`ArrayList` 指的是类型为 `E` 的元素。这是一个泛型类型（E 代表 element，元素），在创建 `ArrayList` 时确定。因此，你只需要创建一个存储特定类型对象的 `ArrayList` 对象即可。给定对象的类型参数写在类名后的角括号中。我们可以讨论管理其他对象的 `ArrayList<String>`，或者管理 `Book` 对象列表的 `ArrayList<Book>`。

你可以在不指定元素类型的情况下创建一个 `ArrayList`，此时 `ArrayList` 存储的是引用（References），这意味着你可以向列表中放入任何类型的对象。这通常不是一个好主意。能够专门于在泛型 `ArrayList` 中存储特定类型的优点是，编译器可以帮助你检查列表中只存储了适当类型的对象。

> 核心概念

> 当创建一个 `ArrayList` 对象时，你需要指定将存储在列表中的元素类型。

`ArrayList` 的索引值从 0、1 开始。从概念上讲，例如，一个 `String` 对象的 `ArrayList` 可能管理以下列表：

- 0 "Bashful"

- 1 "Sleepy"

- 2 "Happy"

- 3 "Dope"

- 4 "Doc"

同样注意，`ArrayList` 存储的是对象的引用。你不能创建一个存储如 `int` 等原始类型值的 `ArrayList`。但此时包装类（wrapper classes）再次派上了用场。例如，你可以根据需要创建 `ArrayList<Integer>` 或 `ArrayList<Double>`。

# 第 5 章 条件与循环

```
ArrayList<E>()
构造函数：创建一个初始为空的列表。

boolean add (E obj)
  将指定的对象插入此列表的末尾。
void add (int index, E obj)
  在列表的指定索引处插入指定的对象。
void clear()
  从此列表中删除所有元素。
E remove (int index)
  返回并返回此列表中指定索引处的元素。
E get (int index)
  返回列表中指定索引处的对象，但不将其移除。
int indexOf(Object obj)
  返回指定对象第一次出现处的索引。
boolean contains(Object obj)
  如果此列表包含指定的对象，则返回 true。
boolean isEmpty()
  如果此列表不包含元素，则返回 true。
int size()
  返回此列表中的元素数量。
```

图 5.8 `ArrayList<E>` 类的一些方法。

列表 5.11 所示的程序实例化了一个名为 `band` 的 `ArrayList<String>`。使用 `add` 方法按特定顺序将几个 `String` 对象添加到 `ArrayList` 的末尾。删除了一个特定的字符串并在特定索引处插入另一个。对于任何其他对象，每当 `ArrayList` 被发送到 `println` 方法时，都会自动创建 `toString` 方法，该方法会打印被方括号围绕的所有元素。程序末尾的 `while` 循环显式地逐行打印每个元素。

```
列表 5.11
****************************************************************************************************************************************************************
// Beatles.java      Author: Lewis/Loftus
//
// 展示了 ArrayList 对象的使用。
****************************************************************************************************************************************************************
```

### 列表 5.11 续
