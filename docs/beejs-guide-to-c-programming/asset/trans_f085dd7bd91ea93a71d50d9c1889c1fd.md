
## 第 10 章

## typedef：创建新类型

与其说是创建新类型，倒不如说是为现有类型获取新名称。表面上听起来有点毫无意义，但我们可以利用这一点来让代码更整洁。

## 10.1 理论上的 typedef

基本上，你取一个现有类型并使用 `typedef` 为它创建一个别名。
如下：

```c
typedef int antelope; // 让 "antelope" 成为 "int" 的别名

antelope x = 10;              类型 "antelope" 与类型 "int" 相同
```

你可以对任何现有的类型执行此操作。你甚至可以使用逗号列表创建多个类型：
```c
typedef int antelope, bagel, mushroom; // 这些都是 "int"
```

这非常有用，对吧？你可以输入 `mushroom` 而不是 `int`？你一定对这个功能感到超级兴奋吧！
讽刺教授（Professor Sarcasm）——我们稍后介绍它的一些更常见的应用。

### 10.1.1 作用域

typedef 遵循作用域规则。
由于某种原因，经常会发现文件作用域（“全局”）的 typedef，这样所有函数都可以随心所欲使用新类型。

## 10.2 实践中的 typedef

所以，将 `int` 重命名为其他东西并没有那么有趣。让我们看看 typedef 通常出现在哪里。

### 10.2.1 typedef 和结构体 (structs)

有时候结构体会被 `typedef` 为一个新名称，这样你就不需要反复输入 `struct` 单词。

```c
struct animal {
  char *name;
  int leg_count, speed;
};
```

```c
// 原名    新名称
//               |       |
//               V       V
//      |----------|-----
typedef struct animal;
```

struct animal y; // 这可以运行，因为 "animal" 是一个别名
animal z; // 这也可以运行

个人而言，我不喜欢这种做法。在类型中添加 `struct` 单词时，代码具有清晰度；程序员们知道他们得到的是什么。但这非常常见，所以我把它放在这里。

现在我想以你可能会常见的方式给出确切的示例。我们将 `struct animal` 放在 `typedef` 中。你可以像这样把它们合并在一起：

```c
// 原名
//               |
//               V
//      |------------
typedef struct animal {
  char *name;
  int leg_count, speed;
} animal; // <-- 新名称
```

struct animal y; // 这可以运行，因为 "animal" 是一个别名
animal z; // 这也可以运行

这与之前的示例完全相同，只是更简洁。

但并非如此！你可能会在使用所谓的“匿名结构体”（anonymous structures）的代码中看到另一种快捷方法。事实证明你实际上不需要在很多地方为结构体命名，而 `typedef` 就是其中之一。

让我们用匿名结构体做同样的示例：

```c
// 匿名结构体！它没有名字！
//               |
//               V
//      |-----
typedef struct {
  char *name;
  int leg_count, speed;
} animal; // <-- 新名称
```

// struct animal y; // 错误：这不再起作用——没有 struct！
animal z; // 这可以运行，因为 "animal" 是一个别名

```

作为另一个示例，我们可能会发现这样的内容： 

```c
typedef struct {
  int x, y;
  point;
};
```

> 我们稍后会详细讨论这些。

point p = {.x=20, .y=40};

printf("%d, %d\n", p.x, p.y); // 20, 40

### 10.2.2 typedef 和其他类型

将 `typedef` 用于像 `int` 这样的简单类型并不是完全没用……它可以帮助你抽象类型，以便以后更改它们。

例如，如果你将 `float` 遍布在代码的 100 万亿处，如果你以后发现由于某种原因需要将它们全部改为 `double`，那将非常痛苦。

但如果你提前做了一点准备：

```c
typedef float app_float;

//
app_float f1, f2, f3;
```

那么如果你想更改另一种类型（`long double`），你只需要修改 `typedef`：

```c
//  搞定！
//  |------|
typedef double app_float;
```

// 并且不需要修改这一行：

```c
app_float f1, f2, f3; // 现在这些都是 long 声明。
```

### 10.2.3 typedef 和指针

你可以创建一个类型指针的类型。

```c
typedef int *intptr;
```

```c
int a = 10;
intptr x = &a; // "intptr" 是类型 "int*"
```

我真的不喜欢这种做法。它隐藏了 `x` 是指针类型的事实，因为你没有在声明中看到 `*`。

在我看来（IMHO），显式地显示你正在声明一个指针类型更好，这样其他开发者就能清楚地看到它，而不会误认为 `x` 是非指针类型。

但最后统计，，说有 832,007 人持有不同意见。

### 10.2.4 typedef 和大小写

我见过 `typedef` 各种类型的大写方式。

```c
typedef struct {
int x, y;
} my_point; // 全小写蛇形命名法 (lower snake case)
```

```c
typedef struct {
int x, y;
} MyPoint; // 驼峰命名法 (CamelCase)
```

```c
typedef struct {
    int x, y;
    // 首字母大写 (Leading uppercase)
} Mypoint;

```

```c
typedef struct {
    int x, y;
    // 大写蛇形命名法 (UPPER SNAKE CASE)
} MY_POINT;
```

C11 规范没有规定哪一种，并展示了全大写和小写的示例。

K&R 主要使用大写，但展示了一些大写和蛇形命名法（带 _）。

如果你有风格指南，就遵循它。如果没有，找一个并遵循它。

## 10.3 数组和 typedef

语法有点奇怪，在我的经验中很少见到，但你可以对数组项进行 `typedef`。

```c
// 让 five_ints 成为长度为 5 的数组
typedef int five_ints[5];
```

```c
five_ints x = {11, 22, 33};
```
