
使用 Visual Studio 2008 IDE 创建 XML 输出文件时，必须激活“属性”页面。接下来，选择“生成”。然后，选中“XML 文档文件”复选框并指定 XML 文件的名称。

## 一个 XML 文档示例

这里有一个示例演示了多个文档注释。它同时使用了多行和单行形式。顺便提一下，许多程序员即使注释跨越多行，也会使用一系列单行文档注释而不是多行注释。（本示例中的多个注释采用了这种方法。）优点是它能清楚地标识较长文档注释中的每一行都是文档注释的一部分。当然，这是一个风格问题，但它是常见做法。

// A documentation comment example.

using System;

/** <remark>
This is an example of multiline XML documentation.
The Test class demonstrates several tags.
</remark>
*/

class Test {
/// <summary>
/// Main is where execution begins.
/// </summary>
static void Main() {
int sum;

sum = Summation(5);
Console.WriteLine("Summation of " + 5 + " is " + sum);
}

/// <summary>
/// Summation returns the summation of its argument.
/// <param name="val">The value to be summed is passed in val.</param>
/// <see cref="int" />
/// <returns> The summation is returned as an int value.</returns>
/// </summary>
static int Summation(int val) {
int result = 0;

for(int i=1; i <= val; i++)
result += i;

return result;
}
}

![](img/7022d9b97326a713562c15aa43977d15_895_0.png)

假设前面的程序名为 XmlTest.cs，以下行将编译程序并生成一个名为 XmlTest.xml 的文件，其中包含注释：

```
csc XmlTest.cs /doc:XmlTest.xml
```

编译后，将生成以下 XML 文件：

```
<?xml version="1.0"?>
<doc>
  <assembly>
    <name>DocTest</name>
  </assembly>
  <members>
    <member name="T:Test">
      <remark>
        This is an example of multiline XML documentation.
        The Test class demonstrates several tags.
      </remark>
    </member>
    <member name="M:Test.Main">
      <summary>
        Main is where execution begins.
      </summary>
    </member>
    <member name="M:Test.Summation(System.Int32)">
      <summary>
        Summation returns the summation of its argument.
        <param name="val">
          The value to be summed is passed in val.
        </param>
        <see cref="T:System.Int32" /> </see>
        <returns>
          The summation is returned as an int value.
        </returns>
      </summary>
    </member>
  </members>
</doc>
```

请注意，每个已记录的元素都被赋予一个唯一标识符。其他使用 XML 文档的程序可以使用这些标识符。

## 符号

### A

