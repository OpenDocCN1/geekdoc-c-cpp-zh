
Smalltalk 受到了 Simula 和 Lisp 的影响。它的初始开发经历了一系列阶段，其主要早期版本为 `Smalltalk-72`、`Smalltalk-76` 和 `Smalltalk-80`。到 20 世纪 80 年代末，普通的桌面计算机已足够强大，可以支持内存密集型的 Smalltalk 编程环境。`Digitalk` 公司发布了 `Smalltalk/V`，它可在 Windows 和 Macintosh 平台上运行。Smalltalk 于 1998 年达到 ANSI 标准，目前有多个开源和低成本商业版本可用。

在所有面向对象语言中，Smalltalk 对面向对象范式的处理最为一致。在 Smalltalk 中，几乎每个语言实体都是一个对象，包括常量（如数字和字符）以及类本身。因此，可以说 Smalltalk 在本质上是纯粹面向对象的，就像 Haskell 等语言可以被称为纯函数式一样。

Smalltalk 从 Lisp 借用了垃圾回收（在运行时自动回收未使用的动态存储）和动态类型（在运行时检查表达式中操作数的类型）的机制。然而，Smalltalk 不仅在语言方面具有创新性，而且从一开始就被设想为个人工作站的完整程序开发环境。用户界面也具有创新性，因为它包括一个具有菜单和鼠标的窗口系统，早在这种系统对个人计算机变得普遍之前很久。

Smalltalk 作为一种语言是交互式的和动态导向的。程序员可以通过在交互式解释器中输入表达式和语句来进行实验。所有类和对象都是通过与系统交互使用一组浏览器窗口创建的。新类在输入到类字典时被编译，对象的交互也由系统管理。Smalltalk 系统附带一个庞大的预先存在的类层次结构，每个新类必须是现有类的子类。在以下小节中，我们将探讨 Smalltalk 表达式和语句的语法、新类的定义，以及消息传递、封装、继承和多态等基本面向对象概念。

### 5.2.1 Smalltalk 的基本元素：类、对象、消息和控制

现实世界中的每个对象都有一组属性和行为。例如，汽车具有包括车轮数量、车门数量和里程评级在内的属性。其行为包括向前移动、向后移动以及向左或向右转。同样，Smalltalk 中的每个对象（即每个数据值和每个类或数据类型），无论是内置的还是由程序员创建的，都有一组属性和行为。在 Smalltalk 程序中，对象通过向它们发送消息来让其他对象做事。消息是对服务的请求。接收消息的对象（有时称为接收者）通过调用适当的方法来执行其服务。该方法反过来可能会向其他对象发送消息以完成其任务。正如你很快就会看到的，方法类似于过程或函数，并在接收者对象的类或其类层次结构中的一个祖先类中定义。消息的发送者也可能随消息一起提供数据，以参数或参数的形式。当接收者的方法调用完成后，它可能会向发送者返回数据（另一个对象）。因此，发送

向对象发送消息有点像在函数式语言中调用函数。然而，一些被称为**修改器**的消息可能会导致接收方对象的状态发生变化，而函数调用只是向调用者返回一个值。发送和接收消息的过程也称为**消息传递**。对象能够识别的消息集合有时被称为它的**接口**。

Smalltalk 的消息传递语法相当简单，但有些不合常规。接收消息的对象写在最前面，后面跟着消息名称（也称为**选择器**）和任何参数。在包含对象和消息的表达式中，各元素通常从左到右读取和求值。例如，我们可以通过向 Smalltalk 内置的 `Set` 类发送 `new` 消息来创建一个新的集合对象，如下所示：

```
Set new    "Returns a new set object"
```

注意，类名首字母大写，消息名首字母不大写。Smalltalk 的注释用双引号括起来。本小节中的任何代码示例都可以通过将它们输入到 Smalltalk 的 `Transcript` 窗口，并从 **Smalltalk** 菜单中选择 **显示它** 选项来进行求值。整个讨论中，我们使用 `Smalltalk/V` 语法。

我们可以通过向这个对象发送 `size` 消息来检查新集合中的元素数量：

```
Set new size    "Returns 0"
```

在这段代码中，`Set` 类接收 `new` 消息，该消息返回一个 `Set` 实例，和之前一样。这个对象接着接收 `size` 消息，该消息返回一个整数对象。`new` 消息也称为**类消息**，因为它是发送给类的；而 `size` 消息称为**实例消息**，因为它是发送给类的实例的。这些消息也是**一元消息**的示例，因为它们不期望任何参数。

需要参数的消息称为**关键字消息**。例如，我们可以通过向新集合发送 `includes:` 消息来查看它是否包含给定元素。这个消息期望一个参数，即搜索的目标对象。在下一个示例中，集合被询问是否包含字符串 `'Hello'`：

```
Set new includes: 'Hello'    "Returns false"
```

注意，关键字消息的名称以冒号（`:`）结尾。如果参数多于一个，则每个参数前面必须另有其他关键字。关键字消息的参数在消息发送之前会被求值。下面的示例向一个新的集合对象添加一个字符串：

