

```
int mat[5][10];
...
fun(mat);
...
}
```

这种以参数形式传递矩阵的方法存在一个问题：它不允许程序员编写一个可以接受列数不同的矩阵的函数；对于每一个列数不同的矩阵，都必须编写一个新的函数。实际上，这就禁止了编写灵活的函数，而这些函数如果处理多维数组本可以有效地重用。在 C 和 C++ 中，由于包含指针算术，问题是可以绕过的。矩阵可以作为指针传递，并且矩阵的实际维度也可以作为参数传递。然后，函数就可以在每次需要引用矩阵元素时，使用指针算术来评估用户编写的存储映射函数。例如，考虑以下函数原型：

```
void fun(float *mat_ptr,
    int num_rows,
    int num_cols);
```

以下语句可用于将变量 x 的值移动到 fun 中参数矩阵的 [row][col] 元素：

```
*(mat_ptr + (row * num_cols) + col) = x;
```

虽然这可行，但显然难以阅读，并且由于其复杂性，容易出错。可以通过使用宏来定义存储映射函数来缓解阅读上的困难，例如

```
#define mat_ptr(r,c) (*(mat_ptr + ((r) * (num_cols) + (c))))
```

有了它，赋值可以写成

```
mat_ptr(row,col) = x;
```

其他语言采用不同的方法来处理传递多维数组的问题。

在 Java 和 C# 中，数组是对象。它们都是单维的，但元素可以是数组。每个数组都继承一个命名常量（Java 中的 length 和 C# 中的 Length），该常量在数组对象创建时设置为数组的长度。矩阵的形参使用两组空括号出现，如以下 Java 方法所示：

```
float sumer(float mat[][]) {
    float sum = 0.0f;
    for (int row = 0; row < mat.length; row++) {
        for (int col = 0; col < mat[row].length; col++) {
            sum += mat[row][col];
        } //** for (int col ...
    } //** for (int row ...
    return sum;
}
```

由于每个数组都有自己的长度值，在矩阵中，行可以具有不同的长度。

### 9.5.7 设计考虑

选择参数传递方法时涉及两个重要考虑：效率以及是否需要单向或双向数据传输。

当代软件工程原则规定，应尽量减少子程序代码对子程序外部数据的访问。秉持这一目标，当不需要通过参数向调用者返回数据时，应使用 in-mode 参数。当没有数据传输到被调用子程序，但子程序必须向调用者传回数据时，应使用 out-mode 参数。最后，仅当数据必须在调用者和被调用子程序之间双向移动时，才应使用 inout-mode 参数。

存在一个与此原则相冲突的实际考虑。有时，为单向参数传输传递访问路径是合理的。例如，当一个大型数组要传递给不修改它的子程序时，可能更喜欢单向方法。然而，按值传递将要求将整个数组移动到子程序的局部存储区。这在时间和空间上都是昂贵的。正因如此，大型数组通常按引用传递。这正是 Ada 83 定义允许实现者在结构化参数的两种方法之间选择的原因。C++ 常量引用参数提供了另一种解决方案。另一种替代方法是将选择权留给用户。

函数的参数传递方法的选择与另一个设计问题相关：函数副作用。该问题在第 9.10 节中讨论。

### 9.5.8 参数传递示例

考虑以下 C 函数：

```
void swap1(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
}
```

假设此函数以

```
swap1(c, d);
```

调用。回想一下，C 使用按值传递。swap1 的行为可以用以下伪代码描述：

```
a = c      - Move first parameter value in
b = d      - Move second parameter value in
temp = a
a = b
b = temp
```

尽管 a 最终具有 d 的值，b 最终具有 c 的值，但 c 和 d 的值保持不变，因为没有向调用者传回任何内容。

我们可以修改 C 的 swap 函数以处理指针参数，从而实现按引用的效果：

```
void swap2(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
```

swap2 可以用

```
swap2(&c, &d);
```

