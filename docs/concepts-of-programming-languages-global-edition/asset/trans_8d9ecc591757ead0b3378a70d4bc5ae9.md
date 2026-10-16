

```
if ((listLen > 0) && (listLen < 100)) {

    // Get the input and compute its sum
    for (counter = 0; counter < listLen; counter++) {
        intList[counter] = prompt (
            "Please type the next number", "");
        sum += parseInt(intList[counter]);
    }

    // Compute the average
    average = sum / listLen;

    // Count the input values that are > average
    for (counter = 0; counter < listLen; counter++)
        if (intList[counter] > average) result++;

    // Display the results
    document.write("Number of values > average is: ",
        result, "<br />");
} else
    document.write(
        "Error - input list length is not legal <br />");
```

## 2.18.3 PHP 的起源与特点

PHP (Tatroe, et al., 2013) 由 Apache 组的成员 Rasmus Lerdorf 于 1994 年开发。他的最初动机是提供一个工具来帮助跟踪他个人网站的访问者。1995 年，他开发了一个名为 Personal Home Page Tools 的软件包，这成为 PHP 的第一个公开分发版本。最初，PHP 是 Personal Home Page 的缩写。后来，其用户社区开始使用递归名称 PHP: Hypertext Preprocessor，这随后使原始名称变得默默无闻。PHP 现在作为开源产品进行开发、分发和支持。PHP 处理器驻留在大多数 Web 服务器上。

PHP 是一种专门为 Web 应用程序设计的 HTML 嵌入式服务器端脚本语言。当浏览器请求嵌入其中的 HTML 文档时，PHP 代码会在 Web 服务器上被解释。PHP 代码通常会产生 HTML 代码作为输出，该输出会替换 HTML 文档中的 PHP 代码。因此，Web 浏览器永远看不到 PHP 代码。

PHP 在语法外观、字符串和数组的动态特性以及动态类型的使用方面与 JavaScript 相似。PHP 的数组是 JavaScript 数组和 Perl 哈希的结合。

PHP 的原始版本不支持面向对象编程，但在第二个版本中添加了该支持。然而，PHP 不支持抽象类或接口、析构函数或类成员的访问控制。

PHP 允许简单地访问 HTML 表单数据，因此使用 PHP 进行表单处理很容易。PHP 为许多不同的数据库管理系统提供支持。这使其成为构建需要 Web 访问数据库的程序的有用语言。

## 2.18.4 Python 的起源与特点

Python (Lutz, 2013) 是一种相对较新的面向对象的解释型脚本语言。其初始设计由荷兰 Stichting Mathematisch Centrum 的 Guido van Rossum 在 1990 年代初期完成。其开发现在由 Python 软件基金会进行。Python 用于与 Perl 相同的应用类型：系统管理、CGI 编程和其他相对较小的计算任务。Python 是一个开源系统，可用于大多数常见的计算平台。Python 实现可在 www.python.org 获取，该网站还提供有关 Python 的大量信息。

Python 的语法不直接基于任何常用语言。它是类型检查的，但动态类型。与其使用数组，Python 包含三种数据类型结构：列表；不可变列表，称为元组；以及哈希，称为字典。有一组列表方法，如 append、insert、remove 和 sort，以及一组用于字典的方法，如 keys、values、copy 和 has_key。Python 还支持列表推导，其起源于 Haskell 语言。列表推导在第 15.8 节中讨论。

Python 是面向对象的，包含 Perl 的模式匹配功能，并具有异常处理。垃圾回收用于在对象不再需要时回收它们。

对 CGI 编程的支持，特别是表单处理，由 cgi 模块提供。还提供支持 cookie、网络和数据库访问的模块。

Python 包括对其线程的并发支持，以及对其套接字的网络编程支持。它还比其他非函数式编程语言提供更多对函数式编程的支持。

Python 的一个更有趣的特性是它可以由任何用户轻松扩展。支持扩展的模块可以用任何编译语言编写。扩展可以添加函数、变量和对象类型。这些扩展被实现为对 Python 解释器的补充。