```
Set new add: 'Ken'    "This set now includes 'Ken'"
```

`add:` 消息是**修改器**的一个示例，它改变接收方对象的状态。

一个稍微复杂的示例创建一个包含 10 个元素的新数组，并将值 66 存储到数组的第一个位置。代码首先向 `Array` 类发送类消息 `new:`，以实例化一个有 10 个位置的数组（每个位置包含默认值 `nil`）。然后这个数组接收实例消息 `at:put:`，将整数存储到数组的第一个位置。

```
(Array new: 10) at: 1 put: 66    "Stores 66 at the first position in the array"
```

关键字消息 `at:put:` 期望两个参数。第一个参数是数组中某个对象的索引。第二个参数是要放置在该索引处的对象。一元消息的优先级高于关键字消息，可以使用括号来提高清晰度或覆盖优先级。注意，最后一个示例需要括号来区分两个关键字消息。如果没有括号，解释器会把 `new:at:put` 视为 `Array` 类的类消息。这会产生一个无法识别的消息错误。

Smalltalk 还提供了一小组二元消息，允许程序员使用常规中缀表示法编写算术和比较表达式。例如，以下每个表达式：

```
3 + 4    "Returns 7"
3 < 4    "Returns true"
```

实际上都是发送给第一个整数对象（接收方）的关键字消息的语法糖。第二个整数对象是该消息的参数。二元消息的优先级低于关键字消息。

与许多其他语言一样，程序员可以使用变量来引用对象，也可以使用语句序列来组织代码。下一个代码段将一个新的五位置数组赋给一个临时变量，然后在单独的语句中发送五条消息来重置其内容：

```
| array |
array := Array new: 5.      "Create an array of 5 positions"
array at: 1 put: 10.      "Run a sequence of 5 replacements"
array at: 2 put: 20.
array at: 3 put: 30.
array at: 4 put: 40.
array at: 5 put: 50
```

临时变量写在两条竖线之间，且首字母不大写。语句之间用句点分隔。与 Lisp 一样，Smalltalk 变量没有指定的数据类型；任何变量都可以引用任何对象。还要注意，Smalltalk 的赋值运算符 `:=` 的写法与 Pascal 和 Ada 相同。

当一串消息发送给同一个对象时，我们可以使用分号来级联这些消息：

```
| array |
array := Array new: 5.      "Create an array of 5 positions"
array at: 1 put: 10;      "Run a sequence of 5 replacements, cascaded"
    at: 2 put: 20;
    at: 3 put: 30;
    at: 4 put: 40;
    at: 5 put: 50
```

与许多其他语言（Lisp、Java 和 Python）一样，Smalltalk 的变量使用引用语义而非值语义。在引用语义中，变量引用一个对象；而在值语义中（参见 Ada 和 C++ 等语言），变量本身是对象或包含对象。因此，将一个 Smalltalk 变量赋值给另一个变量，并不会像 Ada 或 C++ 那样传递对象本身的副本，而只是建立对同一对象的另一个引用（本质上是一个别名）。复制需要显式实例化一个与原对象具有相同属性的新对象。Smalltalk 包含两个运算符，`=` 用于相等性，`==` 用于对象同一性，以区分这两种关系。下一段代码使用了 Smalltalk 的 `#( )` 表示法来表示数组字面量，说明了它们的用法：

```
| array alias clone |
array := #(0 0).      "Create an array containing two integers"
alias := array.       "Establish a second reference to the same object"
clone := #(0 0).      "Create a copy of the first array object"
array == alias.       "true, they refer to the exact same object"
array = alias.        "true, because they are =="
array = clone.        "true, because they refer to distinct objects with"
                      "the same properties"
array == clone        "false, because they refer to distinct objects"
clone at: 1 put: 1.   "The second array object now contains 1 and 0"
array = clone         "false, because the two array objects no longer"
                      "have the same properties"
```

引用语义中的对象共享提高了面向对象程序的效率，但代价是可能因别名而带来安全问题。对于函数式语言来说这不是问题，因为它们不允许对对象产生副作用。

理想情况下，初始化数组元素的代码应该以循环方式运行，这样对任意大小的数组都适用。下一个代码段展示了一个 `to:do` 循环，它把数组中每个位置的对象设置为一个新值。这个循环类似于其他语言中基于索引的 for 循环。

```
| array |
array := Array new: 100.      "Instantiate an array of 100 positions"
1 to: array size do: [:i |      "Index-based loop sets the element at each i"
    array at: i put: i * 10]
```

