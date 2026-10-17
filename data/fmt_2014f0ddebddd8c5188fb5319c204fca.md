
```
for (int row = 0; row < sales.GetLength(0); row++)

{

    name = salesman[row].Split(' ');

    Console.Write("{0,-20}", name[1] + ", " + name[0]);

    for (int col = 0; col < sales.GetLength(1); col++)

    {

        Console.Write("{0, 11:N2}", sales[row, col]);

    }

    Console.WriteLine();

}

}
```

一次测试运行的输出如图 8-12 所示。

![](img/45e6f245af31396d967c3186f196d331_481_0.png)

**图 8-12** TempAgency 应用输出

### 编码标准

你开发的每个项目都应该遵循约定的编码标准。它们能让你的代码更具可读性并有助于减少错误。

### 集合命名指南

使用单数名词作为集合对象的标识符。

在实例化集合对象时，使用驼峰命名法。

## 高级数组建议

如果方法返回一个集合且没有值可返回，请返回一个空集合而不是 `null`。

在处理集合时，尽可能使用 `.NET` 预定义的方法和属性而不是编写新代码。

## 资源

你可能想要探索的额外网站：

数据结构的深度解析

`http://msdn.microsoft.com/en-us/library/aa289148(VS.71).aspx`

实现简单的哈希算法

`http://blog.roblevine.co.uk/?p=15`

## 快速复习

- 1. 二维数组和多维数组可以包含任意数量的相同类型的变量。使用一个通用标识符命名整个结构。
- 2. 二维数组和多维数组应该使用单数名词命名。
- 3. 要访问二维或多维数组元素，请使用声明中包含的索引数量。索引由逗号分隔并括在方括号中。
- 4. 当将二维或多维数组作为方法参数使用时，要指定数组标识符和类型；不包含数组的长度或大小。需要开启、闭括号和逗号。调用该方法时仅包含数组名称。
- 5. 二维数组和多维数组可以作为参数传递给方法，此外方法可以使用二维或多维数组作为返回类型。方法名称前的方括号为空，除非有一个或多个逗号。分隔符标识维数。
- 6. 二维数组和其他多维数组遵循与一维数组相同的指南。
- 7. 二维数组通常被可视化为分为行和列的表格。
- 8. 二维数组和多维数组、交错数组（jagged arrays）的长度可以不同。
- 9. `ArrayList` 创建列表。
- 10. 二维数组和多维数组、交错数组的长度可以不同。
- 11. `String` 类是不可不可的。
- 12. `String` 类不能被修改。
- 13. `String` 方法是内置的。
- 14. `Hashtable` 表示键/值对。
- 15. `BitArrays` 对大数据很有用处。
- 16. `Queue` 代表先进先出 (FIFO)。
- 17. `Stack` 代表后进先出 (LIFO)。

## 练习

- 1. 当括号内包含三个值时，该数字代表：
    a. 类
    b. 行
    c. 平
    d. 列
    e. 以上都不是
- 2. 下列哪种声明允许你存储每天的高温和低温？
    a. `int[temp1Lo, temp2Lo, temp3Lo, temp4Lo, temp5Lo, temp6Lo, temp7Lo, temp1Hi, temp2Hi, temp3Hi, temp4Hi, temp5Hi, temp6Hi, temp7Hi, 2];`
- 3. 假设声明了一个名为 `num` 的二维数组用于存储 4 行 7 列。以下哪条语句正确地将值 100 分配给第三列？
    a. `for(x = 0; x < 3; ++x) num[x, 2] = 100`
    b. `for(x = 0; x < 4; ++x) num[x, 2] = 100;`
    c. `for(x = 1; x < 4; ++x) num[x, 2] = 100;`
    d. `for(x = 1; x < 5; ++x) num[x, 2] = 100;`
    c. 以上都不是
- 4. 选择不适用于以下声明的语句：
    `double[][] totalCostOfItems = {{109.95, 169.95, 1.50, 89.95}{27.9, 18.6, 26.8, 98.5}};`
- 5. 方法 `anArray` 返回什么值？

6. 可以声明用于存储值的最大维度数组是几？
a. 10
b. 100
c. 3
d. 5
e. 没有限制

7. 使用以下声明：
`char [, ] n = {{'a', 'b', 'c', 'd', 'e'}, {'f', 'g', 'h', 'i', 'j'}};`
`n[1, 1]` 指的是什么？

a. a
b. f
c. b
d. g
e. 以上都不是

8. 二维数组是一个 _________ 的数据项列表。
a. 所有项具有相同类型
b. 所有项名称都不同
c. 所有都是整数
d. 所有最初都被设置为空字符 ('\0')
e. 以上都不是

9. 使用以下声明：
`int [, ] x = {{12, 13, 14, 15}, {16, 17, 18, 19}};`
`x[2, 4]` 指的是什么？

a. 19
b. 18
c. '\0'
d. 0
e. 以上都不是

## 练习 453

10. 下列哪个选项将当前存储 14 的数组元素加上 95？
`int [ , ] x = {{12, 13}, {14, 15}, {16, 17}, {18, 19}};`