-   &
-   按位与，73–76
-   逻辑与，67, 68, 70, 71, 229–235
-   指针运算符，587
-   &&（短路或条件与），67, 70–71, 229, 231–235
-   *
-   乘法运算符，24, 63
-   指针运算符，586–587, 594, 595
-   @ 用于指定逐字字符串文字，48–49
-   @ - 限定关键字，33–34
-   |
-   按位或，73, 76–77
-   逻辑或，67, 68, 69–70, 71, 229–235
-   ||（短路或条件或），67, 70, 71, 229, 231–235
-   [, 137, 138, 142, 151, 245, 483, 484, 598
-   ^
-   按位异或，73, 77–78
-   逻辑异或，67, 68
-   :（冒号），271, 278, 334
-   :: 命名空间别名限定符，447–451
-   [], 20, 21, 29, 31, 52, 118, 140, 143, 414, 416, 569
-   与格式说明符一起使用，43–46
-   =, 24, 71–72
-   =（关系运算符），27, 67, 537
-   重载，224, 226, 306
-   和字符串，158, 665
-   => lambda 运算符，413–414
-   |, 67, 68, 69–70, 229–231
-   !=, 27, 67, 537
-   重载，226
-   和字符串，158, 665
-   /, 24, 63
-   /* */, 20
-   /** */, 867
-   //, 21
-   ///, 867
-   <
-   I/O 重定向运算符，381–382
-   关系运算符，27, 67, 224–226
-   > , 497
-   <<, 73, 79–81
-   <=, 27, 67, 226
-   –, 24, 63
-   =
-   复合赋值运算符，72
-   和委托，404
-   和事件访问器，425
-   ->, 589
-   –, 29, 63, 64–65
-   重载，217
-   %
-   取模运算符，63–64
-   与自定义日期和时间占位符字符一起使用，698
-   (), 21, 63, 116, 122
-   .(点运算符)，111, 119, 205, 332, 589
-   +
-   加法运算符，24, 63
-   用其连接字符串，159, 670
-   与 WriteLine() 一起使用，24
-   +=
-   复合赋值运算符，72
-   和委托，404
-   和事件访问器，425
-   ++, 29, 63, 64–67
-   重载，217–220
-   #
-   与预处理器指令一起使用，451
-   与 WriteLine() 一起使用，45, 692–695
-   ?
-   条件运算符，82–83
-   与可空类型声明一起使用，599
-   ?? 空合并运算符，601–602
-   >
-   I/O 重定向运算符，381–382
-   关系运算符，27, 67, 224–226
-   >>, 73, 79–81
-   >=, 27, 67, 226
-   ;（分号），21, 31, 92, 143, 409, 548
-   用于自定义格式说明符，693–694, 695
-   ~
-   按位非，73, 78–79
-   用于析构函数声明，131–132
-   Abort()，741–745
-   Abs()，193, 618
-   抽象类型修饰符，294, 301, 305
-   访问控制，165–172
-   使用 public 和 private 的指南，167–168
-   访问修饰符/说明符，110, 116, 165–166, 261–264, 458
-   访问器，245
-   事件，424–429
-   索引器，246, 248–249
-   属性，254–255, 259–260
-   与其一起使用访问修饰符，261–264
-   acos()，618
-   Action 委托，653–654
-   add 事件访问器，425, 428
-   Add()，631, 752, 763, 776, 777, 787, 790, 792, 794, 796, 852–853, 859, 860, 864
-   和集合初始化器，819
-   AddAfter()，784
-   AddBefore()，784
-   AddFirst()，784
-   AddLast()，784
-   AddMemoryPressure()，658
-   AddRange()，756, 780
-   ADO.NET 数据集，546
-   All() 扩展方法，578–579
-   AllKeys 属性，834
-   AllowMultiple 命名参数，491
-   AND 运算符
-   按位（&），73–76
-   逻辑（&&），67, 68, 70, 71, 229–235
-   短路或条件（&&），67, 70–71, 229, 231–235
-   And()，772
-   Any() 扩展方法，578–579
-   Application 类，851
-   Application.EnableVisualStyles()，851
-   Application.Exit()，858
-   ApplicationException，354
-   ArgumentException，372, 378, 380, 381, 384, 802, 805
-   ArgumentNullException，372, 378, 380, 381, 384, 397, 753, 777, 830
-   ArgumentOutOfRangeException，372, 758
-   参数，21, 116, 122
-   命令行，200–202

参数（续）
传递，174-176
类型。参见 Type argument(s)
可变数量的，使用，
182-185
算术运算符，24, 63-67
Array 类，641-654, 762
方法，表，642-647
属性，表，641-642
Array.ForEach()。参见 ForEach()
数组，137-152
数组的，144, 146
边界，141, 338
边界错误，使用索引器
防止由此引起的运行时异常，
246-249, 252-254
边界错误，使用一个
属性防止由此引起的运行时
异常，256-259，
262-264
复制一个，651-652
自定义，使用索引器和
属性创建，264-268
动态，268, 755, 779
和定长缓冲区，596-598
使用 foreach 循环遍历，
153-156
一般形式，137-138，
141, 142
和 Enumerable<T>
接口，546, 547, 550, 566, 576
在 C# 中作为对象实现，
137-138, 148
隐式类型，151-152
索引（访问元素），
138-139, 142, 145
初始化，140, 143-144
使用 I/O，392-394
不规则，144-146, 150-151, 152
Length 属性，148-151
和 LINQ，151, 152, 546
多维，141-146
以 null 结尾，593
一维，137-141
参数 params，182-185
指针的，595
指针和，591-593
矩形，144
引用变量，分配，
146-147
从方法返回，187-188
反转一个，650-651
排序，648-650
搜索，155-156, 648-650
字符串的，160-161

ArrayList 类，749, 755-762, 774, 779
方法，表，756-758
ArrayTypeMismatchException，353
箭头运算符 (->)，589
as 运算符，439, 460-462
ascending 上下文关键字，
550, 553
ASCII 字符集，41, 363
ASCIIEncoding，664
Asin()，618
ASP.NET，457, 821
AsQueryable() 扩展方法，752
AsReadOnly<T>()，642
Assembly，166, 457-458
别名，610-611
和 DLL 文件，480-481
友元，605
和反射，475-481
Assembly 属性，464
赋值运算符
=, 24, 71-72
算术和逻辑
复合 (op=)，72
按位复合，81
和运算符重载，
239-240
赋值
引用变量和，115-116，
146-147, 328, 329-330
结构，328-329
类型转换，55-58
Atan()，618
Atan2()，618
Attribute 类，483, 484, 485
属性，459, 464, 483-493
附加，484-485
内置，491-493
创建，484
和命名参数，487-490
检索，485-486
Attributes 属性，464
AttributeTargets 枚举，491
AttributeUsage 属性，484, 491
AuthenticationLevel 属性，825
AutoResetEvent 类，737, 739
Average() 扩展方法，578-579

### B

后备字段，259, 260
反斜杠字符常量，47
base 关键字
访问隐藏的基类
成员，278, 283-285

调用基类构造函数，
278-282, 288, 355, 358
BaseAddress 属性，843
BaseType 属性，464
BigMul()，618
BinaryReader 类，367, 383, 384-390
输入方法，表
常用，385
BinarySearch()，642, 648, 756，
760-761, 780
BinaryWriter 类，367, 383-384，
386-390
输出方法，表
常用，384
BindingFlags 枚举，468
位字段，700
BitArray 类，750, 771-774
方法，表，772
BitConverter 类，654-656
方法，表，655-656
按位运算符，73-81
代码块，21, 29-31, 52
和匿名方法，
409-411
和名称隐藏，54
bool 值类型，36, 42-43, 623
和逻辑运算符，67, 68
和关系运算符，43, 67
布尔表达式，27
Boolean 结构，623, 640-641
方法，表，640-641
Bottom 属性，855
装箱和拆箱，307-309
break 语句，85, 89, 91, 102-104，
107, 154, 815
BufferedStream 类，365
缓冲区，定长，596-598
Button 类，852, 854, 856
ButtonBase 类，852
Byte .NET 结构，396, 397, 623
byte 值类型，36, 37, 38, 363，
396, 625
字节码，5, 8

### C

C 格式说明符，45-46
C，历史，3-4
C++，历史，4
C#
作为组件导向
语言，6-7
大小写敏感，21
历史，3, 5-7
Internet 和，821
和 Java，3, 6