`to:do:` 消息被发送给一个整数，该整数表示迭代的下界。与关键字 `to:` 关联的参数也是一个整数，表示迭代的上界（在本中是数组的大小）。与关键字 `do:` 关联的参数是一个 Smalltalk 块。块用方括号 `[]` 括起来，是一个包含代码的对象，这些代码在每次循环迭代时执行。块类似于 Scheme 中的 lambda 形式，因为它们可以包含以块变量形式出现的参数。我们示例中的 `to:do:` 块包含块变量 `i`，在循环执行期间，它会接收下界和上界之间的每个值。在每次 `to:do:` 循环中，Smalltalk 都会向该块发送 `value:` 消息，并将序列中的下一个数字作为参数。块中的其余代码可以是任意语句序列。如你所见，在 Smalltalk 中，甚至控制语句也是通过消息传递来表达的。

其他类型的控制语句，如 if/else 语句和 while 循环，在 Smalltalk 中也是通过关键字消息来表达的。下一个代码段使用 `ifTrue:ifFalse:` 消息将数组中奇数位置的元素设置为 1，偶数位置的元素设置为 2：

```
| array |
array := Array new: 100.      "Instantiate an array of 100 positions"
1 to: array size do: [:i |      "Treat odd and even positions differently"
    i odd
        ifTrue: [array at: i put: 1]
        ifFalse: [array at: i put: 2]]
```

`ifTrue:ifFalse:` 消息的接收者必须是 Boolean 对象。两个参数是代码块，表达了 if/else 逻辑中的替代操作路径。接收者对象根据自身状态（true 或 false）只评估两个块中的一个。注意，在此示例中，临时变量 `array` 和块变量 `i` 的作用域包含任何嵌套块。

由于 `to:do:` 循环消息是发送给一个数字的，实现其方法的代码位于 `Number` 类中。我们稍后会讨论为类定义方法，但这里有一个预览，显示 `to:do:` 实际上只是对更繁琐的、计数控制的 `whileTrue:` 循环的语法糖：

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

在此方法定义上下文中，符号 `self` 指的是消息的接收者，在此例中为一个数字。`whileTrue:` 消息关联了两个块。与 `ifTrue:ifFalse:` 消息不同，其接收者对象只被评估一次，`whileTrue:` 消息必须以块作为其接收者对象。Smalltalk 评估此块，其中包含一个布尔表达式，一次或多次，直到它返回 false。每次第一个块评估为 true 时，第二个块（`whileTrue:` 的参数），即循环体，也会被评估。此第二个块中的代码包含两个语句。第一个语句通过发送 `value:` 消息来评估 `aBlock`（此处正在定义 `to:do:` 方法的参数）。在循环过程中，此消息的参数 `index` 会取到 `self` 与 `aNumber` 之间序列中每个数字的值。第二个语句递增 `index` 以实现此效果。

本小节中的最后一个示例代码段展示了如何将数组的内容打印到 transcript 窗口。代码使用 `do:` 循环遍历数组。这里我们不关心在数组的索引位置替换元素，而只是访问元素本身。`do:` 循环按顺序访问数组的每个元素，从第一个到最后一个。每次循环遍历时，块参数会被评估，块变量绑定到当前元素。

```
array do: [:element | "Print to transcript each element followed by a return"
    Transcript nextPutAll: element printString; cr]
```

全局变量 `Transcript` 指 Smalltalk 的 transcript 窗口对象。`nextPutAll` 消息期望一个字符串作为参数，因此我们使用 `printString` 消息获取元素的字符串表示，然后将其发送到 transcript。此消息还要求 transcript 显示一个回车字符。

Smalltalk 包含许多类型的集合类以及用于对集合执行迭代的不同类型的消息，例如 `map` 和 `filter`，与函数式语言类似。我们稍后会讨论其中一些操作，也称为 **iterators**。

正如这些简短示例所示，大多数 Smalltalk 代码都由创建适当类的对象并向其发送消息组成。对象本身处理大部分算法细节。剩下的软件开发工作则在于为合适的工作选择合适的类并学习其接口。当此类类尚不存在时，Smalltalk 程序员会创建新的类来自定义现有类。为了了解这是如何完成的，我们现在探索 Smalltalk 庞大的内置类层次结构中的两个类别的类：magnitudes 和 collections。

## 5.2.2 The Magnitude Hierarchy

一个类提供了对象集合的属性和行为的定义。在 Smalltalk 中，内置类以树状层次结构组织，根部有一个名为 `Object` 的单一类。`Object` 下的每个类都继承其在层次结构中祖先类中定义的任何属性和行为。层次结构中的类通常从更一般到更具体地下降，每个新类都会增加和/或修改其上方类中已有的行为和/或属性。**Inheritance**，因此支持结构和行为的重用。**Polymorphism**，或对不同类请求类似服务的消息使用相同名称，也是一种代码重用形式。在本节中，我们检查 Smalltalk 的 magnitude 类的一部分，如图 5.1 的类图中所示。

![](img/062750ade02e28185b1fb8e8cf6dc89e_156_0.png)

正如您从图 5.2 中看到的，magnitude 类包括其他语言中常见的数字类型，如 `Integer`、`Float` 和 `Fraction`，以及与数值相关的一些其他类型，如 `Time` 和 `Date`。这些类有时被称为 **concrete classes**，
