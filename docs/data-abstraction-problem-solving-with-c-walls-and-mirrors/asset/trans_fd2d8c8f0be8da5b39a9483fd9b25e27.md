

# UML 类图 745

图 C-3 银行类的三种可能的类图

![](img/d0cb86b2f18b2db569968ad7c743510e_771_0.png)

类图以一种独立于语言的方式表示对象类的概念模型。这意味着，该图并不规定类的具体实现方式。它只是为你提供了一个可以作为依据的设计。然而，你可以作为选项指定许多与类的属性和操作相关的特性。这些特性在 C++ 中很容易实现，并且它们增加了设计中提供的信息量。

类属性的 UML 语法为：
`[visibility] name [type]=defaultValue[{property}]`

其中

-   * 括号内的所有元素都是可选的。
-   visibility（可见性）可以是 + 表示公共访问、- 表示私有访问或 # 表示受保护访问。（C++ 间插 4 涵盖了受保护访问）。如果省略，可见性默认为私有访问。
-   name 是属性的名称。
-   type 是属性的数据类型。
-   defaultValue 是属性的默认值。
-   property 指明适用于此属性的某些属性。

至少应该定义一个属性。只有在设计规定该属性具有合适的默认值时，才会给出 defaultValue。在某些情况下，省略属性类型可能是合适的，将此决策推迟到实现阶段。

UML 规定属性类型应使用独立于语言的名称。本文将遵循 UML 建议，使用 integer 用于整数存储，使用 float 用于浮点数存储，使用 bool 用于布尔存储，使用 string 用于字符串字符串。
属性的 property 可以有以下值之一：

-   * changeable 表示一个普通的、可修改的属性，通常会被省略。
-   frozen 表示常量或只写一次的属性。

图 C-3b 中 Bank 类的属性可以写为：
-name: string
-routingNum: integer

这些属性的可见性遵循了面向对象编程中的信息隐藏原则。

类操作的 UML 语法更为复杂：
`[visibility] name ([parameterList]) [type]{[property}]`

其中

-   - 方方括号内的所有元素都是可选的。
-   visibility 与属性指定的相同，但如果省略操作，则操作默认为公共访问。
-   name 是操作的名称。
-   type 是操作返回的结果的数据类型。如果操作不返回任何，type 可以省略或指定为 void。此处应用的独立语言的类型与属性类型相同。
-   property 指明适用于此操作的某些属性。与其相关的唯一属性是 query，表示该操作不会修改调用对象中的任何数据成员。
-   parameterList 可以是空的——参数仍然是必须的——或者包含一个用逗号分隔的操作参数列表。每个参数的语法如下：

```
[direction]name:type[=defaultValue]
```

其中

-   - 方方括号内的所有元素都是可选的。
-   direction 显示参数是用于输入 (in)、输出 (out) 还是输入输出都是 (inout)。
-   name 是参数的名称。
-   type 是参数的数据类型。此处应用的独立语言的类型与属性类型相同。
-   defaultValue 是当调用此操作时未提供实际参数，该参数的值。

在图 C-3b 中，Bank 操作可以写为：
+authorize(in name: string, in identifier: string): void {query-createAccount()}

authorize 操作具有公共访问权限，而 createAccount 操作是私有的。由于 authorize 操作的设计指定了 query 属性，此操作不会更改调用对象中的任何数据。

UML 为类图中的类提供了几种类型的关系。例如，图 C-4 显示了银行系统的静态（类）图。由于银行为客户提供支票账户和储蓄账户，该图显示了五类对象类：Bank 类、Customer 类、Account 类、Checking 类和 Savings 类。这些类通过相互发送消息来相关联。通过这些协作，类之间以各种方式相互关联。

例如，Bank 和 Customer 之间存在关联关系，由没有箭头的实线表示。关联末端的数字是重数（multiplicities）。每个银行都与两个或多个客户关联，但每个客户只关联一个账户。每个客户可以有多种账户，而每个账户只能属于一个客户。

Bank Account 关系属于部分/整体关系的一种类型，称为聚合（aggregation）或包含（containment）关系，它由包含类附近的菱形箭头表示。在聚合关系中，被包含对象的生命和包含对象的生命周期并不一定相同。银行的“寿命”比它们包含的账户要长。部分/整体关系称为组合（composition），使用包含类附近的实心菱形箭头。这

关联表示类之间相互彼此

聚合表示一个类包含另一个类的实例

# UML 类图 747

图 C-4 银行系统的 UML 类图

| Bank | 1 |
| --- | --- |
| -name: string | |
| -routingNum: integer | |
| -createAccount() | |
| | 0..* |
| Account | 0..* |
| -accountNum: integer | |
| -balance: float | |
| +getBalance(): float (query) | |
| +withdraw(in accountNum: integer, in amount: float): boolean | |
| +deposit(in accountNum: integer, in amount: float): boolean | |

| Checking | Savings |
| --- | --- |
| -chargePerCheck: float | -interestRate: float |
| -numCheck: float | -accrualInterest() |
| -minBalance: float | +getBalance(): float (query) |
| +getBalance(): float (query) | |

| Customer | |
| --- | |
| -name: string | |
| -address: string | |
| +getName(): string (query) | |
| +changeName(newName: string) | |
| +getAddress(): string (query) | |
| +changeAddress(newAddress: string) | |

关系描述了一种更强的连接，当容器和被包含对象的生命周期相同时。例如，圆珠笔是一种尖端有一个球的笔。当笔“死亡”时，球也随之死亡。笔和它的球处于组合关系。通过观察重数，我们可以说它包含——零或多个账户。Customer 和 Account 类之间是聚合关系。

每个银行账户都存储其账号和余额，并允许客户查询当前余额、提取资金和存款。Account 类指定了所有账户通用的属性和操作。Account 与 Checking 和 Savings 类通过泛化关系相关联，由指向通用（或父类）类的空三角形箭头表示。泛化关系表示继承。祖类的属性和操作被后代类 Checking 和 Savings 继承。

注意图 C-4 中的 Account 类是斜体。这表示一个抽象类。Account 类中的 getBalance 操作也是斜体。这表示 getBalance 在 Account 类中没有实现，但必须在后代类中实现。事实上，Checking 和 Savings 类都实现了被继承的 getBalance 操作。当从父类对象调用时，该操作将表现出多态行为。设计和实现方面的许多要点将在 C++ 间插 4 中进行详细介绍。

> 注意：UML 类图（静态图）

-   显示单个类的属性和操作
-   显示系统中类之间不变的关系