## 2.18.5 Ruby 的起源与特点

Ruby (Thomas et al., 2005) 由 Yukihiro Matsumoto（又名 Matz）在 1990 年代初期设计，并于 1996 年发布。此后它不断发展。Ruby 的动机是其设计者对 Perl 和 Python 不满意。虽然 Perl 和 Python 都支持面向对象编程，

但两者都不是纯面向对象的语言，至少在每个都有原始的（非对象）类型并且每个都支持函数这一意义上如此。

Ruby 的主要特征是它是一种纯面向对象的语言，就像 Smalltalk 一样。每个数据值都是一个对象，所有操作都是通过方法调用进行的。Ruby 中的运算符只是指定相应操作的方法调用的语法机制。因为它们是方法，所以可以重新定义。所有类，无论是预定义还是用户定义，都可以被子类化。

Ruby 中的类和对象在动态方面都是动态的，因为方法可以动态地添加到两者中。这意味着类和对象在执行期间的不同时间可以具有不同的方法集。因此，同一类的不同实例化可以表现不同。方法、数据和常量的集合可以包含在类的定义中。

Ruby 的语法与 Eiffel 和 Ada 相关。由于使用动态类型，因此无需声明变量。变量的作用域在其名称中指定：以字母开头的变量具有局部作用域；以 @ 开头的变量是实例变量；以 $ 开头的变量具有全局作用域。Ruby 中存在 Perl 的许多特性，包括具有愚蠢名称的隐式变量，例如 $_。

与 Python 一样，任何用户都可以扩展和/或修改 Ruby。Ruby 在文化上很有趣，因为它是第一种在日本设计并在美国获得相对广泛使用的编程语言。

## 2.18.6 Lua 的起源与特点

Lua 由 Roberto Ierusalimschy、Waldemar Celes 和 Luis Henrique de Figueiredo 于 1990 年代初期在巴西里约热内卢教皇大学设计。它是一种脚本语言，支持过程式和函数式编程，其主要目标之一是可扩展性。影响其设计的语言包括 Scheme、Icon 和 Python。

Lua 与 JavaScript 相似，因为它不支持面向对象编程，但它显然受到了其影响。两者都有充当类和对象的角色的对象，并且两者都有原型继承而不是类继承。然而，在 Lua 中，语言可以扩展以支持面向对象编程。

与 Scheme 一样，Lua 的函数是第一类值。此外，Lua 支持闭包。这些功能使其可用于函数式编程。Lua 与 Scheme 也有相似之处，它只有一个数据结构，尽管在 Lua 的情况下，它是表。Lua 的表扩展了 PHP 的关联数组，后者取代了传统命令式语言的数组。对表元素的引用可以采用传统数组、关联数组或记录的引用形式。因为函数是第一类值，所以它们可以存储在表中，这样的表可以充当命名空间。

## 以下是一个 C# 程序的示例：

```
// C# Example Program
// Input: An integer, listlen, where listlen is less than
// 100, followed by listlen-integer values.
// Output: The number of input values that are greater
// than the average of all input values.
using System;
public class Ch2example {
static void Main() {
int[] intlist;
int listlen, counter, sum = 0, average, result = 0;
intList = new int[99];
listlen = Int32.Parse(Console.readLine());
if ((listlen > 0) && (listlen < 100)) {
// Read input into an array and compute the sum
for (counter = 0; counter < listlen; counter++) {
intList[counter] = Int32.Parse(Console.readLine());
sum += intList[counter];
} // end of for (counter ...
// Compute the average
average = sum / listlen;
// Count the input values that are > average
foreach (int num in intList)
if (num > average) result++;
// Print result
Console.WriteLine(
"Number of values > average is:" + result);
} // end of if ((listlen ...
else
Console.WriteLine(
"Error--input list length is not legal");
} // end of method Main
} // end of class Ch2example
```

## 2.20 标记-编程混合语言

标记-编程混合语言是一种标记语言，其中某些元素可以指定编程操作，例如控制流和计算。以下小节介绍两种此类混合语言，XSLT 和 JSP。

