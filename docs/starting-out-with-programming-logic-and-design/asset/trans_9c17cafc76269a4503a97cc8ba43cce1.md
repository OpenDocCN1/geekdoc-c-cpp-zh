

## 第 14 章 面向对象编程

将对象作为之前所示 `showAnimalInfo` 模块的参数。程序 14-6 中的伪代码演示了这一点。

## 程序 14-6

```
1 Module main()
2   // 声明三个类变量。
3   Declare Animal myAnimal
4.Declare Dog myDog
5   Declare Cat myCat
6
7   // 创建一个 Animal 对象、一个 Dog 对象、
8   // 和一个 Cat 对象。
9   Set myAnimal = New Animal()
10 Set myDog = New Dog()
11 Set myCat = New Cat()
12
13  // 显示关于动物的信息。
14  Display "Here is info about an animal."
15  showAnimalInfo(myAnimal)
16  Display
17
18  // 显示关于狗的信息。
19  Display "Here is info about a dog."
20  showAnimalInfo(myDog)
21  Display
22
23  // 显示关于猫的信息。
24  Display "Here is info about a cat."
25  showAnimalInfo(myCat)
26  End Module
```

## 程序输出

Here is info about an animal.
I'm just a regular animal.
Grrrrr

Here is info about a dog.
I'm a dog.
Woof! Woof!

Here is info about a cat.
I'm a cat.
Meow

## 复习题

尽管这些示例非常简单，但多态有很多实际用途。例如，大学的软件处理大量关于学生的数据，因此它可能会使用 `Student` 类。`Student` 类中的一个方法可能被称为 `getFees`。该方法将返回一个典型生物学生的费用金额。

此外，软件可能有一个 `BiologyStudent` 作为 `Student` 类的子类（因为生物学生也是学生）。由于额外的实验室费用，生物学学生的费用通常比典型学生高。因此，`BiologyStudent` 类将有自己的方法来返回生物学学生的费用。

![](img/c939132f78787c7f339c6977b3fc8c85_585_0.png)

## 检查点

14.25 观察以下伪代码类定义：

```
Class Vegetable
  Public Module message()
  Display "I'm a vegetable."
End Class
Class Potato Extends Vegetable
  Public Module message()
  Display "I'm a potato."
End Class
```

给定这些定义，以下伪代码将执行什么？

```
Declare Vegetable v
Declare Potato p
Set v = New Potato()
Set p = New Potato()
Call v.message()
Call p.message()
```

## 复习题

#### 单选题

- 1. 一种 \__________ 编程实践是以创建与它们处理的数据分离的模块和函数为中心的。
    - a. 模块化的
    - b. 过程化的
    - c. 函数式的
    - d. 面向对象的

- 2. 一种 \__________ 编程实践是以创建对象为中心的。
    - a. 以对象为中心的
    - b. 目标导向的
    - c. 过程化的
    - d. 面向对象的

- 3. 一个 ________ 是类中持有数据的成员。
    - a. 方法
    - b. 实例
    - c. 字段
    - d. 构造函数

- 4. _________ 指定了类的字段或方法如何被类外部的代码访问。
    - a. 字段声明
    - b. New 关键字
    - c. 访问修饰符
    - d. 构造函数

- 5. 类字段通常用 _________ 访问修饰符声明。
    - a. 私有 (Private)
    - b. 公有 (Public)
    - c. 只读 (ReadOnly)
    - d. 隐藏 (Hidden)

- 6. ________ 是一种可以引用内存中对象的特殊类型变量。
    - a. 内存
    - b. 过程化的
    - c. 类
    - d. 动态的

- 7. 在许多编程语言中，________ 在内存中创建一个对象。
    - a. Create
    - b. New
    - c. Instantiate
    - d. Declare

- 8. 一种 ________ 方法从类的字段获取值但不改变它。
    - a. 获取器 (retriever)
    - b. 构造函数
    - c. 修改器 (mutator)
    - d. 访问器 (accessor)

- 9. 一种 ________ 方法在字段中存储值或以某种方式更改字段的值。
    - a. 修改 (modifier)
    - b. 构造函数
    - c. 修改器 (mutator)
    - d. 访问器 (accessor)

- 10. 当创建对象时会自动调用一种 ________ 方法。
    - a. 访问器 (accessor)
    - b. 构造函数
    - c. 设置 (setter)
    - d. 修改器 (mutator)

- 11. 由 ________ 提供的图形描述面向对象的系统的标准图。
    - a. 统一建模语言 (ML)
    - b. 流程图
    - c. 伪代码
    - d. 对象层次系统

