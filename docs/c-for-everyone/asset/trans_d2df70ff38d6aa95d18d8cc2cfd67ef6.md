

而

11  1  4  9  16  9  7  4  9

会被视为相同，但

1  4  9  16  9  7  4  9  11

和

11  11  7  9  16  4  1  4  9

则不会。你可能需要一个或多个辅助函数。

**P6.12** 编写一个从数组中删除重复项的函数。例如，如果用包含

`1  4  9  16  9  7  4  9  11`

的数组调用 `remove_duplicates`，那么该数组会变为

`1  4  9  16  7  11`

你的函数应有一个用于数组大小的引用参数，该参数在删除重复项时更新。

**P6.13** *连续段* 是相邻重复值的一个序列。编写一个程序，生成 20 次随机掷骰子的序列并打印这些骰子值，通过将连续段括在括号中来标记它们，如下所示：

`1 2 (5 5) 3 1 2 4 3 (2 2 2 2) 3 6 (5 5) 6 3 1`

使用以下伪代码：

```text
Set a Boolean variable in_run to false.
For each valid index i in the array
    If in_run
        If values[i] is different from the preceding value
            Print ).
            in_run = false
    If not in_run
        If values[i] is the same as the following value
            Print (.
            in_run = true
    Print values[i].
If in_run, print ).
```

**P6.14** 编写一个程序，生成 20 次随机掷骰子的序列，并打印这些骰子值，只标记最长的连续段，如下所示：

`1 2 5 5 3 1 2 4 3 (2 2 2 2) 3 6 5 5 6 3 1`

如果有多个长度最大的连续段，则标记第一个。

**P6.15** 编写一个程序，生成 20 个介于 0 和 99 之间的随机值序列，打印该序列，对其进行排序，并打印排序后的序列。使用标准 C++ 库中的 sort 函数。

**P6.16** 编写一个程序，生成数字 1 到 10 的十个随机排列。要生成一个随机排列，你需要用数字 1 到 10 填充一个数组，使得没有两个元素具有相同的内容。你可以通过暴力方法来实现，通过

然后编写一个程序，读取一百个地形高度值，并显示当地形从最低点到最高点分十步增加水位时，地形如何被淹没。

**工程题 P6.34** 修改本书配套代码中的 ch06/image.cpp 程序，以生成正弦波的图像。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_329_0.png)

每五度绘制一行像素。

**工程题 P6.35** 修改 ch06/animation.cpp 程序，以显示动画正弦波。在第 *i* 帧中，将正弦波平移 5 × *i* 度。

**工程题 P6.36** 编写一个程序，为一个质量为 *m* 且连接在振荡弹簧上的物体运动建模。当弹簧从其平衡位置位移 *x* 时，胡克定律指出恢复力为

$$F = -kx$$

其中 *k* 是取决于弹簧的常数。（本模拟使用 10 N/m。）

![](img/5e58fb4c840712efd6ed6fa82bb97f57_329_1.png)

从给定的位移 *x* 开始（例如 0.5 米）。将初始速度 *v* 设为 0。根据牛顿定律（*F = ma*）和胡克定律，使用质量 1 kg 计算加速度 *a*。使用小时间间隔 Δ*t* = 0.01 秒。更新速度——它变化 *a*Δ*t*。更新位移——它变化 *v*Δ*t*。

每十次迭代，将弹簧位移绘制为条形，其中 1 像素表示 1 厘米。修改 ch06/image.cpp 程序以创建图像。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_329_2.png)

## 自测题答案

1. `int primes[] = { 2, 3, 5, 7, 11 };`

2. `2, 3, 5, 3, 2`

3. `3, 4, 6, 8, 12`

4. `values[0] = 0;`  
   `values[CAPACITY - 1] = 0;`

5.
```cpp
for (int i = SIZE - 1; i >= 0; i--)
{
    cout << values[i] << endl;
}
```

6. `string words[10];`

7. `string words[] = { "Yes", "No" };`

8.
```text
20 <= largest value
10
20 <= largest value
```

9.
```cpp
int count = 0;
for (int i = 0; i < size; i++)
{
    if (values[i] == 0)
    {
        count++;
    }
}
```

10. 如果 values 的所有元素都是负数，那么结果会被错误地计算为 0。

11.
```cpp
for (int i = 0; i < size; i++)
{
    cout << values[i];
    if (i < size - 1)
    {
        cout << " | ";
    }
}
```

