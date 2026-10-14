
关于 Python 和 OOP 需要注意的一点是：在你的代码中使用对象并非强制性的。正如你之前所见，Python 使用函数也能运行得很好。与 Java 等语言不同，你不必局限于一种做事方式；你可以根据需要在同一程序中混合使用函数和类。这使得你构建代码
以最合适的方式运作；也许你不需要编写一个包含初始化代码和方法的完整类仅仅为了返回一个计算结果。在使用 Python 时，你可以达到你想要的技术深度。

##### 15.2 类有什么优势？

想象一下，你有一个程序使用函数来计算二维平面上汽车的速度。如果你想制作一个新的程序来计算三维空间中飞机的速度，你可以利用汽车函数的概念来让飞机模型工作，但你必须重写许多函数以适应垂直维度，尤其是如果你想在三维空间中映射该对象。你可能会很幸运，能够复制粘贴其中的一些函数，但大部分情况下你都得重做许多工作。

类允许你定义一次对象，然后多次复用它。你可以给它一个基础函数（在 OOP 术语中称为方法），然后基于该方法对其进行重新定义，按需扩展。它也比使用函数更准确地模拟现实世界中的对象。

例如，你可以创建一个轮胎类，定义轮胎的尺寸、保持的压力、材质等，然后创建方法来确定在特定条件下轮胎磨损的速度。接着，你可以将这个轮胎类用作汽车类、自行车类或任何其他类的一部分。轮胎类的每次使用（称为实例）都会使用基础轮胎对象的不同属性。如果基础轮胎对象说它只是由橡胶制成，那么汽车类可能会通过声明轮胎带有钢带来“增强”它，或者自行车类可能会说它有一个内部气囊。这一点稍后会有更清晰的解释。

##### 15.3 提升你的类素养

有几种类的概念非常重要，需要知道。

- 1. 类拥有明确的命名空间，就像模块一样。尝试从不同的类调用类方法会产生错误，除非你对其进行限定，例如 `spamClass.eggMethod`。

- 2. 类支持多个副本。这是因为类具有两种不同的对象：类对象和实例对象。类对象提供默认行为，用于创建实例对象。实例对象是在你的程序中实际执行工作的对象。你可以拥有同一类对象任意数量的实例对象。实例对象通常由关键字 `self` 标记，因此类方法可以是 `Car.Brake()`，而 `Brake()` 方法的特定实例会被标记为 `self.Brake()`。（我稍后会更深入地介绍这一点）。

- 3. 每个实例对象都有自己独立的命名空间，同时也继承自基础类对象。这意味着每个实例具有与类对象相同的默认命名空间组件，但此外每个实例还可以为自己创建新的命名空间对象。

- 4. 类可以定义响应与内置类型相同操作的对象。因此，类对象可以像字符串、列表和其他标准 Python 类型一样被切片、索引、连接等。这是因为 Python 中的一切实际上都是类对象；我们并没有在使用类时做真正的新颖事情，我们只是在学习如何更好地利用 Python 语言固有的特性。

以下是 Python OOP 思想的简要列表：

- 类语句创建类对象并为其命名。这会创建一个新的命名空间。

- 类内部的赋值创建类属性。这些属性通过限定名称使用点语法访问：`ClassName.Attribute`。

- 类属性导出对象的状态及其关联的行为。这些属性被类的所有实例共享。

- 调用类（就像函数一样）创建该类的新实例。这就是支持多个副本的部分。

- 每个实例都会获取（“继承”）默认的类属性，并获得自己独立的命名空间。这防止了实例对象相互重叠并使程序混乱。

- 使用术语 `self` 来标识特定实例，从而允许按实例定义属性。这使得变量等项目能够与特定实例相关联。

##### 15.4 类看起来是什么样子的？

在结束本教程的这一部分之前，我会给你一些快速示例来解释我到目前为止所谈论的内容。假设你正在使用 Python 交互式解释器，一个简单的类看起来像这样。

```python
###### Listing 15.1: Defining a class
>>> class Hero: #define a class object
...     def setName(self, value):  #define class methods
...         self.name = value   #self identifies a particular instance
...     def display(self):
...         print self.name #print the data for a particular instance
```

关于这个示例，有几点需要注意：

- 1. 当定义类对象时，末尾没有括号；括号仅用于函数和方法。但是，有关注意事项请参见第 15.5 节。

- 2. 类方法括号中的第一个参数必须是 `self`。这用于标识调用该方法的实例。Python 解释器在内部处理调用。你要做的只是确保 `self` 在正确的位置，以避免错误。尽管你必须使用 `self` 来标识每个实例，但 Python 足够智能，知道正在引用哪个特定实例，因此同时存在多个实例并不是问题。（`self` 类似于 `this`，后者用于 Java 等多种其他语言）。

- 3. 当你分配变量时，例如 “self.name”，变量必须用 "self" 标题进行限定。同样，这用于标识特定实例。

那么，让我们创建几个实例来看看这是如何工作的：

```python
###### Listing 15.2: Creating class instances
>>> x = Hero()
>>> y = Hero()
>>> z = Hero()
```