- 12. 当某项的值取决于其他数据，且当数据更改时该项没有更新时，我们说该值变成了 _________
    - a. 苦的 (bitter)
    - b. 过时的 (stale)
    - c. 异步的 (asynchronous)
    - d. 发霉的 (moldy)

- 13. 类的职责是 _________
    - a. 从类创建的对象
    - b. 类所知道的内容
    - c. 类执行的操作
    - d. 都是 b 和 c

- 14. 在继承关系中，________ 是通用类。
    - a. 子类
    - b. 基类
    - c. 奴隶类
    - d. 子类

- 15. 在继承关系中，________ 是特化类。
    - a. 基类
    - b. 主类
    - c. 子类
    - d. 父类

- 16. 面向对象编程的 _________ 特性允许基类变量引用子类对象。
    - a. 多态
    - b. 继承
    - c. 泛化
    - d. 特殊化

### 判断题

- 1. 过程化编程实践是以创建对象为中心的。
- 2. 对象重用性是增加面向对象编程使用的的一个因素。
- 3. 面向对象编程中一种常见的做法是将类的所有字段设为公有。
- 4. 寻找面向对象程序所需类的方法是识别问题描述中所有的动词。
- 5. 子类继承子类的字段和方法。
- 6. 多态允许基类变量引用基类或子类的对象。

### 简答

1. 什么是封装？
2. 为什么对象的内部数据通常对外部代码隐藏？
3. 类和类的实例之间的区别是什么？
4. 在许多编程语言中，`new` 关键字的作用是什么？
5. 下述伪代码语句调用了对象的方法。方法的名称是什么？引用对象的变量名称是什么？
`Call wallet.get()`
6. 什么是过时数据 (stale data)？
7. 子类从其基类继承什么？
8. 观察以下伪代码，类定义的第一行。基类的名称是什么？子类的名称是什么？
`Class Tiger Extends Felis`

## 算法工作

1. 假设 `myCar` 是引用对象的类变量名，`go` 是一个方法名。该方法不接受任何参数。
2. 观察此部分定义，然后按照说明操作：
   `Class Book`
   `Private String title`
   `Private String author`
   `Private Integer copiesSold`
   a. 为此类编写一个构造函数。
   b. 为每个字段编写访问器（accessor）和修改器（mutator）方法。
   c. 为该类绘制 UML 图。
3. 银行提供以下类型的账户：储蓄账户、支票账户和货币市场账户。客户允许向账户存款（增加余额）、从账户取款（从而减少余额）并赚利。每个账户都有利率。
   a. 识别该领域的潜在类。
   b. 精炼列表以仅包含必要的类。
   c. 识别类的职责。
4. 用伪代码写出 Poodle 类定义的第一行。该类应该扩展 `dog` 类。
5. 观察以下类定义：
   ```
   Class Plant
     Public Module message()
     Display "I'm a plant."
   End Class
   Class Tree Extends Plant
     Public Module message()
     Display "I'm a tree."
   End Class
   ```
   给定这些定义，以下伪代码将设计什么？
   `Declare Plant p`
   `Set p = New Tree()`
   `Call p.message()`

## 编程练习

1. Pet 类

设计一个名为 `Pet` 的类，它应该具有以下字段：

- name: name 字段持有宠的名称。
- type: type 字段持有动物的类型。示例值为 "Dog", "Cat" 和 "Bird"。
- age: age 字段持有宠物的年龄。

`Pet` 类应该有以下方法：

- setName: setName 方法在 name 字段中存储一个值。
- setType: setType 方法在 type 字段中存储一个值。
- setAge: setAge 方法在 age 字段中存储一个值。
- getName: getName 方法返回 name 字段的值。
- getType: getType 方法返回 type 字段的值。
- getAge: getAge 方法返回 age 字段的值。

设计好该类后，设计一个程序创建该类的一个对象，并提示用户输入宠的名称、类型和年龄。这些数据应该存储在对象中。使用对象的访问器方法获取宠的名称、类型和年龄，并将这些数据显示在屏幕上。

2. Car 类

设计一个 `Car` 类，它具有以下字段：

- yearModel: yearModel 字段是一个整数，持有汽车的年份。
- make: make 字段引用一个字符串，持有汽车的品牌。
- speed: speed 字段是一个整数，持有汽车的当前速度。

此外，该类应该有以下构造函数和其他方法：

- 构造函数：构造函数接受汽车的年份和品牌作为参数。这些值应被赋值给对象的 `yearModel` 和 `make` 字段。构造函数还将将 `speed` 字段赋值为 0。

