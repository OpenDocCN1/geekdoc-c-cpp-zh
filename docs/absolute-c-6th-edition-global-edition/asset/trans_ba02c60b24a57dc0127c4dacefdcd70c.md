
求婚者将被编号为 1，第二位编号为 2，依此类推直到最后一位求婚者，编号为 n。从第一个求婚者开始，她会沿着队伍数三个求婚者（因为她名字的字母有三个），第三个求婚者将被淘汰出赢得她芳心的竞争，并从队伍中移除。Eve 随后会继续，数另外三个求婚者，并淘汰每第三个求婚者。当她到达队伍末尾时，她会从开头继续计数。

例如，如果有六个求婚者，那么淘汰过程将如下进行：
123456 求婚者初始列表，从 1 开始计数
12456 求婚者 3 被淘汰，继续从 4 计数
1245 求婚者 6 被淘汰，继续从 1 计数
125 求婚者 4 被淘汰，继续从 5 计数
15 求婚者 2 被淘汰，继续从 5 计数
1 求婚者 5 被淘汰，1 是幸运的赢家

编写一个程序，使用 vector 来确定如果你有 n 个求婚者，应该站在哪个位置才能娶到公主。你会发现 Vector 类中的以下函数很有用：

```
v.erase(iter);
// Removes element at position iter
```

例如，要使用此函数从名为 theVector 的 vector 变量开头删除第四个元素，请使用

```
theVector.erase(theVector.begin() + 3);
```

使用数字 3 是因为 vector 中的第一个元素位于索引位置 0。

6. 本编程项目要求你首先完成第 6 章的编程项目 6.7，这是一个 Pizza 类的实现。添加一个 Order 类，其中包含一个类型为 Pizza 的私有 vector。此类表示客户的整个订单，订单可能包含多个披萨。包含适当的函数，以便 Order 类的用户可以向订单中添加披萨（类型为深盘、手抛或平底；尺寸为小、中或大； pepperoni 或奶酪配料的数量）。你可以使用常量来表示类型和尺寸。还编写一个函数来输出订单中的所有内容以及总价格。编写一个合适的测试程序，将多个披萨添加到订单中。

7. 做编程项目 6.8，Money 类的定义，除了创建一个默认构造函数，将货币金额设置为 0 美元和 0 美分，并创建一个第二个构造函数，具有美元和美分变量金额的输入参数。修改你的测试代码以调用构造函数。

- 8. 编写一个程序，输出一个班级学生作业成绩的直方图。程序应输入每个学生的成绩作为整数，并将成绩存储在 vector 中。成绩应输入直到用户为成绩输入 −1 为止。程序随后应扫描 vector 并计算直方图。在计算直方图时，成绩的最小值为 0，但你的程序应确定用户输入的最大值。将直方图输出到控制台。有关如何计算直方图的详细信息，请参阅编程项目 5.7。

- 9. 在 2009 年之前，美国邮政服务用于信封上的条形码使用一种称为 POSTNET 的格式表示五位（或更多）邮政编码。条形码由一个长条和三十个条组成，如下所示：

![](img/c76bba8c1d927f399768ffe2ab5f5bee_353_0.png)

对于此程序，我们将条形码表示为数字字符串。数字 1 表示长条，数字 0 表示短条。因此，所示的条形码在我们的程序中将表示如下：

```
110010010010100101000101001
```

条形码的第一个和最后一个数字始终为 1。去掉它们后剩下 25 个数字。如果将这 25 个数字分成每组五个数字，则我们有以下内容：

```
10100 10100 01010 11000 01001
```

接下来，考虑每组五个数字。每组数字中始终恰好有两个 1。每个数字代表一个数字。从左到右，数字编码的值为 7、4、2、1 和 0。将对应值与数字相乘并计算总和以得到邮政编码的最终编码数字。下表显示了 10100 的编码。

|  | 1 | 0 | 1 | 0 | 0 |
|---|---:|---:|---:|---:|---:|
| **Value** | 7 | 4 | 2 | 1 | 0 |
| **Product of Digit * Value** | 7 | 0 | 2 | 0 | 0 |

Zip Code Digit = 7 + 0 + 2 + 0 + 0 = **9**

对每组五个数字重复此操作并连接起来得到完整的邮政编码。有一个特殊值。如果一组五个数字的总和为 11，则表示数字 0（这是必要的，因为每组两个数字无法表示零）。样本条形码的邮政编码解码为 90504。虽然 POSTNET 方案似乎不必要地复杂，但其设计允许机器检测扫描邮政编码时是否出现错误。

编写一个 `zip` 代码类，用于编码和解码美国邮政服务在信封上使用的五位条形码。该类应有两个构造函数。第一个构造函数应以整数形式输入邮政编码，第二个构造函数应以如上所述由 0 和 1 组成的条形码字符串形式输入邮政编码。虽然你有两种输入邮政编码的方式，但在内部，类应仅使用一种格式存储邮政编码。（你可以选择将其存储为条形码字符串或邮政编码数字。）该类还应至少有两个公共成员函数：一个返回邮政编码作为整数，另一个以字符串形式返回邮政编码的条形码格式。所有辅助函数应声明为私有。将你的类定义嵌入到合适的测试程序中。

- 10. 首先，完成编程项目 6.12。修改 main 函数，使用一个循环，以便用户决定创建多少个 `BoxOfProduce` 对象。每个盒子应包含从以下列表中随机选择的三种水果或蔬菜捆：tomatillo、broccoli、tomato、kiwi 和 kale。添加一个菜单，以便用户可以决定何时停止创建盒子。菜单应允许用户对盒子中随机选择的项目进行替换。

你希望在盒子包含 tomatillos 时附赠一份免费的 salsa verde 食谱传单。然而，只有 5 张食谱传单。将一个静态成员变量添加到 `BoxOfProduce` 类中，统计剩余的食谱传单数量并初始化为 5。还添加一个成员变量来指示盒子是否包含食谱传单，并修改输出函数以在盒子包含食谱传单时也打印“salsa verde recipe”。最后，在类内部添加逻辑，以便如果盒子包含至少一个 tomatillos 订单，则在所有食谱传单用完之前自动获得一份食谱传单。

通过使用菜单创建包含 tomatillos 的盒子，直到所有传单用完来测试你的类。

- 11. 做编程项目 5.19，但这次使用名为 `Player` 的类来存储玩家的姓名和分数。确保为此类包含一个构造函数来设置姓名和分数。然后使用 `Player` 类的 vector 来存储十名玩家。

## Operator Overloading, Friends, and References 8

## 8.1 BASIC OPERATOR OVERLOADING 356

- Overloading Basics 357
- Tip: A Constructor Can Return an Object 362
- Returning by const Value 363
- Overloading Unary Operators 366
- Overloading as Member Functions 366
- Tip: A Class Has Access to All Its Objects 369
- Overloading Function Application ( ) 369
- Pitfall: Overloading &&, ||, and the Comma Operator 370

## 8.2 FRIEND FUNCTIONS AND AUTOMATIC TYPE CONVERSION 370

- Constructors for Automatic Type Conversion 370
- Pitfall: Member Operators and Automatic Type Conversion 371
- Friend Functions 372
- Friend Classes 375
- Pitfall: Compilers without Friends 376

## 8.3 REFERENCES AND MORE OVERLOADED OPERATORS 377

- References 378
- Tip: Returning Member Variables of a Class Type 379
- Overloading >> and << 380
- Tip: What Mode of Returned Value to Use 386
- The Assignment Operator 389
- Overloading the Increment and Decrement Operators 389
- Overloading the Array Operator [ ] 392
- Overloading Based on L-Value versus R-Value 394