这里你会注意到出现了括号。这表示这些是由 Hero 类创建的实例对象。这些实例中的每一个都具有完全相同的属性，这些属性继承自 Hero 类。（稍后我会展示如何自定义实例以执行比基础类更多的操作）。

现在，让我们添加一些信息。

```python
###### Listing 15.3: Adding data to instances
>>> x.setName("Arthur, King of the Britons")
>>> y.setName("Sir Lancelot, the Brave")
>>> z.setName("Sir Robin, the Not-Quite-So-Brave-As-Sir-Lancelot")
```

这些调用了位于 Hero 类中的 **setName()** 方法。然而，正如你现在所知，每一个都是针对不同的实例；不仅 x、y 和 z 每个都有不同的值，而且 Hero 中的原始值也保持未变。

如果你现在为每个实例调用 **display()** 方法，你应该能看到每个英雄的名字。

```python
###### Listing 15.4: Displaying instance data
>>> x.display()
Arthur, King of the Britons
>>> y.display()
Sir Lancelot, the Brave
>>> z.display()
Sir Robin, the Not-Quite-So-Brave-As-Sir-Lancelot
```

你可以通过在类对象内的方法中向 *self* 赋值，或者通过显式向实例对象赋值，来“即时”更改实例属性。

```python
###### Listing 15.5: Modifying instances
>>> x.name = "Sir Galahad, the Pure"
>>> x.display()
Sir Galahad, the Pure
```

对于这一课，这大概已经足够了。我将在下一章中涵盖类的其余部分，但希望这足以让你了解在编程中类和 OOP 一般可以多么有用。目前使用的大多数语言在某种程度上都实现了 OOP，因此学习如何使用类和对象将有助于你在获得知识时有所帮助。幸运的是，Python 以合理的方式实现了 OOP，因此与 C++ 相比，在 Python 中学习起来相对无痛，至少根据我的经验来看如此。

##### 15.5 “新式”类

从 Python 2.2 开始，为 Python 开发了一种新类型的类。这种新类为程序员提供了一种创建直接从 Python 内置类型（如列表、字符串等）派生的类的方法。

你可以像上面的示例那样创建一个新类，不使用括号。但是，你也可以显式地从 *object* 类继承你的新类，或者从内置类型之一派生新类。Listing 15.6 展示了这是如何看起来的。将你的自定义类从 *object* 派生是一个好主意，因为 Python 3.x 仅使用“新式”类，而省略 *object* 可能会导致问题。更多信息可以在 Python 新式类简介和 Python 的新式类中找到。

```python
###### Listing 15.6: New-style classes
class NewStyleUserDefinedClass(object):
    pass
class DerivedFromBuiltInType(list):
    pass
```

##### 15.6 关于风格

如前所述，Python 有一种被视为编写 Python 程序“正确”方式的特定“风格语法”。PEP 8 是描述所有“被认可”编写方式的文档。其中一点是关于如何命名类、函数、方法等。

类的名称首字母应大写；类名中的其他单词也应以大写字母开头：`class SpamAndEggs(object)`。函数和方法应使用小写字母，单词之间用下划线分隔：`def bunny_vicious_bite()`。常量（值不发生变化的变量）应全部使用大写字母：`MAX_VALUE = 22`。

还有许多其他需要关注的风格想法。我必须承认，我在遵循 Python 风格约定方面并不是做得最好的人，但我会尽力根据记忆去遵循它们。即使我不遵循“Python 方式”，我也试图在我自己的程序中保持一致性。我个人的建议是阅读 PEP 8 并查看不同 Python 程序的源代码，然后选择最适合你的风格。最重要的是拥有一致的风格。

### 第 16 章

#### 面向对象编程进阶

上一章我告诉你了一些关于使用 Python 类和面向对象编程的基础知识。现在是时候深入探讨类，看看它们如何让编程生活变得更好。

##### 16.1 继承

首先，类允许你在不真正修改程序的情况下对其进行修改。具体来说，通过对类进行子类化，你可以通过向其添加新的组件来改变程序的行为，而不是重写现有的组件。

如我们所见，类的实例继承该类的属性。然而，类也可以从其他类继承属性。因此，子类从父类（超类）继承，允许你创建一个通用的父类，并通过子类对其进行特化。子类可以覆盖父类中的逻辑，允许你在完全不改变父类的情况下改变类的行为。

让我们做一个简单的示例。首先创建一个类：

列表 16.1：定义父类

```python
class FirstClass:    #define the superclass
    def setdata(self, value):   #define methods
        self.data = value    #self' refers to an instance
```

然后我们创建一个子类：

列表 16.2：定义子类

```python
class SecondClass(FirstClass):  #inherits from FirstClass
    def display(self):  #redefines 'display'
        print "Current value = '%s'" % self.data
```

你可以看到，SecondClass “覆盖”了 display 方法。当创建 FirstClass 的实例时，其所有操作都将取自在 FirstClass 中定义的方法。当创建 SecondClass 的实例时，它将使用从 FirstClass 继承的 setdata() 方法，但 display 方法将是来自 SecondClass 的那一个。

