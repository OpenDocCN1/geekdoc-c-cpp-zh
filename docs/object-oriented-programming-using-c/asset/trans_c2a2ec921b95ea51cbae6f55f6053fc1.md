

# 使用 C# 进行面向对象编程

# 统一建模语言 (UML)

## 活动 1

绘制一个图表示名为 'BankAccount' 的类，它具有属性 balance（类型为 int）以及方法 `DepositMoney()`、`WithdrawMoney()` 和 `DisplayBalance()`。请显示合适的可见性修饰符。

反馈 1

| BankAccount |
| :--- |
| - balance :int |
| + DepositMoney() |
| + WithdrawMoney() |
| + DisplayBalance() |

上面的图表显示了这些信息

UML 允许我们在图中忽略不希望突出显示的任何信息——这使我们能够忽略无关的细节，并将读者的注意力集中在我们想要关注的信息上。因此，以下都是有效的类图……

![](img/e143b38d00f95425fa4f3efca0527189_33_0.png)

首先，在不显示访问修饰符的情况下……

| BankAccount |
| :--- |
| balance int |
| DepositMoney() |
| WithdrawMoney() |
| DisplayBalance() |

其次，在显示访问修饰符但不显示数据类型的情况下……

| BankAccount |
| :--- |
| balance |
| DepositMoney() |
| WithdrawMoney() |
| DisplayBalance() |

最后，在不显示属性和方法的情况下……

| BankAccount |
| :--- |

即：有一个名为 'BankAccount' 的类，但它的细节没有显示。

当然，几乎所有的 C# 程序都由许多类组成，类与类之间相互关联——某些类将使用其他类。这些关系通过箭头表示。不同类型的箭头表示不同的关系（包括继承和聚合关系）。

此外，类图还使用了关键字、备注和注释。

正如我们在接下来的示例中看到的，类图可以显示以下信息：

- 类
  - 属性
  - 操作
  - 可见性
- 关系
  - 可导航性
  - 多重性
  - 依赖
  - 聚合
  - 组合
- 一般化 / 特殊化
  - 继承
  - 接口
- 关键字
- 备注和注释

## 2.3 UML 语法

由于 UML 图传达的是精确的信息，因此应该遵循精确的语法。

属性应显示为：*可见性 名称：类型 多重性*

其中可见性是以下之一：

- + public 公
- - private 私有
- # protected 保护
- ~ package 包

多重性是以下之一：

- n 恰好 n
- * 零或多个
- m..n 在 m 到 n 之间

以下是使用 UML 正确指定的属性示例：

- - custRef : int [1]

私有属性 custRef 是一个单一 int 值，这通常显示为 - **custRef : int**。但在没有显示多重性的情况下，我们无法安全地假设作者想要表达多重性为一。

- # itemCodes : String [1..]

受保护属性 `itemCodes` 是一个或多个 String 值。

- # validCard : boolean

属性 `validCard` 的可见性未指定，多重性也未指定。

操作也有精确的语法，并应显示为：
可见性 名称 (参数1 : 类型1, 参数2: 类型2): 返回类型

其中每个参数都用（括号）显示，然后指定返回类型。

例如

+ + AddName(newName : String): boolean

这表示一个公共方法 'AddName'，它接受一个类型为 String 的参数 'newName' 并返回一个布尔值。

## 活动 2

绘制一个图表示名为 'BankAccount' 的类，它有一个私有属性 balance（这是一个单一整数）和一个公共方法 `DepositMoney()`，该方法接受一个整数参数 'deposit' 并返回一个布尔值。在 UML 类图中完整指定所有这些信息。

## 表示关系

类图在表示单个类的同时，还表示类之间的关系。其中一种关系被称为“关联 (Association)”。我们将在第 6 章学习更多关于关联的内容。

反馈 2

| BankAccount |
| :--- |
| - balance :int |
| + DepositMoney(deposit : int): boolean |

上面的图显示了 `OneClass` 拥有属性 `value`。

| OneClass |
| :--- |
| value |

使用关联当 `source` 指向 `target` 类时，为了解释某个类的一个方面，功能性：

![](img/e143b38d00f95425fa4f3efca0527189_38_0.png)

这暗示 `OneClass` 维护一个类型为 `OtherClass` 的集合。我们将在第 7 章查看集合。

活动 3

绘制一个图表示 'Catalogue' 类和如下所示的 ItemForSale 类——ItemSale 有一个类型为 String 的属性 `name` 和一个类型为 int 的属性 `price`。它还有一个方法 `SetPrice()` 接受一个整数参数 `newPrice`。'Catalogue' 有一个属性 `listOfItems`，即当前目录中的项。由于零或多个项可以存储在目录中，`listOfItems` 需要是一个数组或集合。'Catalogue' 还有一个方法 `AddItem()`，接受一个参数（类型为 ItemSale）。在类图中显示属性和方法的适当可见性修饰。

反馈 3

| Catalogue | ItemForSale |
| :--- | :--- |
| 1..* | - name:String |
| + AddItem(item :ItemSale) | + SetPrice(newPrice :int) |

注意：按照这里的命名规范，所有类名大写开头，属性名小写开头，方法名大写开头以区别于类名。此外注意 ItemForSale 描述的是单个项目（而不是多个）。'listItems' 维护零或多个独立对象。

## 关联类型

有由不同箭头表示的不同关联类型：

- 依赖 (Dependency)。

![](img/e143b38d00f95425fa4f3efca0527189_39_0.png)

![](img/e143b38d00f95425fa4f3efca0527189_40_0.png)

- 依赖
- 简单关联（从 A 到 B 可导航）
- 双向关联
- 聚合
- 组合

## 依赖

![](img/e143b38d00f95425fa4f3efca0527189_40_1.png)

- 依赖是类之间最不具体的关系（不是严格的“关联”）
- 类 A 以某种方式使用类 B 定义的功能
- 对类 B 的更改可能会类 A

依赖线的典型情况是：类 A 有一个方法接受类 B 的对象参数，或者使用该类的局部变量，或者调用了类 B 的“静态”方法。

例如：`Print()` 可能需要一个打印机对象作为参数。每次调用 `Print()` 方法时，都可以传递一个不同的打印机对象作为参数，因此打印结果将出现在不同的位置因此因此虽然包含 `Print()` 方法的类需要打印机对象才能工作，但它不需要与特定的打印机永久关联。