a. `x[2] += 95;`
b. `x[1, 0] += 95;`
c. `x[1, 0 += 95;`
d. `x = 14 + 95;`
e. 以上都不是

11. 下述语句分配了多少个组件？
`double [ , ] values = new double [3, 2];`

a. 32
b. 3
c. 5
d. 6
e. 以上都不是

12. 给第 11 题中 `values` 的声明，你如何将在最后一个物理位置存储 0？

a. `values = 0;`
b. `values[6] = 0;`
c. `values[3, 2] = 0;`
d. `values[2, 1] = 0;`
e. 以上都不是

13. 如果你声明一个数组为 `int [,] anArray = new int[5, 3]`，你可以通过语句将 `anArray [2, 1]` 中存储的值翻倍：

a. `anArray [2, 1] = anArray [5, 1] * 2;`
b. `anArray = anArray * 2;`
c. `anArray [2, 1] *= anArray [2, 1] * 2;`
d. `anArray [2, 1] *= 2;`
e. 以上都不是

## 第 8 章 高级集合

14. 使用以下声明：
`int [ , ] points =`
`{{300, 100, 200, 400, 600},`
`{550, 700, 900, 100}};`

语句 `points [1, 3] = points [1, 3] + 10;` 将
a. 将 300 替换为 310，并将 900 替换为 910
b. 将 500 替换为 510
c. 将 900 替换为 910
d. 将 800 替换为 810
e. 以上都不是

15. 使用以下声明：
`int [ , ] points =`
`{{300, 100, 200, 400, 600},`
`{550, 700, 900, 200, 100}};`

语句 `points [0, 4] = points [0, 4-2];` 将
a. 将 400 替换为 2
b. 将 300 和 600 替换为 2
c. 将 600 替换为 200
d. 导致错误
e. 以上都不是

16. 语句 `Console.Write(points [1, 2] + points [0, 3]);` 将
a. 显示 900400
b. 显示 1300
c. 显示 "points[1, 2] + points[0, 3]"
d. 导致错误
e. 以上都不是

17. 当你从 `ArrayList` 传递一个元素到方法时，该方法接收：
a. `ArrayList` 的副本
b. `ArrayList` 的地址
c. `ArrayList` 中元素值的副本
d. `ArrayList` 中元素的地址
e. 以上都不是

18. 当你将整个 `ArrayList` 传递给一个方法时，该方法接收：

a. `ArrayList` 的副本
b. `ArrayList` 的地址
c. `ArrayList` 中第一个值的副本
d. `ArrayList` 中每个元素的地址
e. 以上都不是

19. 要将字符串中的大写字母转换为其对应的小写字母，你可以使用字符串类中的 ________________ 方法。

a. `IsLower()`
b. `ConvertLower()`
c. `Lower()`
d. `ToLower()`
e. 以上都不是

20. `ArrayList` 类中的哪个方法可以将一个值置于 `ArrayList` 的末尾？

a. `Add()`
b. `AddLast()`
c. `Add()`
d. `Insert()`
e. 以上都不是

21. `ArrayList` 类中的哪个方法可以获取或设置 `ArrayList` 可以包含的元素数量？

a. `Length()`
b. `Size()`
c. `Dimension()`
d. `Rank()`
e. `Capacity()`

22. 哪个类包含创建一维结构的方法？

a. `Array`
b. `string`
c. `array`
d. `ArrayList`
e. 以上都是

23. 具有以下头部 `result(int [] anArray, int num)` 的正确方法调用是：
a. `Console.Write(result(anArray, 3));`
b. `result(anArray, 30);`
c. `Console.Write(result(anArray, 0));`
e. 以上都不是

24. 对于数组，`foreach` 语句的限制是：
a. 只能读取
b. 仅用于整数类型
c. 不能用于多维数组
d. 仅用于小于 1000 的数组
e. 不能用于动态数组

25. 为了从 `Queue` 对象中检索值，你会使用哪种方法？
a. `Pop()`
b. `Push()`
c. `Dequeue()`
d. `Enqueue()`
e. 以上都不是

26. 使用以下字符串回答 a 到 e。
`string sValue = "Today is the first Day of the rest of your life."`
a. 创建一个除 Day 单词外全是小写的字符串。Day 应该是大写的。
b. 创建一个包含元素的字符串数组。`sValue` 中的每个单词应在一个单元格中。
c. 从 b 步创建的数组中删除句号。显示数组的内容。
d. 在 `sValue` 两端加上星号。
e. 将 `sValue` 中的单词 first 替换为 best。

## 编程练习

27. 使用以下声明：
```
int [,] anArray = {{34, 55, 67, 89, 99}, {22, 68, 11, 19, 45}};
```
以下输出语句的结果是什么：

a. `Console.WriteLine(anArray[1, 2]);`
b. `Console.WriteLine(anArray[0, GetLength(0) - 2]);`
c. `Console.WriteLine(anArray[0, 2 + 1] * anArray[0, 0]);`
e. `Console.WriteLine(anArray.Rank);`

28. 使用以下声明，编写 a 到 e 的解决方案：
```
int [,] cArray = new int [2, 3];

string [,,] dArray = new string [5, 2, 6];
```
