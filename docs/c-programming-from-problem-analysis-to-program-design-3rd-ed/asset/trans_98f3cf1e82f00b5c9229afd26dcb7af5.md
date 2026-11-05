
3. 假设声明了一个名为 num 的二维数组，用于存放四行七列。下列哪条语句能正确地将值 100 赋给每一行的第三物理列？

- a. for(x = 0; x < 3; ++x) num[x, 2] = 100;
- b. for(x = 0; x < 4; ++x) num[x, 2] = 100;
- c. for(x = 1; x < 4; ++x) num[x, 2] = 100;
- d. for(x = 1; x < 5; ++x) num[x, 2] = 100;
- e. 以上都不是

4. 选择不适用于以下声明的语句：

```csharp
double[,] totalCostOfItems = {{109.95, 169.95, 1.50, 89.95}, {27.9, 18.6, 26.8, 98.5}};
```

- a. 声明一个浮点值二维数组
- b. 将最大行数设为 4
- c. 将数组元素 totalCostOfItems[0, 1] 设置为 169.95
- d. 在内存中声明一个可存储 double 类型数据的区域
- e. 以上都正确

5. 名为 result 的方法返回什么值？

```csharp
int result(int[,] anArray)
{
    int j = 0,
        i = 0;
    for(int r = 0; r < anArray.GetLength(0); r++)
        for(int c = 0; c < anArray.GetLength(1); c++)
            if (anArray[r, c] < anArray[i, j])
            {
                i = r;
                j = c;
            }
    return i;
}
```

- a. 数组 anArray 中最大元素的行索引
- b. 数组 anArray 中最大元素的值
- c. 数组 anArray 中最小元素的行索引
- d. 数组 anArray 中最小元素的列索引
- e. 最后一个大于其前一个元素的索引

6. 声明数组存储值时，最大维度是多少？

- a. 10
- b. 100
- c. 3
- d. 5
- e. 没有限制

7. 使用以下声明：

```csharp
char[,] n = {{'a', 'b', 'c', 'd', 'e'}, {'f', 'g', 'h', 'i', 'j'}};
```

n[1, 1] 指的是什么？

- a. a
- b. f
- c. b
- d. g
- e. 以上都不是

8. 二维数组是一个数据项列表，这些数据项_____________。

- a. 都具有相同类型
- b. 都有不同名称
- c. 都是整数
- d. 最初都设置为 null（'\0'）
- e. 以上都不是

9. 使用以下声明：

```csharp
int[,] x = {{12, 13, 14, 15}, {16, 17, 18, 19}};
```

x[2, 4] 指的是什么？

- a. 19
- b. 18
- c. '\0'
- d. 0
- e. 以上都不是

10. 下列哪一项将 95 加到当前存储 14 的数组元素上？

```csharp
int[,] x = {{12, 13}, {14, 15}, {16, 17}, {18, 19}};
```

- a. x[2] += 95;
- b. x[1, 0] += 95;
- c. x[1, 0] += 95;
- d. x = 14 + 95;
- e. 以上都不是

11. 以下语句分配了多少个分量？

```csharp
double[,] values = new double[3, 2];
```

- a. 32
- b. 3
- c. 5
- d. 6
- e. 以上都不是

12. 给定上面第 11 题中 values 的声明，如何将 0 存储到最后一个物理位置？

- a. values = 0;
- b. values[6] = 0;
- c. values[3, 2] = 0;
- d. values[2, 1] = 0;
- e. 以上都不是

13. 如果将数组声明为 int[,] anArray = new int[5, 3];，可以用哪条语句将 anArray[2, 1] 中存储的值加倍：

- a. anArray[2, 1] = anArray[5, 1] * 2;
- b. anArray = anArray * 2;
- c. anArray[2, 1] *= anArray[2, 1] * 2;
- d. anArray[2, 1] *= 2;
- e. 以上都不是

14. 使用以下声明：

```csharp
int[,] points =
    {{300, 100, 200, 400, 600},
     {550, 700, 900, 800, 100}};
```

语句 points[1, 3] = points[1, 3] + 10; 将

- a. 将 300 替换为 310，并将 900 替换为 910
- b. 将 500 替换为 510
- c. 将 900 替换为 910
- d. 将 800 替换为 810
- e. 以上都不是

15. 使用以下声明：

```csharp
int[,] points =
    {{300, 100, 200, 400, 600},
     {550, 700, 900, 200, 100}};
```

语句 points[0, 4] = points[0, 4-2]; 将

- a. 将 400 替换为 2
- b. 将 300 和 600 替换为 2
- c. 将 600 替换为 200
- d. 导致错误
- e. 以上都不是

16. 使用以下声明：

```csharp
int[,] points =
    {{300, 100, 200, 400, 600},
     {550, 700, 900, 200, 100}};
```

语句 Console.Write(points[1, 2] + points[0, 3]); 将

