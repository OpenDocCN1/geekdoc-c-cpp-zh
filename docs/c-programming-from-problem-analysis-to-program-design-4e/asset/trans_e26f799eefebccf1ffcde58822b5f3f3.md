
4. 字面量不能被更改。它们是程序中使用的数字、字符以及字符组合。
5. 类型实际上是通过类实现的。这意味着类被用来定义类型。
6. 一个 `object` 是 `class` 的一个实例。它是 `class` 的一个例子。
7. 值类型通常被称为基本或原始数据类型。它们是语言预定义的数据类型。
8. 值类型包括九种整型（整数）类型、两种浮点类型以及 `decimal` 类型。
9. 所有整型值都表示整数，即没有小数表示的值。值类型 `int` 使用最频繁。
10. 浮点值允许你保留数据项的小数部分。它们可以用带指数的科学计数法指定，也可以用标准十进制表示法指定。
11. `decimal` 格式适用于财务和货币计算。
12. 一个 `bool` 变量的值可以是 `true` 或 `false`。
13. `string` 类型表示 Unicode 字符的组合。
14. `const` 强制实现不允许值被更改的功能。
15. 赋值语句的形式为 变量 = 表达式。
16. 一元运算符需要单个操作数。
17. `++` 和 `--` 的前置递增和后置递增运算符将数字一（1）加到或减去一个存储位置。
18. 复合运算符包括赋值运算符，并用于通过将其原始值作为计算的一部分来修改变量。
19. 执行计算的顺序称为运算顺序。可以在表达式中添加括号以改变顺序。
20. 左结合意味着运算从左到右执行。这意味着在表达式中从左到右移动时，先遇到的运算先执行。
21. 如果二元运算同时涉及 `double` 和 `int`，则会执行隐式类型强制转换。
22. 通过类型转换或类型转换的显式类型强制转换的形式为 (type) expression。

## 练习

1. 以下哪一个是有效的标识符？
- a. `namespace`
- b. variable 1
- c. exampleOfaValue
- d. 3value
- e. value#1

2. 数字 768 是 ________ 类型的例子。
- a. `bool`
- b. integral
- c. floating-point
- d. `struct`
- e. `decimal`

3. 以下哪一个是引用类型？
- a. `int`
- b. `bool`
- c. `string`
- d. `decimal`
- e. integral

4. 不能与标识符一起使用的字符是：
- a. –
- b. $
- c. *
- d. #
- e. all of the above

5. 以下哪一个是保留关键字？
- a. Console
- b. data
- c. int
- d. System
- e. all of the above

6. `float`、`double` 和 `decimal` 之间的主要区别之一是：
- a. `float` 用于表示更多有效数字。
- b. `double` 通常用于大额货币值。
- c. `decimal` 不用于显示负值。
- d. `double` 不需要用 m 或 f 等值后缀数字面量。
- e. `decimal` 主要用于表示需要 $ 进行格式化的较小货币值。

7. 以下哪一个是用于存储本教科书名称的变量的有效声明？
- a. `string` name of book;
- b. `char` nameOfBook;
- c. boolean nameOfBook;
- d. `string` bookName;
- e. `char` book Name;

8. 类型在 C# 中使用以下方式实现：
- a. classes
- b. types
- c. objects
- d. namespaces
- e. programs

9. `int` 类的 `object` 是：
- a. 47.98
- b. 47
- c. `int` class
- d. type `object`
- e. type integral

10. 用于作为标志以指示值是否已达到上限的存储位置的适当声明是什么？
- a. `int` upperLimit;
- b. upperLimit reached;
- c. `bool` upperLimit;
- d. Boolean upperLimit;
- e. `string` upperLimit;

11. 在声明中添加关键字 `const`：
- a. 将一个值放在内存中且不能被更改
- b. 声明常量类型的变量
- c. 必须将其放在标识符之后
- d. 只能与整型一起使用
- e. 在 C# 中被禁止

12. 哪条语句使结果增加 15？
- a. `15 += result;`
- b. `15 =+ result;`
- c. `result =+ 15;`
- d. `result += 15;`
- e. `result = 15 +;`

13. 给定以下声明，算术表达式的结果 ans 中存储的是什么？

```
int ans = 0, v1 = 10, v2 = 19;
ans = --v2 % v1++;
```

- a. 1.8
- b. 9
- c. 8
- d. 2
- e. none of the above

14. 给定以下声明，算术表达式的结果 ans 中存储的是什么？

```
int ans = 10, v1 = 5, v2 = 7, v3 = 18;
ans += v1 + 10 * (v2---- / 5) + v3 / v2;
```

- a. 18
- b. 32
- c. 28
- d. 30
- e. none of the above

15. 以下哪一个将 86 格式化为小数点后显示两位数字？
- a. `{0:C}`
- b. `{0:c}`
- c. `{0:F2}`
- d. all of the above
- e. none of the above

16. 通过在赋值运算符下方放置数字来指示以下赋值语句的运算顺序，如图 2–13 所示。
- a. `ans = value1 + value2 * value3 – (value4 + 20 / 5 % 2) * 7;`
- b. `ans += value1 – – * 10;`
- c. `ans = (((value1 + 7) – 6 * value2) / 2);`
- d. `ans = value1 + value2 / value3 * value4 – –;`

17. 以下哪些是有效的标识符？如果无效，请说明原因。
- a. `intValue`
- b. `value#1`
- c. `the first value`
- d. `_value1`
- e. `AVALUE`

18. 对于以下每项，使用最佳数据类型选择声明一个变量。
- a. 正确答案的数量计数器
- b. 你在信用卡上欠的钱数
- c. 你家乡的名称
- d. 你希望在下次考试中获得的成绩
- e. 你希望本课程学期末被记录的成绩

19. 对于以下每个声明，编写适当的编译时初始化。
- a. 正确答案的数量计数器从零开始
- b. 你在信用卡上欠的钱数是零
- c. 家乡的名称或学校所在城市的名称
- d. 下次考试的成绩为 100
- e. 本课程学期末要记录的成绩为 A

20. 假设 x、y 和 z 是 int 变量且 x = 2、y = 6 且 z = 10。执行以下每个语句后，每个变量的存储位置中会有什么？（对于每个练习，使用原始声明。）
- a. z += ++y % 2;
- b. x = y + 14 - z / 7;
- c. x = y * z / 2 - x * z;
- d. x %= --z - y * 2;
- e. y = (z - y) * 2 + -- y;

21. 假设 x、y 和 z 是 double 变量且 x = 2.5、y = 6.9 且 z = 10.0。执行以下每个语句后，每个变量的存储位置中会有什么？（对于每个练习，使用原始声明。）
- a. z *= y + % 7;
- b. x = (int) y + (14 - z / 7);
- c. x = z / 3 * --y;
- d. z /= (int) y / x;
- e. z = x + y / 4;

22. 以下每个语句的输出会是什么？
- a. Console.Write("Result is {0:c}", 67);
- b. Console.Write("Number {0:f0} is {1:c}", 1, 3);
- c. Console.Write("{0:f0} - {1:c}", 1, 3 * 2);
- d. Console.Write("{0:f0} result " + "xyz {1:f2}", 1, 25);
- e. Console.Write("This is the {0:f0}st example: {1:f2}", 1, 3);

23. 解释变量与常数有何不同。

24. 解释类型、类和对象与字符串的关系。
