
你也不再需要用 `m_` 前缀来标识成员变量。你的类和函数应该足够小，以至于不需要它们。并且你应该使用一个能够高亮或着色成员变量的编辑环境，以便区分它们。

```java
public class Part {
    private String m_dsc; // The textual description
    void setName(String name) {
        m_dsc = name;
    }
}
```

```java
public class Part {
    String description;
    void setDescription(String description) {
        this.description = description;
    }
}
```

此外，人们很快就会学会忽略前缀（或后缀），只看名字中有意义的部分。我们读代码越多，就越少看到这些前缀。最终，前缀变成了看不见的杂物和旧代码的标记。

## 接口与实现

## 避免心智映射

读者不应该在脑海中把你的名字转换成他们已经知道的其他名字。这个问题通常源于既没有使用问题领域术语，也没有使用解决方案领域术语的选择。

单字母变量名就是这样一个问题。当然，如果循环计数器的范围非常小，且没有其他名字与之冲突，它可以用 `i`、`j` 或 `k` 命名（但绝不能用 `l`！）。这是因为这些单字母的循环计数器名称是传统习惯。然而，在大多数其他情况下，单字母名称是一个糟糕的选择；它只是一个占位符，读者必须通过心智映射将其映射到实际概念。没有比“因为 `a` 和 `b` 已经被用了”更糟糕的理由来使用 `c` 这个名字了。

总的来说，程序员是非常聪明的人。聪明人有时喜欢通过展示他们的心智杂耍能力来炫耀自己的聪明。毕竟，如果你能可靠地记住 `r` 是去掉了主机和协议的 URL 小写版本，那么你显然一定非常聪明。

聪明程序员和专业程序员之间的一个区别是，专业程序员明白*清晰至上*。专业人士将他们的才智用在正道上，编写他人能够理解的代码。

## 类名

类和对象应该使用名词或名词短语名称，如 `Customer`、`WikiPage`、`Account` 和 `AddressParser`。避免在类名中使用 `Manager`、`Processor`、`Data` 或 `Info` 之类的词。类名不应是动词。

## 方法名

方法应该使用动词或动词短语名称，如 `postPayment`、`deletePage` 或 `save`。访问器、修改器和谓词方法应该根据其值命名，并按照 JavaBean 标准加上 `get`、`set` 和 `is` 前缀。^4

```java
String name = employee.getName();
customer.setName("mike");
```

```java
if (paycheck.isPosted())...
```

当构造函数被重载时，使用名称能描述参数的静态工厂方法。例如，

```java
Complex fulcrumPoint = Complex.FromRealNumber(23.0);
```

通常比

```java
Complex fulcrumPoint = new Complex(23.0);
```

更好。

考虑通过将相应的构造函数设为 `private` 来强制使用它们。

## 不要卖弄聪明

如果名字太过于巧妙，那么只有与作者有同样幽默感的人才能记住它们，而且只有在这些人记得这个玩笑的时候。他们会知道名为 `HolyHandGrenade` 的函数是做什么的吗？当然，这很俏皮，但也许在这种情况下 `DeleteItems` 会是更好的名字。选择清晰而非娱乐价值。

![](img/d3848357ae109884a140c7b3662e0e30_70_0.png)

代码中的俏皮话常常以口语或俚语的形式出现。例如，不要用 `whack()` 来表示 `kill()` 的意思。不要讲那些依赖文化的笑话，比如用 `eatMyShorts()` 来表示 `abort()`。

言必由衷，言必有物。

## 每个概念选择一个词

为每个抽象概念挑选一个词，并坚持使用它。例如，在不同的类中，将 `fetch`、`retrieve` 和 `get` 作为等价的方法会让人困惑。你如何记住哪个方法名对应哪个类？遗憾的是，你常常必须记住是哪个公司、团队或个人编写了该库或类，才能记得使用了哪个术语。否则，你会花大量时间浏览头文件和之前的代码示例。

像 Eclipse 和 IntelliJ 这样的现代编辑环境提供了上下文相关的线索，例如你可以在给定对象上调用的方法列表。但要注意，这个列表通常不会显示你在函数名和参数列表周围写的注释。如果它能给出函数声明中的*参数名*，你就很幸运了。函数名必须能够独立表达意义，并且必须保持一致，以便你无需额外探索就能选对方法。

同样，在同一个代码库中同时存在 `controller`、`manager` 和 `driver` 也会令人困惑。`DeviceManager` 和 `ProtocolController` 之间的本质区别是什么？为什么不是都为 controller 或都为 manager？它们真的都是 driver 吗？这些名字会让你期望两个对象具有非常不同的类型和不同的类。

一致的词汇表对于必须使用你的代码的程序员来说是一个巨大的福音。

## 不要双关

避免使用同一个词来表示两种目的。用同一个术语来表示两个不同的概念本质上是一种双关。

如果你遵循“一个概念一个词”的规则，你可能会得到许多类，例如，都有一个 `add` 方法。只要各种 `add` 方法的参数列表和返回值在语义上是等价的，那就没问题。

然而，当一个人实际上并不是在相同的意义上进行“添加”时，他或她可能会决定使用 `add` 这个单词来保持“一致性”。假设我们有很多类，其中 `add` 通过将两个现有值相加或连接来创建一个新值。现在假设我们正在编写一个新类，该类有一个方法将其单个参数放入一个集合中。我们是否应该将此方法称为 `add`？这看起来可能是一致的，因为我们有很多其他的 `add` 方法，但在这种情况下，语义是不同的，所以我们应该使用诸如 `insert` 或 `append` 之类的名称。将新方法称为 `add` 就是一种双关。

## 添加有意义的语境

想象一下，你有变量名 `firstName`、`lastName`、`street`、`houseNumber`、`city`、`state` 和 `zipcode`。综合来看，很明显它们构成一个地址。但如果你只看到 `state` 变量在某个方法中单独使用，你会自动推断它是地址的一部分吗？

你可以通过使用前缀来添加上下文：`addrFirstName`、`addrLastName`、`addrState` 等等。至少读者会理解这些变量是更大结构的一部分。当然，更好的解决方案是创建一个名为 Address 的类。然后，即使是编译器也知道这些变量属于一个更大的概念。

考虑 [清单 2-1](#listing-2-1) 中的方法。这些变量需要更有意义的上下文吗？函数名只提供了部分上下文；算法提供了其余的部分。当你通读这个函数，你会看到 `number`、`verb` 和 `pluralModifier` 这三个变量是“猜测统计”消息的一部分。不幸的是，上下文必须被推断出来。当你第一次看到这个方法时，这些变量的含义是晦涩难懂的。

### 清单 2-1 上下文不明确的变量。

```java
private void printGuessStatistics(char candidate, int count) {
    String number;
    String verb;
    String pluralModifier;
    if (count == 0) {
        number = "no";
        verb = "are";
        pluralModifier = "s";
    } else if (count == 1) {
        number = "1";
        verb = "is";
        pluralModifier = "";
    } else {
        number = Integer.toString(count);
        verb = "are";
        pluralModifier = "s";
    }
}
```
