
# 陷阱：未初始化变量

变量在程序为其赋值之前，不具有有意义的值。例如，如果变量minimumNumber没有通过赋值语句左侧或其他方式（如通过cin语句获得输入值）被赋值，那么下面的代码就是一个错误：

```
desiredNumber = minimumNumber + 10;
```

这是因为minimumNumber没有有意义的值，因此等号右侧的整个表达式也没有有意义的值。像minimumNumber这样未被赋值的变量称为未初始化变量。实际上，这种情况比minimumNumber完全没有值更糟糕。未初始化变量（如minimumNumber）只会包含某个垃圾值。未初始化变量的值取决于最后一个使用该内存区域的程序留在其内存位置上的任意0和1模式。

避免未初始化变量的一种方法是在声明变量的同时对其进行初始化。可以通过添加等号和值来实现，如下所示：

```
int minimumNumber = 3;
```

这既将minimumNumber声明为int类型的变量，又将变量minimumNumber的值设置为3。以这种方式在声明中初始化变量时，可以使用更复杂的表达式，例如涉及加法或乘法的表达式。再举一个例子，下面声明了三个变量并初始化了其中两个：

```
double rate = 0.07, time, balance = 0.00;
```

C++允许在声明变量时使用另一种初始化语法。下面演示了这种替代语法，它与前面的声明等价：

```
double rate(0.07), time, balance(0.00);
```

## 在声明中初始化变量

你可以在声明变量时初始化变量（即给它一个值）。

## 语法

```
Type_Name Variable_Name_1 = Expression_for_Value_1,
    Variable_Name_2 = Expression_for_Value_2, ...;
```

**示例**

```text
int count = 0, limit = 10, fudgeFactor = 2;
double distance = 999.99;
```

## 语法

在声明中初始化的替代语法：

```
Type_Name Variable_Name_1 (Expression_for_Value_1),
             Variable_Name_2 (Expression_for_Value_2), ...;
```

**示例**

```text
int count(0), limit(10), fudgeFactor(2);
double distance(999.99);
```

## 提示——使用有意义的名称

程序中的变量名和其他名称至少应暗示其命名对象的含义或用途。如果变量具有有意义的名称，程序就更容易理解。对比

```text
x = y * z;
```

与更具提示性的

```text
distance = speed * time;
```

这两个语句完成同样的事情，但第二个更容易理解。

## 更多赋值语句

存在一种简写符号，它将赋值运算符（=）与算术运算符组合在一起，从而可以通过加、减、乘或除以指定值来改变给定变量的值。一般形式为

```text
Variable Operator = Expression
```

它等价于

```text
Variable = Variable Operator (Expression)
```

表达式可以是另一个变量、一个常量或更复杂的算术表达式。下面列出了一些示例。

| 示例 | 等价于 |
|---|---|
| count += 2; | count = count + 2; |
| total -= discount; | total = total - discount; |
| bonus *= 2; | bonus = bonus * 2; |
| time /= rushFactor; | time = time/rushFactor; |
| change %= 100; | change = change % 100; |
| amount *= cnt1 + cnt2; | amount = amount * (cnt1 + cnt2); |

# 自测练习

- 1. 给出名为feet和inches的两个变量的声明。两个变量都是int类型，并且都应在声明中初始化为零。给出两种初始化替代方案。
- 2. 给出名为count和distance的两个变量的声明。count是int类型，初始化为零。distance是double类型，初始化为1.5。给出两种初始化替代方案。
- 3. 编写一个程序，其中包含一些语句，用于输出五个或六个已定义但未初始化变量的值。编译并运行该程序。输出是什么？请解释。

# 赋值兼容性

作为一般规则，你不能将一种类型的值存储在另一种类型的变量中。例如，大多数编译器会反对以下代码：

int intVariable;
intVariable = 2.99;

问题是类型不匹配。常量2.99是double类型，而变量intVariable是int类型。不幸的是，并非所有编译器对上述赋值语句的反应都相同。有些会发出错误消息，有些只会发出警告消息，还有些编译器根本不会反对。即使编译器确实允许你使用上述赋值，它也会给intVariable赋予int值2，而不是3。既然你不能指望编译器接受上述赋值，就不应该将double值赋给int类型的变量。

即使编译器允许你在赋值语句中混合类型，在大多数情况下你也不应该这样做。这样做会降低程序的可移植性，并且可能造成混淆。

在某些特殊情况下，允许将一种类型的值赋给另一种类型的变量。将整数类型（如int）的值赋给浮点类型（如double）的变量是可以接受的。例如，以下代码既合法又风格可接受：

```
double doubleVariable;
doubleVariable = 2;
```

上述代码会将名为doubleVariable的变量的值设置为2.0。

尽管这样做通常不是一个好主意，但你可以将int值（如65）存储在char类型的变量中，也可以将字母（如'Z'）存储在int类型的变量中。在许多情况下，C语言将字符视为小整数，也许不幸的是，C++从C语言继承了这一点。允许这样做是因为char类型的变量比int类型的变量占用更少的内存；因此，用char类型的变量进行算术运算可以节省一些内存。然而，处理整数时使用int类型，处理字符时使用char类型会更清晰。

一般规则是，你不能将一种类型的值放入另一种类型的变量中——尽管看起来这条规则的例外情况可能比遵循规则的情况还要多。即使编译器没有非常严格地执行这条规则，遵循它仍然是一个好习惯。将一种类型的数据放入另一种类型的变量可能会引起问题，因为该值必须被转换为适当类型的值，而这个值可能不是你期望的。

bool类型的值可以赋给整数类型（short、int、long）的变量，整数也可以赋给bool类型的变量。不过，这样做风格不佳。为了完整性并帮助你阅读他人的代码，以下是细节：当赋给bool类型的变量时，任何非零整数都将存储为true。零将存储为false。当将bool值赋给整数变量时，true存储为1，false存储为0。

# 字面量

字面量是某个特定值的名称。字面量通常被称为常量，与变量相对。字面量或常量不会改变值；变量可以改变其值。整数常量的书写方式与你平时写数字的方式一致。int类型（或任何其他整数类型）的常量不能包含小数点。double类型的常量可以用两种形式之一书写。double常量的简单形式类似于日常书写小数的方式。以这种形式书写时，double常量必须包含小数点。在C++中，任何数字常量（整数或浮点数）都不能包含逗号。