现在你知道为什么我们以另一种方式设置循环了。

12. 如果序列没有元素，那么会打印一个随机值。

13. 如果存在匹配，那么 pos 会在循环退出前递增。

14. 这个循环将所有元素设置为 values[pos]。

15. sum 函数会将 values 数组中的所有数字以及接下来的 900 个数字相加，产生一个随机结果。（实际上，程序可能没有权限访问所有这些数字，在这种情况下操作系统会终止它。）

16.
```cpp
int numbers[5];
squares(5, numbers);
```

17.
```cpp
int find_first(double values[], int size, double searched_value)
{
    for (int pos = 0; pos < size; pos++)
    {
        if (values[pos] == searched_value)
        {
            return pos;
        }
    }
    return -1;
}
```

注意，这个循环比第 6.2.6 节中的循环更简单，因为当找到匹配时我们可以直接返回位置。

18.
```cpp
void read_inputs(double inputs[], int capacity, int& size)
{
    size = 0;
    double input;
    while (cin >> input)
    {
        if (size < capacity)
        {
            inputs[size] = input;
            size++;
        }
    }
}
```

19.
```cpp
int append(double first[], int first_size,
           double second[], int second_size,
           double target[], int target_capacity)
```

注意以下事项：

- 你必须传入第一个和第二个数组的大小，以便函数知道要复制多少个元素。
- 你必须传入目标数组的容量，以便函数不会写到末尾之后。
- 目标数组是一个参数变量——函数不能返回数组。
- 返回类型是 int，以便函数可以返回目标数组的大小。（或者，你可以使用引用参数 `int& target_size`。）

20. 使用第一个算法。在计算和时，元素的顺序无关紧要。

21.
- 找到最小值。
- 计算总和。
- 减去最小值。

22. 使用计数匹配的算法（第 4.7.2 节）两次，一次用于计数正值，一次用于计数负值。

23. 你需要修改第 6.2.5 节中的算法。

```cpp
bool first = true;
for (int i = 0; i < size of values; i++)
{
    if (values[i] > 0)
    {
        if (first) { first = false; }
        else { cout << ", "; }
    }
    cout << values[i];
}
```

注意，你不能再使用 `i > 0` 作为打印分隔符的条件。

24. 使用算法将所有正值收集到一个数组中，然后使用第 6.2.5 节中的算法打印匹配数组。

![](img/5e58fb4c840712efd6ed6fa82bb97f57_336_0.png)

**图 1** 内存中的指针和值

类型 `double*`，即“指向 double 的指针”，表示一个 double 变量的位置。`&` 运算符，也称为地址运算符，产生一个变量的位置。取一个 double 变量的地址会产生一个 `double*` 类型的值。

类型 `T*` 表示一个指向 `T` 类型变量的指针。

思考指针可能相当抽象，但你可以使用一个简单的技巧使它更具体。计算机程序中的每个变量都位于特定的内存位置。你不知道每个变量存储在哪里，但你可以假装知道。让我们假设我们知道 `harrys_account` 存储在位置 20300。（这只是一个编造的值。）如图 1 所示，`harrys_account` 的值是 0，但 `&harrys_account` 的值是 20300。`account_pointer` 的值也是 20300。在我们的图中，我们将从指针到位置画一个箭头，但当然计算机不存储箭头，只存储数字。

`&` 运算符产生一个变量的位置。

通过使用指针，你可以随时切换到不同的账户。要访问不同的账户，只需更改指针值：

```cpp
account_pointer = &joint_account;
```

## 7.1.2 通过指针访问变量

当你有一个指针时，你会想要访问它所指向的变量。`*` 运算符用于读取或更新指针所指向的变量。当与指针一起使用时，`*` 运算符与乘法无关。在 C++ 标准中，这个运算符称为间接运算符，但它通常也称为解引用运算符。

`*` 运算符访问指针所指向的变量。

这条语句向 `account_pointer` 所指向的账户进行初始存款（见图 2）：

```cpp
*account_pointer = 1000;
```

换句话说，你可以完全像使用 `harrys_account` 或 `joint_account` 一样使用 `*account_pointer`。使用哪个账户取决于指针的值。当程序执行这条语句时，它会获取存储在 `account_pointer` 中的地址。然后它使用该地址处的变量，如图 2 所示。