为了便于理解，这里有一些实践中的示例。

列表 16.3：更多继承示例

```python
x = FirstClass() #instance of FirstClass
y = SecondClass() #instance of SecondClass
x.setdata("The boy called Brian.")
y.setdata(42)
x.display()
The boy called Brian.
y.display()
Current value = '42'
```

两个实例（x 和 y）都使用来自 FirstClass 的同一个 setdata() 方法；x 使用它是因为它是 FirstClass 的实例，而 y 使用它是因为 SecondClass 从 FirstClass 继承了 setdata()。然而，当调用 display 方法时，x 使用 FirstClass 中的定义，而 y 使用 SecondClass 中的定义，其中 display 被覆盖了。

由于可以通过子类对程序逻辑进行修改，与传统的函数相比，类的使用通常更好地支持代码复用和扩展。函数必须被重写才能改变其工作方式，而类只需进行子类化即可重新定义方法。

最后一点说明，如果你需要一个属于不同组的类，可以使用多重继承（在括号中添加多个父类）。从理论上讲，这是好的，因为它应该减少额外的工作。例如，一个人可以是厨师、音乐家、店主和程序员；这个人可以继承所有这些角色的属性。但在现实中，管理多重继承集可能非常痛苦。你必须问自己，“这个类是否真的需要从所有这些其他类继承？”；答案通常是“不是”。

使用多重继承被认为是一种“高级技术”，因此我不会讨论它。实际上，我不使用它；如果我遇到可以使用它的情况，我会尝试重新思考程序的结构以避免使用它。这有点像规范化数据库；你不断将其分解，直到它变得尽可能简单。如果你仍然需要多重继承，我建议你阅读更高级的 Python 书籍。

##### 16.2 运算符重载

运算符重载简单地意味着，你从类创建的对象可以响应 Python 内部已定义的操作（动作），如加法、切片、打印等。虽然这些操作可以通过类方法实现，但使用重载将行为更紧密地绑定到 Python 的对象模型，并且对象接口与 Python 的内置对象更一致，因此重载更容易学习和使用。

用户自定义的类可以覆盖 Python 内置的操作方法几乎全部。这些方法通过方法名称前后有两个下划线来识别，像这样：`__add__`。当 Python 评估运算符时，这些方法会被自动调用；如果用户类重载了 `__add__` 方法，那么当表达式中包含“+”时，将使用用户的方法而不是 Python 的内置方法。

借用《Learning Python》一书中的例子，以下是运算符重载在实际中如何工作的示例：

列表 16.4：运算符重载示例

```python
class ThirdClass(SecondClass):    #is-a SecondClass
    def __init__(self, value):    #on "ThirdClass(value)"
        self.data = value
    def __add__(self, other):    # on "self + other"
        return ThirdClass(self.data + other)
    def __mul__(self, other):    #on "self * other"
        self.data = self.data * other

a = ThirdClass("abc")    #new __init__ called
a.display()  #inherited method
Current value = 'abc'
b = a + "xyz"    #new __add__ called: makes a new instance
b.display()
Current value = 'abcxyz'
a * 3    #new __mul__ called: changes instance in-place
a.display()
Current value = 'abcabcabc'
```

ThirdClass 在技术上是一个 SecondClass 的子类，但它没有覆盖 SecondClass 的任何方法。如果你愿意，可以将 ThirdClass 中的方法放入 SecondClass，然后从那里开始。然而，创建一个新的子类允许你在程序中拥有灵活性。

当创建 ThirdClass 的新实例时，`__init__` 方法接受实例创建参数并将其赋值给 self.data。ThirdClass 还覆盖了“+”和“*”运算符；当在表达式中遇到这些运算符之一时，运算符左侧的实例对象传递给 self 参数，右侧的对象传递给 other。这些方法与 Python 处理“+”和“*”的正常方式不同，但它们仅适用于 ThirdClass 的实例。其他类的实例仍使用 Python 的内置方法。

关于运算符重载还要最后提及的一点是，你可以让你的自定义方法做任何你想做的事。然而，常见的做法是遵循内置方法的结构。也就是说，如果一个内置方法在调用时创建了一个新对象，你的覆盖方法也应该如此。这可以减少当其他人使用你的代码时的混淆。关于上面的例子，解决“*”表达式的内置方法创建一个新对象（就像“+”方法那样），因此我们创建的覆盖方法可能也应该创建一个新对象，而不是像目前那样就地改变值。你并没有义务“遵守规则”，但当事情按预期工作时，这确实让事情变得更简单。

##### 16.3 类方法

实例方法（我们到目前为止一直在使用的方法）和类方法是调用 Python 方法的两种方式。事实上，实例方法会被 Python 自动转换为类方法。

这就是我想说的。假设你有一个类：

列表 16.5：类方法，第一部分

```python
class PrintClass:
    def printMethod(self, input):
        print input
```

现在我们将使用普通的实例方法和“新”的类方法来调用该类的方法：

列表 16.6：类方法，第二部分
