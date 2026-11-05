
> CHRIS SELLS 我发现自己很少使用数组——即使是单维数组，更不用说多维或锯齿数组了——因此那些奇怪的边界情况通常无关紧要。鉴于 List<T>、Dictionary<K, V> 和 IEnumerable<T> 的可用性，如果完全没有数组我也会很开心。

> PETER SESTOFT Eric 抱怨的运行时检查的必要性源于数组类型在元素类型上是协变的（当 Student 是 Person 的子类型时，Student[] 是 Person[] 的子类型）。这种数组协变的设计缺陷与 Java 编程语言共用，在 Java 中情况甚至更糟：因为 Java 通过类型擦除实现泛型，运行时不存在表示泛型类型参数的类型对象，因此如果数组是作为 new T[...] 为某个类型参数 T 创建的，或作为 new Stack<Person>[...] 创建的，则无法执行检查。因此 Java 必须禁止创建元素类型为类型参数或作为泛型类型的类型实例构造的类型 的数组。在 C# 中，类型参数和构造类型在运行时得到忠实表示，因此这些限制对数组创建并不存在。

> 在 Scala 语言中，该语言诞生时就带有泛型类型，数组类型在元素类型上是不变的，因此不需要运行时检查（但在 Scala 编译为 Java 字节码时很可能会仍然执行）。

> BILL WAGNER Eric 的评论在很大程度上解释了为什么 C# 4.0 为泛型添加的安全协变和逆变如此重要。用同一次更改同时提高速度和正确性通常是很少见的。

数组协变特指不扩展到值类型的数组。例如，不存在允许将 int[] 视为 object[] 的转换。

## 12.6 数组初始化器

数组初始化器可在字段声明 (§10.5)、局部变量声明 (§8.5.1) 和数组创建表达式 (§7.6.10.4) 中指定：

```
array-initializer:
{ variable-initializer-list_opt }
{ variable-initializer-list , }
```

```
variable-initializer-list:
    variable-initializer
    variable-initializer-list  ,  variable-initializer

variable-initializer:
    expression
    array-initializer
```

数组初始化器由一系列变量初始化器组成，用“{”和“}”标记括起来，并用“,”标记分隔。每个变量初始化器是一个表达式，或者在多维数组的情况下，是一个嵌套的数组初始化器。

在数组初始化器被使用的上下文决定了正在初始化的数组的类型。在数组创建表达式中，数组类型紧跟在初始化器之前，或从数组初始化器中的表达式推断得出。在字段或变量声明中，数组类型是正在声明的字段或变量的类型。当数组初始化器在字段或变量声明中使用时，例如

```
int[] a = {0, 2, 4, 6, 8};
```

它只是等效数组创建表达式的简写：

```
int[] a = new int[] {0, 2, 4, 6, 8};
```

对于单维数组，数组初始化器必须由与数组元素类型赋值兼容的表达式序列组成。表达式按递增顺序初始化数组元素，从索引 0 处的元素开始。数组初始化器中表达式的数量决定了正在创建的数组实例的长度。例如，上面的数组初始化器创建一个长度为 5 的 int[] 实例，然后用以下值初始化该实例：

```
a[0] = 0; a[1] = 2; a[2] = 4; a[3] = 6; a[4] = 8;
```

对于多维数组，数组初始化器必须具有与数组中维度一样多的嵌套层级。最外层的嵌套层级对应于最左边的维度，最内层的嵌套层级对应于最右边的维度。数组每个维度的长度由数组初始化器中相应嵌套层级处的元素数量决定。对于每个嵌套的数组初始化器，其元素数量必须与同一层级的其他数组初始化器相同。示例

```
int[,] b = {{0, 1}, {2, 3}, {4, 5}, {6, 7}, {8, 9}};
```

创建一个二维数组，最左边维度的长度为 5，最右边维度的长度为 2：

```
int[,] b = new int[5, 2];
```

然后用以下值初始化数组实例：