调用。swap2 的行为可以用以下描述：

```
a = &c      - Move first parameter address in
b = &d      - Move second parameter address in
temp = *a
*a = *b
*b = temp
```

在这种情况下，交换操作是成功的：c 和 d 的值确实被互换。swap2 可以使用 C++ 的引用参数写成如下形式：

```
void swap2(int &a, int &b) {
    int temp = a;
    a = b;
    b = temp;
}
```

这种简单的交换操作在 Java 中是不可能的，因为它既没有指针，也没有 C++ 那种引用。在 Java 中，引用变量只能指向对象，而不能指向标量值。

按值结果传递的语义与按引用传递的语义相同，只是当涉及别名时除外。Ada 对 inout-mode 标量参数使用按值结果传递。为了探索按值结果传递，考虑以下函数 swap3，我们假设它使用按值结果参数。它以类似于 Ada 的语法编写。

```
procedure swap3(a : in out Integer, b : in out Integer) is
    temp : Integer;
    begin temp := a;
    a := b;
    b := temp;
    end swap3;
```

假设 swap3 以

```
swap3(c, d);
```

调用。swap3 在此调用下的行为为

```
addr_c = &c          - Move first parameter address in
addr_d = &d          - Move second parameter address in
a = *addr_c          - Move first parameter value in
b = *addr_d          - Move second parameter value in
temp = a
a = b
b = temp
*addr_c = a          - Move first parameter value out
*addr_d = b          - Move second parameter value out
```

因此，这个交换子程序再次运行正确。接下来，考虑调用

```
swap3(i, list[i]);
```

在这种情况下，行为为

```
addr_i = &i           - Move first parameter address in
addr_listi= &list[i]   - Move second parameter address in
a = *addr_i            - Move first parameter value in
b = *addr_listi        - Move second parameter value in
temp = a
a = b
b = temp
*addr_i = a            - Move first parameter value out
*addr_listi = b        - Move second parameter value out
```

再次，子程序运行正确，在这种情况下是因为要返回参数值的地址是在调用时计算的，而不是在返回时计算的。如果在返回时计算实际参数的地址，结果就会错误。

最后，我们必须探讨当别名涉及按值结果传递和按引用传递时会发生什么。考虑以下用 C 风格语法编写的骨架程序：

```
int i = 3; /* i is a global variable */
void fun(int a, int b) {
    i = b;
}
void main() {
    int list[10];
    list[i] = 5;
    fun(i, list[i]);
}
```

在 fun 中，如果使用按引用传递，i 和 a 是别名。如果使用按值结果传递，i 和 a 不是别名。fun 的行为，假设使用按值结果传递，如下所示：

```
addr_i = &i          - Move first parameter address in
addr_listi = &list[i] - Move second parameter address in
a = *addr_i          - Move first parameter value in
b = *addr_listi      - Move second parameter value in
i = b                - Sets i to 5
*addr_i = a          - Move first parameter value out
*addr_listi = b      - Move second parameter value out
```

在这种情况下，对 fun 中的全局 i 的赋值将其值从 3 改为 5，但第一个形式参数的回写（示例中倒数第二行）将其改回 3。这里的重要观察是，如果使用按引用传递，结果是回写不是语义的一部分，i 保持为 5。另请注意，由于第二个参数的地址是在 fun 开始时计算的，对全局 i 的任何更改都不会影响在结束时用于返回 list[i] 的值所使用的地址。

### 9.6 参数为子程序

在编程中，出现许多情况，如果子程序名可以作为参数发送给其他子程序，则最方便处理。其中一个常见例子是当子程序必须采样某个数学函数时。例如，执行数值积分的子程序通过在多个不同点采样函数来估计函数图像下的面积。当编写此类子程序时，它应可用于任何给定的函数；它不需要为每个必须积分的函数重写。因此，自然地，要被积分的数学函数的求值程序函数的名称应作为参数发送给积分子程序。

