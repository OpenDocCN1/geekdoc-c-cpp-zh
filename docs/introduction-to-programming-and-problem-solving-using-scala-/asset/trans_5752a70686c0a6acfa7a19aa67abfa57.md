

# 面向对象 491

强制程序员使用这些函数。程序员可能会在某处变得“偷懒”，直接访问余额。这套银行软件的结果可能是灾难性的。

通过特定方法访问数据的能力是面向对象编程最重要的能力之一，它是改进软件构建和控制复杂性的方法。这种能力的真正用处是将正确用的责任从对象用户手中转移开。如果使用对象的唯一方式是通过方法或专为他们准备的数据，那么他们就不会弄乱它，也不需要担心这一点。相反，他们可以专注于自己正在处理的逻辑。

我们如何在类中实现这一点呢？我们通过设置成员的可见性来实现。Scala 中有三个主要的可见性级别，它们与你在其他面向对象的语言中看到的非常相似。

- Public（公共） - 意味着任何代码索引或类外部都可以访问它。在 Scala 中，这是元素的默认可见性，因此没有对应的关键字。

- private（私有） - 意味着该成员只能在类内部访问。从类外部访问该成员将导致语法错误。如果你在类中的声明前加上 `private` 关键字，该成员将是私有的。

- protected（受保护） - 这类似于 private，但受保护的成员在子类中也是可见的。这些细节超出了本书的范围，但在《使用 Scala 的面向对象、抽象和数据结构[1] 中会有讨论。

在我们的示例 `Account` 中，我们希望余额是私有的。我们可以简单地在 `var` 之前添加 `private` 来实现。

```scala
class Account {
  var balance = 0
}
```

遗憾的是，这让我们拥有了一个完全没用的类。在进行此更改之前，我们可以执行如下操作。

```scala
val myAccount = new Account
println(myAccount.balance)
myAccount.balance += 10
println(myAccount.balance)
```

如果我们现在这样做，我们会得到一组错误消息。

```scala
ScalaS1/Chapters/ObjectOrientation/Code/Bank.scala:6: error: variable balance in
class Account cannot be accessed in this.Account
println(myAccount.balance)
```

```scala
ScalaS1/Chapters/ObjectOrientation/Code/Bank.scala:7: error: variable balance in
class Account cannot be accessed in this.Account
myAccount.balance += 10
```

```scala
ScalaS1/Chapters/ObjectOrientation/Code/Bank.scala:8: error: variable balance in
class Account cannot be accessed in this.Account
println(myAccount.balance)
```

发现了三个错误。

# 使用 Scala 进行编程与问题解决导论

注意这个错误信息与我们之前在 `Student` 类中看到的 `name` 错误不同。它没有告诉我们 `balance` 不是成员，而是告诉我们 `balance` 无法被访问。这是因为 `balance` 是私有的，而代码在类外部。

为了让这个类有用，我们需要在其中放置一些公共方法，以允许操作余额。我们在银行设计中了三个这样的方法。我们从 `deposit`（存款）和 `withdraw`（取款）方法开始。以下是 `deposit` 方法可能的样子。注意它是缩进的，因为它出现在 `Account` 类内部。

```scala
def deposit(amount:Int):Boolean = {
  if (amount > 0) {
    balance += amount
    true
  } else false
}
```

该方法接收要存款的金额作为 `Int`。它返回一个 `Boolean` 来告诉我们存款是否成功。此方法不支持日志记录，因为在目前阶段添加比我们想要的更深的功能。它确实会检查存款金额是否为正。如果是，则将金额加到 `balance` 中并将结果为 `true`；否则，什么都不做，结果为 `false`。我们可以添加一个看起来非常相似的 `withdraw` 方法。

```scala
def withdraw(amount:Int):Boolean = {
  if (amount > 0 && amount <= balance) {
    balance -= amount
    true
  } else false
}
```

`deposit` 和 `withdraw` 之间的区别在于你不能提取超过你拥有的钱，并且金额会从 `balance` 中减去。

我们最后需要添加一个获取余额的方法以便进行检查。在 Scala 中，这种方法的正确风格是将方法命名为 `balance`，并将私有成员命名为 `_balance`。这将使我们的类看起来如下。

```scala
class Account {
  private var _balance = 0

  def deposit(amount:Int):Boolean = {
    if (amount > 0) {
      _balance += amount
      true
    } else false
  }

  def withdraw(amount:Int):Boolean = {
    if (amount > 0 && amount <= _balance) {
      _balance -= amount
      true
    } else false
  }

  def balance = _balance
}
```

# 面向对象

`balance` 方法简单地返回账户中 `_balance` 的值。我们可以通过以下方式来利用这段代码。

```scala
val myAccount = new Account
println(myAccount.balance)
myAccount.deposit(100)
println(myAccount.balance)
```

注意，由于使用了 `balance` 这个名字，`println` 语句显示的方式与 `balance` 是公共 `var` 时相同。区别在于，现在除非通过 `deposit` 方法或 `withdraw` 方法，否则你无法设置 `balance`。

我们原始的设计包含了另一个方法和更多的数据成员。示例中的这些额外元素，有些也将是。

## 面向对象

`balance` 方法简单地返回账户中 `_balance` 的值。我们可以通过以下方式来利用这段代码。

```scala
val myAccount = new Account
println(myAccount.balance)
myAccount.deposit(100)
println(myAccount.balance)
```

注意，由于使用了 `balance` 这个名字，`println` 语句显示的方式与 `balance` 是公共 `var` 时相同。区别在于，除非通过 `deposit` 方法或 `withdraw` 方法，否则你无法设置 `balance`。

我们原始的设计包含了另一个方法和更多的数据成员。示例中的这些额外元素，有些也将是。

### 特殊方法

`balance` 方法简单地返回账户中 `_balance` 的值。我们可以通过以下方式来利用这段代码。

```scala
val myAccount = new Account
println(myAccount.balance)
myAccount.deposit(100)
println(myAccount.balance)
```

注意，由于使用了 `balance` 这个名字，`println` 语句显示的方式与 `balance` 是公共 `var` 时相同。区别在于，除非通过 `deposit` 方法或 `withdraw` 方法，否则你无法设置 `balance`。

我们原始的设计包含了另一个方法和更多的数据成员。示例中的这些额外元素，有些也将是。

### 赋值方法

`balance` 方法简单地返回账户中 `_balance` 的值。我们可以通过以下方式来利用这段代码。

```scala
val myAccount = new Account
println(myAccount.balance)
myAccount.deposit(100)
println(myAccount.balance)
```

注意，由于使用了 `balance` 这个名字，`println` 语句显示的方式与 `balance` 是公共 `var` 时相同。区别在于，除非通过 `deposit` 方法或 `withdraw` 方法，否则你无法设置 `balance`。

我们原始的设计包含了另一个方法和更多的数据成员。示例中的这些额外元素，有些也将是。

这种方法的优势在于在 Scala 中：

- _balance = b

- _balance = b

- _balance = b

- _balance = b

- _balance = b

的 _ 的 = the

 是，有情况要。