```
b[0, 0] = 0; b[0, 1] = 1;
b[1, 0] = 2; b[1, 1] = 3;
b[2, 0] = 4; b[2, 1] = 5;
b[3, 0] = 6; b[3, 1] = 7;
b[4, 0] = 8; b[4, 1] = 9;
```

如果除最右边之外的一个维度被指定为长度 0，则假定后续维度也具有长度 0。示例

```
int[,] c = {};
```

创建一个二维数组，最左边和最右边维度的长度均为 0：

```
int[,] c = new int[0, 0];
```

当数组创建表达式同时包含显式维度长度和数组初始化器时，长度必须是常量表达式，并且每个嵌套层级处的元素数量必须与相应的维度长度匹配。以下是一些示例：

```
int i = 3;
int[] x = new int[3] {0, 1, 2};    // Okay
int[] y = new int[i] {0, 1, 2};    // Error: i not a constant
int[] z = new int[3] {0, 1, 2, 3}; // Error: length/initializer mismatch
```

这里，y 的初始化器导致编译时错误，因为维度长度表达式不是常量，而 z 的初始化器导致编译时错误，因为长度和初始化器中的元素数量不一致。

## 13. 接口

接口定义了一个契约。实现接口的类或结构必须遵守其契约。接口可以继承多个基接口，类或结构可以实现多个接口。

> **BILL WAGNER** 接口在范围小且数量少时效果最佳。较大的接口会给实现者带来更多工作。接口数量越多，产生歧义和冲突的机会就越多。

> **ERIC LIPPERT** 接口是契约这一说法无疑既有用又经常被提及。值得指出的是，接口实际上是表示契约的一种相当薄弱的方式。接口告诉你的全部是哪些方法可用、它们的名字是什么、它们接受哪些类型、返回哪些类型。契约中完全没有表示操作的语义：遵守此契约的对象必须积极处置，Drive() 如果在 StartEngine() 之后未调用则抛出异常，第一个参数必须为 null 且第二个参数必须非零，等等。所有这些内容都写在文档中，而不是分析工具可以挖掘的地方。随 CLR 4.0 版本发布的新的代码契约系统使你既能比单独使用接口更详细地指定契约，又能在编译时对这些契约进行有趣的分析。

接口可以包含方法、属性、事件和索引器。接口本身不为其定义成员提供实现。接口仅指定实现接口的类或结构必须提供的成员。

### 13.1 接口声明

interface-declaration 是声明新的接口类型的 type-declaration (§9.6)。

```
interface-declaration:
    attributes_opt interface-modifiers_opt partial_opt interface
    identifier variant-type-parameter-list_opt interface-base_opt
    type-parameter-constraints-clauses_opt interface-body ;_opt
```

interface-declaration 由一组可选的属性 (§17) 组成，其后是可选的一组接口修饰符 (§13.1.1)，其后是可选的 partial 修饰符，其后是关键字 interface 和一个命名接口的标识符，其后是可选的 variant-type-parameter-list 规范 (§13.1.3)，其后是可选的 interface-base 规范 (§13.1.4)，其后是可选的 type-parameter-constraints-clauses 规范 (§10.1.5)，其后是 interface-body (§13.1.5)，可选地后跟一个分号。

### 13.1.1 接口修饰符

interface-declaration 可选择性地包含一系列接口修饰符：

```
interface-modifiers:
    interface-modifier
    interface-modifier interface-modifier
```

```
interface-modifier:
    new
    public
    protected
    internal
    private
```

在接口声明中，相同的修饰符出现多次是编译时错误。

new 修饰符仅允许在类中定义的接口上使用。它指定接口隐藏了同名继承的成员，如 §10.3.4 中所述。

public、protected、internal 和 private 修饰符控制接口的可访问性。根据接口声明出现的上下文，其中只有某些修饰符可能被允许 (§3.5.1)。

### 13.1.2 partial 修饰符

partial 修饰符表示此 interface-declaration 是一个部分类型声明。封闭命名空间或类型声明中具有相同名称的多个 partial 接口声明组合形成一个接口声明，遵循 §10.2 中指定的规则。
