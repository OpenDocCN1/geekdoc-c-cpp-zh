

| array |
array := Array new: 100.      "Instantiate an array of 100 positions"
1 to: array size do: [:i |      "Treat odd and even positions differently"
    i odd
        ifTrue: [array at: i put: 1]
        ifFalse: [array at: i put: 2]]

ifTrue:ifFalse: 消息的接收者必须是 Boolean 对象。两个参数是代码块，表达了 if/else 逻辑中的替代操作路径。接收者对象根据自身状态（true 或 false）只评估两个块中的一个。注意，在此示例中，临时变量 array 和块变量 i 的作用域包含任何嵌套块。

由于 to:do: 循环消息是发送给一个数字的，实现其方法的代码位于 Number 类中。我们稍后会讨论为类定义方法，但这里有一个预览，显示 to:do: 实际上只是对更繁琐的、计数控制的 whileTrue: 循环的语法糖：

```
to: aNumber do: aBlock
"Evaluate the one argument block aBlock for the
numbers between the receiver and the argument
aNumber where each number is the previous number
plus 1."
| index |
index := self.
[index <= aNumber]
    whileTrue: [
        aBlock value: index.
        index := index + 1]
```

在此方法定义上下文中，符号 self 指的是消息的接收者，在此例中为一个数字。whileTrue: 消息关联了两个块。与 ifTrue:ifFalse: 消息不同，其接收者对象只被评估一次，whileTrue: 消息必须以块作为其接收者对象。Smalltalk 评估此块，其中包含一个布尔表达式，一次或多次，直到它返回 false。每次第一个块评估为 true 时，第二个块（whileTrue: 的参数），即循环体，也会被评估。此第二个块中的代码包含两个语句。第一个语句通过发送 value: 消息来评估 aBlock（此处正在定义 to:do: 方法的参数）。在循环过程中，此消息的参数 index 会取到 self 与 aNumber 之间序列中每个数字的值。第二个语句递增 index 以实现此效果。

本小节中的最后一个示例代码段展示了如何将数组的内容打印到 transcript 窗口。代码使用 do: 循环遍历数组。这里我们不关心在数组的索引位置替换元素，而只是访问元素本身。do: 循环按顺序访问数组的每个元素，从第一个到最后一个。每次循环遍历时，块参数都会被评估，块变量绑定到当前元素。

```
```smalltalk
array do: [:element | "Print to transcript each element followed by a return"
    Transcript nextPutAll: element printString; cr]
```
```

全局变量 Transcript 指 Smalltalk 的 transcript 窗口对象。nextPutAll 消息期望一个字符串作为参数，因此我们使用 printString 消息获取元素的字符串表示，然后将其发送到 transcript。此消息还要求 transcript 显示一个回车字符。

Smalltalk 包含许多类型的集合类以及用于对集合执行迭代的不同类型的消息，例如 map 和 filter，与函数式语言类似。我们稍后会讨论其中一些操作，也称为 **iterators**。

正如这些简短示例所示，大多数 Smalltalk 代码都由创建适当类的对象并向其发送消息组成。对象本身处理大部分算法细节。剩下的软件开发工作则在于为合适的工作选择合适的类并学习其接口。当此类类尚不存在时，Smalltalk 程序员会创建新的类来自定义现有类。为了了解这是如何完成的，我们现在探索 Smalltalk 庞大的内置类层次结构中的两个类别的类：magnitudes 和 collections。

## 5.2.2 The Magnitude Hierarchy

一个类提供了对象集合的属性和行为的定义。在 Smalltalk 中，内置类以树状层次结构组织，根部有一个名为 Object 的单一类。Object 下的每个类都继承其在层次结构中祖先类中定义的任何属性和行为。层次结构中的类通常从更一般到更具体地下降，每个新类都会增加和/或修改其上方类中已有的行为和/或属性。**Inheritance**，因此支持结构和行为的重用。**Polymorphism**，或对不同类请求类似服务的消息使用相同名称，也是一种代码重用形式。在本节中，我们检查 Smalltalk 的 magnitude 类的一部分，如图 5.1 的类图中所示。

![](img/062750ade02e28185b1fb8e8cf6dc89e_156_0.png)

正如您从图 5.2 中看到的，magnitude 类包括其他语言中常见的数字类型，如 Integer、Float 和 Fraction，以及与数值相关的一些其他类型，如 Time 和 Date。这些类有时被称为 **concrete classes**，

因为它们的实例是应用程序通常创建和操作的对象。相比之下，此层次结构中的另外两个类，**Magnitude** 和 **Number**，有时被称为 **abstract classes**。它们通常不被实例化，而是作为其下方类共有的属性和行为的存储库。

我们现在在 Smalltalk 的类浏览器中探索 magnitude 类层次结构，以了解类及其方法是如何定义的，并学习语言设计者如何利用继承和多态性。 （请记住，Smalltalk 被构想为不仅是一种语言，也是一种编程环境。）图 5.2 显示了一个类浏览器，magnitude 类列表可见于窗口的最左侧窗格。

![](img/062750ade02e28185b1fb8e8cf6dc89e_157_0.png)

**Figure 5.2** A class browser open on the magnitude classes

请注意，最抽象的类 **Magnitude** 已被选中。其实例消息列在最右侧窗格中。这些包括比较运算符和几个其他消息。这些是任何更具体的 magnitude 类型对象也应识别的最基本消息。图 5.2 的底部窗格中是代码，说明 Magnitude 是 Object 的子类；这意味着在 **Object** 类中定义的任何消息也将被任何 magnitude 类型（或 Smalltalk 中的任何其他类型）的对象识别。该代码还显示 Magnitude 类未定义实例变量、类变量或池字典，从而将它们留给子类在需要时包含。实例变量对应于创建时属于每个单独对象的属性的存储。类变量和池字典对应于所有类对象共有的属性的存储。

图 5.3 显示了在消息列表中选择 max: 消息后相同的浏览器窗口。

![](img/062750ade02e28185b1fb8e8cf6dc89e_158_0.png)

Figure 5.3 The definition of the max: method in the Magnitude class

当程序员选择 max: 消息时，对应于该消息的方法定义出现在底部窗格中。根据方法头和注释，此方法期望另一个 magnitude 对象作为其唯一参数。该方法比较 self，即接收者对象的值，与参数对象，并返回两者中较大的对象。 （Smalltalk 中的返回运算符是 ^，它具有任何运算符中最低的优先级。）在文档中引用时，特定类的特定方法通常会加上类名前缀，以将其与另一类中定义同名的方法区分开来。因此，刚刚检查的方法被标识为 Magnitude>>>max:.

```
max: aMagnitude
"Answer the receiver if it is greater than aMagnitude, else answer aMagnitude."
self > aMagnitude
    ifTrue: [^self]
    ifFalse: [^aMagnitude]
```