- a. 显示 900400
- b. 显示 1300
- c. 显示 "points[1, 2] + points[0, 3]"
- d. 导致错误
- e. 以上都不是

17. 当将 ArrayList 中的一个元素传递给方法时，该方法接收：

- a. ArrayList 的副本
- b. ArrayList 的地址
- c. ArrayList 该元素中值的副本
- d. ArrayList 中该元素的地址
- e. 以上都不是

18. 当将整个 ArrayList 传递给方法时，该方法接收：

- a. ArrayList 的副本
- b. ArrayList 的地址
- c. ArrayList 中第一个值的副本
- d. ArrayList 中每个元素的地址
- e. 以上都不是

19. 要将字符串中的所有大写字母转换为对应的小写字母，可以使用 string 类的 ________ 方法。

- a. IsLower()
- b. ConvertLower()
- c. Lower()
- d. ToLower()
- e. 以上都不是

20. ArrayList 类中的哪个方法可用于将值放到 ArrayList 的末尾？

- a. AddLast()
- b. AddLastIndex()
- c. Add()
- d. Insert()
- e. 以上都不是

21. ArrayList 类中的哪个方法可用于获取或设置 ArrayList 可包含的元素数？

- a. Length()
- b. Size()
- c. Dimension()
- d. Rank()
- e. Capacity()

22. 哪个类包含用于创建动态一维结构的方法？

- a. Array
- b. string
- c. array
- d. ArrayList
- e. 以上都是

23. 对具有以下标头的方法进行正确的方法调用将是：

```csharp
int result(int[,] anArray, int num)
```

- a. `Console.Write(result(anArray, 3));`
- b. `result(anArray, 30);`
- c. `Console.Write(result(anArray[ , 3));`
- d. `result(anArray[ ], 30);`
- e. 以上都不是

24. 对于二维数组，`foreach` 语句的一个限制是它可以：

- a. 仅用于只读访问
- b. 仅与整型数组一起使用
- c. 不能与多维数组一起使用
- d. 仅用于小于 1000 个元素的数组
- e. 不能与动态数组一起使用

25. 为了检索存储在 Queue `class` 对象中的值，你会使用哪个方法？

- a. `Pop();`
- b. `Push();`
- c. `Dequeue();`
- d. `Enqueue();`
- e. 以上都不是

26. 使用以下 `string` 回答 a 到 e 题。

```csharp
string sValue = "Today is the first Day of "
             + "the rest of your life.";
```

- a. 创建一个新的 `string`，其中除单词 Day 外所有字符均为小写。Day 应全部大写。
- b. 创建一个包含八个元素的新 `string` 数组。sValue `string` 中的每个单词应放在单独的数组单元格中。
- c. 从步骤 b 中创建的最后一个数组元素中删除句点。显示新数组的内容以验证其已删除。
- d. 在 sValue `string` 的两端各用三个星号包围。
- e. 在 sValue `string` 中将单词 first 替换为单词 best。

27. 使用以下声明：

```csharp
int[,] anArray = {{34, 55, 67, 89, 99}, {22, 68, 11, 19, 45}};
```

下列每个输出语句的结果会是什么？

- a. `Console.WriteLine(anArray.Length);`
- b. `Console.WriteLine(anArray[1, 2]);`
- c. `Console.WriteLine(anArray[0, anArray.GetLength(0) - 2]);`
- d. `Console.WriteLine(anArray[0, 2 + 1] * anArray[0, 0]);`
- e. `Console.WriteLine(anArray.Rank);`

28. 使用以下声明，为步骤 a 到 e 编写解决方案。

```csharp
int[,] cArray = new int[2, 3];
string[,,] dArray = new string[5, 2, 6];
```

- a. 编写一个 `foreach` 循环以显示 cArray 的内容。
- b. 编写一个 `for` 循环，将 cArray 中的每个元素增加 5。
- c. 编写一个 `foreach` 循环以显示 dArray 的内容。
- d. 能否使用 `foreach` 循环将 dArray 的所有元素初始化为零？如果可以，请展示代码。如果不行，请解释原因。
- e. 编写一个 `for` 循环，将 dArray 中的所有元素初始化为零。

29. 为以下问题说明创建数组声明。

- a. 一个数组，用于保存 5 个州中最大的 3 个城市的名称。用距离你校园最近的 5 个州进行初始化。
- b. 一个单独的数组，用于保存 10 个人的姓名。你应该能够引用每个人的名字，而无需使用字符串操作方法拆分数据。
- c. 一个单独的数组，用于存储五场考试的答案键，每场考试由 15 道判断题组成。

30. 解释 .NET Hashtable 与 Dictionary 类之间的区别。

## 编程练习

1. 编写一个应用程序，创建并返回一个包含二维数组中所有元素的一维数组。按行主序格式存储这些值。为便于测试，可以对一个 6 x 3 的二维数组进行编译时初始化。显示该二维数组和一维数组。
