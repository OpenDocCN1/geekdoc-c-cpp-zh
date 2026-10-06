

```c
double[] total = { 0, 0, 0, 0 };
private void OkButton_Click(object sender, EventArgs e) {
    int dept;
    double contribution;
    dept = Convert.ToInt32(deptTextBox.Text);
    contribution = Convert.ToDouble(contributionTextBox.Text);
    --dept;
    total[dept] += contribution;
    deptTextBox.Text = "";
    contributionTextBox.Text = "";
}
private void DoneButton_Click(object sender, EventArgs e) {
    outputLabel.Text = "Dept Total";
    for (int x = 0; x < total.Length; x++) {
        outputLabel.Text += String.Format("\n{0}: {1}", x + 1, total[x].ToString("C"));
    }
}
```

**图 6-24** 用于 CountContributions 所需的数组声明和两个方法的代码

## 两真一假

## GUI 程序中的数组问题

- 1. 一个 GUI 程序可以包含任意数量、任意数据类型的数组声明。
- 2. 如果一个方法响应用户发起的事件，它就不能包含数组声明。
- 3. 如果一个方法响应用户发起的事件，且该方法包含数组声明，则该数组会在每次事件发生时被重新声明。

> 错误语句是 #2。如果一个方法响应用户发起的事件，它不能存储必须跨越多次事件的数据。唯一的问题是数组会在每次新事件时被重新声明。

## 章节总结

- 数组是数据项列表，所有项都具有相同的类型和相同的名称，但通过下标或索引相互区分。你通过在类型后插入一对方括号来声明数组变量，并使用关键字 **new** 为数组预留内存。任何数组元素的编号都从 0 到数组长度减 1。在 **C#** 中，数组是派自类 **System.Array** 的对象。数组元素被初始化为默认值。要初始化非默认值，你使用用逗号分隔并包含在大括号内的值列表。

- 当使用变量处理数组元素时，数组最强大。任何数组元素的下标必须保持在 0 到 **Length** - 1 的范围内。**Length** 属性自动持有数组的长度。你可以使用 **foreach** 语句循环遍历每个数组元素，而无需使用下标。

- 当你想确定一个变量是否持有多个可能值之一时，可以将该变量与数组中的值列表进行比较。你可以设置一个并行数组来访问额外信息。

- **BinarySearch()** 方法在排序数组中查找请求的值。如果在数组中未找到该值，该方法返回 -1；否则，它返回目标值的位置。**Sort()** 方法将数组按升序排列。**Reverse()** 反转数组中项的顺序。

- C# 支持多维数组，它需要多个下标来访问数组元素。最常用的多维数组是矩形的二维数组。二维数组的每行都有两个或多个列值。在矩形数组中，每行的列数相同。C# 还支持交数组（jagged arrays），即数组的数组。

- 在 GUI 程序中使用数组时最不寻常的是，如果数组值根据用户输入而变化，则数组必须存储在任何响应用户事件的方法之外。

## 关键术语

**数组**（array）是一个具有相同数据类型和相同名称的数据项列表，通过下标或索引相互区分。

**数组元素**（array element）是数组中的单个对象。

**下标**（subscript，也称为**索引** index）是包含在方括号内的整数，指示数组元素的位置。

**初始化列表**（initializer list）是为数组提供的值列表。

**只读**（Read-only）描述可以访问但不能更改的值。

**迭代变量**（iteration variable）是 foreach 语句中用于轮流持有每个数组值的临时位置。

**顺序搜索**（sequential search）通过按顺序检查列表来进行。

**并行数组**（parallel array）与另一个数组具有相同数量的元素和对应的数据。

**范围匹配**（range match）确定值落入的限制值之间的值对。

**二分查找**（binary search）是一种通过反复对分排序后的对象列表来在列表中查找项的算法，直到搜索接近匹配项。

**一维数组**（one-dimensional or single-dimensional array）你可以使用单个下标访问元素的数组。

**多维数组**（Multidimensional arrays）需要多个下标来访问数组元素。

**二维数组**的每行都有两个或多个列值。

**矩形数组**（rectangular array）是每行列数相同的数组。

**交数组**（jagged array）是一个每个元素都是另一个数组的一维数组。

## 复习题

- 1. 在数组中，每个元素都有相同的
  a. 下标
  c. 数据类型
  b. 内存位置
  d. 以上所有

