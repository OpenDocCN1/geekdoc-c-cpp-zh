
这个伪代码可以写成如下 C++ 形式：

```cpp
if (studentGrade >= 90) {
    cout << "A";
}
else {
    if (studentGrade >= 80) {
        cout << "B";
    }
    else {
        if (studentGrade >= 70) {
            cout << "C";
        }
        else {
            if (studentGrade >= 60) {
                cout << "D";
            }
            else {
                cout << "F";
            }
        }
    }
}
```

如果变量 `studentGrade` 大于或等于 90，嵌套 if...else 语句中的前四个条件都将为真，但只有第一个 if...else 语句的 if 部分中的语句会执行。该语句执行后，“最外层” if...else 语句的 else 部分会被跳过。在嵌套 if...else 语句中，要确保测试所有可能的情况。

前面的嵌套 if...else 语句也可以写成以下形式，二者功能相同，但使用的花括号更少，空格和缩进也更少：

```cpp
if (studentGrade >= 90) {
    cout << "A";
}
else if (studentGrade >= 80) {
    cout << "B";
}
else if (studentGrade >= 70) {
    cout << "C";
}
else if (studentGrade >= 60) {
    cout << "D";
}
else {
    cout << "F";
}
```

这种形式避免了代码向右深度缩进，而深度缩进有时会迫使行换行。在本书中，我们将控制语句体括在花括号（{ 和 }）中，从而避免称为“悬垂 else”问题的逻辑错误。我们将在练习 3.13–3.15 中研究此问题。

### 3.6.2 块

if 语句的主体只期望包含一条语句。要在 if 或 else 的主体中包含多条语句，请用花括号将这些语句括起来。始终使用花括号是一种好习惯。一对花括号中的语句（例如控制语句或函数的主体）构成一个块。块可以放在函数中任何可以放置单条语句的位置。

下面的示例在 if...else 语句的 else 部分包含一个由多条语句组成的块：

```cpp
if (studentGrade >= 60) {
    cout << "Passed";
}
else {
    cout << "Failed\n";
    cout << "You must retake this course.";
}
```

如果 studentGrade 小于 60，程序将执行 else 主体中的两条语句并打印

```text
Failed
You must retake this course.
```

如果没有包围 else 子句中两条语句的花括号，那么语句

```cpp
cout << "You must retake this course.";
```

将位于 if...else 语句 else 部分的主体之外，并且无论 studentGrade 是否小于 60 都会执行——这是一个逻辑错误。

### 语法错误和逻辑错误

编译器会捕获语法错误，例如程序漏掉了块中的一个花括号。逻辑错误（例如计算不正确）会在执行时产生影响。致命逻辑错误会导致程序失败并提前终止。非致命逻辑错误允许程序继续执行，但会导致程序产生不正确的结果。

### 空语句

正如块可以放在任何可以放置单条语句的位置一样，也可以有空语句，它就是在通常应放置语句的位置只写一个分号（;）。空语句不起任何作用。

在 if 或 if...else 语句中，将分号放在带括号的条件之后，会在单分支 if 语句中导致逻辑错误，并在双分支 if...else 语句中导致语法错误（当 if 部分包含主体语句时）。

### 3.6.3 条件运算符 (?:)

C++ 提供了条件运算符（?:），可用于代替 if...else 语句。这可以使代码更短、更清晰。条件运算符是 C++ 中唯一的三元运算符（即接受三个操作数的运算符）。操作数与 ?: 符号一起构成条件表达式。例如，下面的语句打印条件表达式的值：

```cpp
cout << (studentGrade >= 60 ? "Passed" : "Failed");
```

? 左侧的操作数是条件。第二个操作数（位于 ? 和 : 之间）是条件为真时条件表达式的值。: 右侧的操作数是条件为假时条件表达式的值。此语句中的条件表达式在条件

```text
studentGrade >= 60
```

为真时求值为字符串 "Passed"，在条件为假时求值为字符串 "Failed"。因此，这条使用条件运算符的语句所执行的功能，与 3.6 节中的第一个 if...else 语句基本相同。条件运算符的优先级较低，因此整个条件表达式通常放在括号中。

### 检查点

- **1. (伪代码)** 编写一个伪代码 if...else 语句，判断 counter 是否大于 10。如果是，该语句应打印“counter is greater than 10.”。否则，应打印“counter is less than or equal to 10.”

**答案：**

```text
if counter is greater than 10
    print “counter is greater than 10.”
else
    print “counter is less than or equal to 10.”
```

- **2. (代码)** 编写一个实现上一练习伪代码的 if...else 语句。假设 int 变量 counter 已经存在。

**答案：**

```cpp
if (counter > 10) {
    cout << "counter is greater than 10.";
}
else {
    cout << "counter is less than or equal to 10.";
}
```

- **3. (代码)** 编写一个嵌套 if...else 语句，显示 counter 的值是大于 10、等于 10 还是小于 10。

**答案：**

```cpp
if (counter > 10) {
    cout << "counter is greater than 10.";
}
else if (counter == 10) {
    cout << "counter is equal to 10.";
}
else {
    cout << "counter is less than 10.";
}
```

## 3.7 while 迭代语句

迭代语句允许指定程序在某条件保持为真时重复执行某个动作。下面的伪代码语句

```text
while there are more items on my shopping list
    purchase next item and cross it off my list
```

描述了购物行程中的迭代。条件“我的购物清单上还有更多物品”可能为*真*或*假*。如果为*真*，则执行动作“购买下一件物品并将其从我的清单中划掉”。只要条件保持为*真*，该动作就会*重复地*执行。*while* 迭代语句中包含的语句构成其主体，主体可以是单条语句或一个块。最终，条件将变为*假*（当购物清单上的最后一项已被购买并划掉时）。此时，迭代终止，并执行迭代语句之后的第一条语句。

作为 *while* 迭代语句的示例，考虑以下程序段，它查找大于 100 的第一个 3 的幂：

```cpp
int product{3};

while (product <= 100) {
    product = 3 * product;
}
```

此 *while* 语句执行后，变量 `product` 包含结果。*while* 语句的每次迭代都将 `product` 乘以 3，因此 `product` 依次取值为 9、27、81 和 243。当 `product` 变为 243 时，`product <= 100` 变为*假*。这会终止迭代，因此 `product` 的最终值为 243。此时，程序执行将继续进行 *while* 语句之后的下一条语句。如果 *while* 语句的主体中未提供最终使条件变为*假*的动作，则会导致称为*无限循环*的逻辑错误（循环永不终止）。

### *while* 语句的 UML 活动图

下面的 *while* 语句 UML 活动图引入了合并符号：

![](img/7b5e2088e71c7f78681d4ddbcf104c06_164_0.png)

UML 将合并符号和判定符号都表示为菱形。合并符号将两个活动流合并为一个。在此图中，合并符号连接来自初始状态和动作状态的转移，因此它们都流入决定循环是否应开始（或继续）执行的判定。

可以通过传入和传出转移箭头的数量来区分判定符号和合并符号。判定符号有一个指向菱形的转移箭头，以及两个或更多从它指向外的箭头，以表示从该判定可能发生的转移。此外，从判定符号指向外的每个箭头都有一个守卫条件。合并符号有两个或更多指向它的转移箭头，并且只有一个从它指向外的箭头，以表示多个活动流合并后继续该活动。与合并符号关联的转移箭头都没有守卫条件。
