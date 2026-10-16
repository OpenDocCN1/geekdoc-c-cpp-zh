
向对象发送消息有点像在函数式语言中调用函数。然而，一些被称为**修改器**的消息可能会导致接收方对象的状态发生变化，而函数调用只是向调用者返回一个值。发送和接收消息的过程也称为**消息传递**。对象能够识别的消息集合有时被称为它的**接口**。

Smalltalk 的消息传递语法相当简单，但有些不合常规。接收消息的对象写在最前面，后面跟着消息名称（也称为**选择器**）和任何参数。在包含对象和消息的表达式中，各元素通常从左到右读取和求值。例如，我们可以通过向 Smalltalk 内置的 Set 类发送 `new` 消息来创建一个新的集合对象，如下所示：

```
Set new    "Returns a new set object"
```

注意，类名首字母大写，消息名首字母不大写。Smalltalk 的注释用双引号括起来。本小节中的任何代码示例都可以通过将它们输入到 Smalltalk 的 Transcript 窗口，并从 **Smalltalk** 菜单中选择 **显示它** 选项来进行求值。整个讨论中，我们使用 Smalltalk/V 语法。

我们可以通过向这个对象发送 `size` 消息来检查新集合中的元素数量：

```
Set new size    "Returns 0"
```

在这段代码中，Set 类接收 `new` 消息，该消息返回一个 Set 实例，和之前一样。这个对象接着接收 `size` 消息，该消息返回一个整数对象。`new` 消息也称为**类消息**，因为它是发送给类的；而 `size` 消息称为**实例消息**，因为它是发送给类的实例的。这些消息也是**一元消息**的示例，因为它们不期望任何参数。

需要参数的消息称为**关键字消息**。例如，我们可以通过向新集合发送 `includes:` 消息来查看它是否包含给定元素。这个消息期望一个参数，即搜索的目标对象。在下一个示例中，集合被询问是否包含字符串 'Hello'：

```
Set new includes: 'Hello'    "Returns false"
```

注意，关键字消息的名称以冒号（`:`）结尾。如果参数多于一个，则每个参数前面必须另有其他关键字。关键字消息的参数在消息发送之前会被求值。下面的示例向一个新的集合对象添加一个字符串：

```
Set new add: 'Ken'    "This set now includes 'Ken'"
```

`add:` 消息是**修改器**的一个示例，它改变接收方对象的状态。

一个稍微复杂的示例创建一个包含 10 个元素的新数组，并将值 66 存储到数组的第一个位置。代码首先向 Array 类发送类消息 `new:`，以实例化一个有 10 个位置的数组（每个位置包含默认值 `nil`）。然后这个数组接收实例消息 `at:put:`，将整数存储到数组的第一个位置。

```
(Array new: 10) at: 1 put: 66    "Stores 66 at the first position in the array"
```

关键字消息 `at:put:` 期望两个参数。第一个参数是数组中某个对象的索引。第二个参数是要放置在该索引处的对象。一元消息的优先级高于关键字消息，可以使用括号来提高清晰度或覆盖优先级。注意，最后一个示例需要括号来区分两个关键字消息。如果没有括号，解释器会把 `new:at:put` 视为 Array 类的类消息。这会产生一个无法识别的消息错误。

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

`to:do:` 消息被发送给一个整数，该整数表示迭代的下界。与关键字 `to:` 关联的参数也是一个整数，表示迭代的上界（在本例中是数组的大小）。与关键字 `do:` 关联的参数是一个 Smalltalk 块。块用方括号 `[]` 括起来，是一个包含代码的对象，这些代码在每次循环迭代时执行。块类似于 Scheme 中的 lambda 形式，因为它们可以包含以块变量形式出现的参数。我们示例中的 `to:do:` 块包含块变量 `i`，在循环执行期间，它会接收下界和上界之间的每个值。在每次 `to:do:` 循环中，Smalltalk 都会向该块发送 `value:` 消息，并将序列中的下一个数字作为参数。块中的其余代码可以是任意语句序列。如你所见，在 Smalltalk 中，甚至控制语句也是通过消息传递来表达的。

其他类型的控制语句，如 if/else 语句和 while 循环，在 Smalltalk 中也是通过关键字消息来表达的。下一个代码段使用 `ifTrue:ifFalse:` 消息将数组中奇数位置的元素设置为 1，偶数位置的元素设置为 2：