- 2. 用于创建对象的运算符是
  a. =
  c. new
  b. +=
  d. create

- 3. 下列哪项正确声明了一个六个整数的数组？
  a. int array[6];
  c. int[6] array;
  b. int[] array = 6;
  d. int[] array = new int[6];

- 4. 数组名称方括号内的值是
  a. 始终是常量
  c. 称为下标
  b. 始终是双精度浮点数
  d. 以上都是

- 5. 如果定义了一个包含10个元素的数组，那么使用的最高下标是
  a. 8	c. 10
  b. 9	d. 11

- 6. 在 C# 中初始化数组
  a. 可选的 c. 困难的
  b. 强制的 d. 禁止

- 7. 当声明一个六个元素的数组但未提供初始化值时，第一个元素的值是
  a. 0.0	c. 5.0
  b. 1.0	d. 未知

- 8. 下列哪项正确声明了四个整数数组？
  a. int[] ages = new int[4]{20, 30, 40, 50};
  b. int[] ages = new int[] {20, 30, 40, 50};
  c. int[] ages = {20, 30, 40, 50};
  d. 以上所有

- 9. 当 数组使用 {20, 30, 40, 50} 正确初始化时，ages[1] 的值是
  a. 0	c. 30
  b. 20	d. 未知

- 10. 当 数组使用 {20, 30, 40, 50} 正确初始化时，ages[4] 的值是
  a. 0	c. 50
  b. 4	d. 未知

- 11. 当你声明 int[] temperature = {0, 2, 5, 9, 1, 4}; 时，temperature.length 的值是
  a. 5	c. 7
  b. 6	d. 未知

- 12. 下列哪项将名为 amount 的10个元素整数数组中的每个值翻倍？
  a. for(int x = 9; x >= 0; x--) amount[x] *= 2;
  b. foreach(int number in amount) number *= 2;
  c. 以上都是 d. 都不是

- 13. 下列哪项为16个元素的数组加10？
  a. for(int sub = 0; sub < 16; sub++) points[sub] += 10;
  b. foreach(int sub in points) sub += 10;
  c. 以上都是 d. 都不是

- 14. 在对应位置存储相关信息的数组。
  a. 交数组 c. 并行数组 b. 矩形

- 15. 假设数组定义为 int[] nums = {2, 3, 4, 5}; 下哪项会反向显示数组？
  a. for(int x = 4; x > 0; x--) Write(nums[x]);
  b. for(int x = 3; x >= 0; x--) Write(nums[x]);
  c. for(int x = 3; x > 0; x--) Write(nums[x]);
  d. for(int x = 4; x >= 0; x--) Write(nums[x]);

- 16. 假设数组定义为 int[] nums = {7, 15, 23, 5, 5}; 下哪项将数组中的值按降序排列？
  a. Array.Sort(nums);
  b. Array.Reverse(nums);
  c. Array.Sort(nums); Array.Reverse(nums);
  d. 以上都是

- 17. BinarySearch() 和 Sort() 方法具有哪些共同点？
  a. 两个方法都接受一个必须是数组的参数。
  b. 它们都对数值数据组成的数组操作。
  c. 每个方法使用的数组必须从升序开始。
  d. 两个方法都属于 System.Array 类。

- 18. 如果你使用 BinarySearch() 方法且在数组中未找到查找的对象，
  a. 显示错误消息
  b. 返回零
  c. 返回值 false
  d. 返回负值

- 19. BinarySearch() 方法在什么情况下是不适用的？
  a. 数组项按升序排列
  b. 数组包含重复值且你想找到所有值
  c. 你想找到某个值的精确匹配
  d. 数组项不是数值型

- 20. 下列哪项声明了一个包含八行五列的整数数组？
  a. int[8, 5] num = new int[,];
  b. int[8][5] num = new int[];
  c. int[ , ] num = new int[5, 8];
  d. int[ , ] num = new int[8, 5];

## 练习

## 编程练习

对于以下每个练习，你可以选择编写基于控制台或GUI的应用程序，或者两者都写。

- 1. 写一个名为 ArrayDemo 的程序，存储一个包含10个整数的数组。在用户输入哨兵值之前，允许用户有四个选项：(1) 从存储数组的第一个位置到最后一个位置顺序查看列表，(2) 从最后一个位置到第一个位置顺序查看列表，(3) 选择特定位置查看，或 (4) 退出应用程序。

