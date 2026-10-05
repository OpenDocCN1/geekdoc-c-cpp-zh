

## 第 5 章 数组

显示 5.10 二维数组 grade

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_253_0.png)

| | grade [0] [0] | grade [0] [1] | grade [0] [2] |
|---|---|---|---|
| student 1 | | | | |
| student 2 | grade [1] [0] | grade [1] [1] | grade [1] [2] |
| student 3 | grade [2] [0] | grade [2] [1] | grade [2] [2] |
| student 4 | grade [3] [0] | grade [3] [1] | grade [3] [2] |

grade [3] [0] 是学生 4 在测验 1 中得到的成绩。grade [3] [1] 是学生 4 在测验 2 中得到的成绩。grade [3] [2] 是学生 4 在测验 3 中得到的成绩。

显示 5.11 二维数组 grade

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_253_1.png)

| | 10 | 10 | 10 | | |
|---|---|---|---|---|---|
| student 1 | | | | stAve [0] |
| student 2 | 2 | 0 | 1 | 1.0 stAve [1] |
| student 3 | 8 | 6 | 9 | 7.7 stAve [2] |
| student 4 | 8 | 4 | 10 | 7.3 stAve [3] |

quizAve 7.0 5.0 7.5

## 自测练习

20. 下面代码的输出是什么？

```
int myArray[4], index1, index2;
for (index1 = 0; index1 < 4; index1++)
  for (index2 = 0; index2 < 4; index2++)
    myArray[index1][index2] = index2;
for (index1 = 0; index1 < 4; index1++)
  for (index2 = 0; index2 < 4; index2++)
    cout << myArray[index1][index2] << " ";
  cout << endl;
```

21. 编写代码，用键盘输入的数字填充一个已声明的数组 `a`。数字每行输入五个，共四行（尽管你的解决方案不需要依赖于输入数字如何分行）。

```
int a[4][5];
```

22. 为一个名为 `echo` 的 `void` 函数编写函数定义，使得以下调用能够回显自测练习 21 中描述的输入，并按照我们指定的输入格式进行回显（即每行五个数字，共四行）：

```
echo(a, 4);
```

## 本章总结

- 数组可以用于存储和处理一组类型相同的数据。
- 数组的索引变量可以像任何其他基础类型的变量一样使用。
- `for` 循环是遍历数组元素并对每个索引变量执行某些操作的好方法。
- 使用数组时最常见的编程错误是尝试访问不存在的数组索引。始终检查操作数组的循环的第一次和最后一次迭代，以确保不会使用非法过小或过大的索引。
- 数组形式参数既不是值传递参数，也不是引用传递参数，而是一种新的类型。

