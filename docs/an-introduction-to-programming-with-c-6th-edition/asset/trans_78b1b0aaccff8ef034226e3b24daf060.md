

# 总结

你标题栏中的文本将会有不同

```
Next price: Next price: Next price: Next price: Next price:
Next price: Next price: Next price: Next price: Next price: Next pr
Next price: Next price: Next price: Next price: Next price: Next pr
Next price: Next price: Next price: Next price: Next price: Next pr
Next price: Next price: Next price: Next price: Next price: Next pr
Next price: Next price: Next price: Next price: Next price: Next pr
Next price: Next price: Next price: Next price: Next price: Next pr
Next price: Next price: Next price: Next price: Next price: Next pr
Next price: Next price: Next price: Next price: Next price: Next pr
Next price: Next price: Next price: Next price: Next price: Next pr
Next price: Next price: Next price: Next price: Next price: Next pr
Next price: Next price: Next price: Next price: Next price: Next pr
Next price: Next price: Next price: Next price: Next price: Next pr
Next price: Next price: Next price: Next price: Next price: Next price
Next price: Next price: Next price: Next price: Next price: Next price:
```

249

图 7-50 显示程序处于死循环的命令行窗口

# 总结

- 当你需要计算机在循环条件为真（或直到满足退出条件）时处理一个或多个程序指令时，请使用重复结构，它也称为循环。

- 重复结构可以是预测试循环，也可以是后测试循环。在预测试循环中，在处理循环内的指令之前会先评估循环条件。在后测试循环中，评估发生在循环内指令处理之后。在这两种类型的循环中，预测试循环最常用。

- 条件出现在预测试循环的开头，决定了是否处理循环内的指令（称为循环体）。循环条件必须产生“真”或“假”的结果。当条件为真时，将执行循环体中列出的指令；否则，将跳过循环体。

- 一些循环需要用户输入特殊值（如哨兵值）来结束循环。你应该使用易于与程序识别的有效数据区分的哨兵值。其他循环则通过使用计数器来终止。

- 出现在预测试循环条件之前的输入指令被称为“引导读取”（priming read），因为它被用于引导（准备或设置）循环。该读取只从用户处获取第一个值。出现在循环内的输入获取剩余值（如果有），并在末尾进行更新。

- 在流程图中，用菱形表示重复结构的条件。该菱形被称为决策符号。

- 计数器和累加器在重复结构内部用于计算小计、总和和平均值。所有的计数器和累加器都必须初始化并更新。计数器通过常值更新，而累加器通过变化的金额进行更新。

# 第 7 章 重复结构

- 许多程序员使用六边形表示 `for` 语句中的 `for` 子。

- 你可以使用 `while` 语句或 `for` 语句在 C++ 中编写预测试循环。

# 关键术语

**累加器 (Accumulator)**——用于累加（相加）某些数值的数值变量

**计数器 (Counter)**——用于计算某些数量的数值变量

**计数器控制循环 (Counter-controlled loops)**——由计数器变量控制处理和终止的循环

**死循环 (Endless loop)**——指令被无限处理的循环；也称为无限循环

**递增 (Incrementing)**——更新的另一种别名

**无限循环 (Infinite loop)**——死循环的另一种别名

**初始化 (Initializing)**——向内存位置（如计数器或累加器变量）分配初始值的过程

**循环 (Loop)**——重复循环的另一种别名

**循环体 (Loop body)**——循环内的指令

**循环退出条件 (Loop exit condition)**——计算机停止循环体指令必须满足的条件

**循环条件 (Looping condition)**——计算机继续执行循环体指令必须满足的条件

**后测试循环 (Posttest loop)**——条件在处理循环体指令后进行评估的循环

**预测试循环 (Pretest loop)**——条件在处理循环体指令之前进行评估的循环

**引导读取 (Priming read)**——出现在循环上方的输入指令；用于从用户处获取第一个项目

**重复结构 (Repetition structure)**——用于重复处理一个或多个程序指令的控制结构；也称为循环

**哨兵值 (Sentinel values)**——用于结束循环的值；也称为触发值或尾部值

**更新读取 (Update read)**——出现在循环内并与引导读取相关的输入指令

**更新 (Updating)**——向计数器或累加器变量中存储的值加上一个数字的过程；也称为递增

# 复习题

参考图 7-51 回答复习题 1 至 4。

![](img/d64a28a68f49d61137bf2f3170ac40ad_271_0.png)

- 1. 图 7-51 中的流程图 A 使用了哪些控制结构？（选择所有适用项。）
  a. 顺序
  b. 选择
  c. 重复

- 2. 图 7-51 中的流程图 B 使用了哪些控制结构？（选择所有适用项。）
  a. 顺序
  b. 选择
  c. 重复

# 第 7 章 重复结构

- 3. 图 7-51 中的流程图 C 使用了哪些控制结构？
  a. 顺序
  b. 选择
  c. 重复

- 4. 图 7-51 中的流程图 D 使用了哪些控制结构？
  a. 顺序
  b. 选择
  c. 重复

- 5. 哪一个 `while` 子句在年龄小于 0 时告诉计算机退出循环？
  a. while (age < 0)
  b. while (age >= 0)
  c. while (age != 0)
  d. while (age >= 0)

- 6. 哪一个是允许输入年龄的良好哨兵值？
  a. -4
  b. 350
  c. 999
  d. 以上所有

- 7. 用于结束循环的值被称为 ________ 值。
  a. 关闭
  b. 结束
  c. 哨兵
  d. 停止

- 8. 允许用户输入一个或多个数字的输入指令只获取第一个数字并被称为 ________。
  a. 进入
  b. 初始化
  c. 
  d. 引导

- 9. 下列代码将执行 `cout << numTimes << endl;` 语句多少次？

```
int numTimes = 0;
while (numTimes > 3)
{
    cout << numTimes << endl;
    numTimes = numTimes + 1;
}
```

- a. 0
  b. 1
  c. 3
  d. 4

- 10. 下列代码将执行 `cout << numTimes << endl;` 语句多少次？

```
for (int numTimes = 1; numTimes < 6; numTimes = numTimes + 1)
    cout << numTimes << endl;
```

- a. 0
  b. 1
  c. 5
  d. 6

- 11. 复习题 10 中 `numTimes` 变量的什么值停止循环？
  a. 1
  b. 5
  c. 6
  d. 7

- 12. 下列代码将执行 `cout << numTimes << endl;` 语句多少次？

```
for (int numTimes = 4; numTimes <= 10; numTimes += 2)
    cout << numTimes << endl;
```

- a. 0
  b. 3
  c. 4
  d. 12

- 复习题 12 中 `numTimes` 变量的什么值停止循环？
  a. 4
  b. 6
  c. 10
  d. 12

- 下列哪项通过 `sales` 变量的值更新 `total` 累加器？
  a. total = total + sales;
  b. total = sales + total;
  c. total += sales
  d. 以上所有

- 哪个语句可以编写执行 10 次的循环？
  a. for
  b. repeat
  c. while
  d. a 或 c

# 练习题

# 纸笔练习

- 1. 为图 7-52 中的代码完成一个跟踪表。代码在计算机屏幕上显示什么？`temp` 变量的什么值停止循环？（TRY THIS 练习题的答案位于章节末尾。）

```
int temp = 0;
while (temp < 5)
{
  cout << temp << endl;
  temp = temp + 1;
} //end while
```

图 7-52

- 2. 为图 7-53 中的代码完成一个跟踪表。代码在计算机屏幕上显示什么？`num` 变量的什么值停止循环？（TRY THIS 练习题的答案位于章节末尾。）

