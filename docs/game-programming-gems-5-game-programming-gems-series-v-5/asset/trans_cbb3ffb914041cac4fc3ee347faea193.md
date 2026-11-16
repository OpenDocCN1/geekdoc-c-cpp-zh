
![](img/672fe9a2d008ba627b1991e15d70f43e_372_0.png)

## 图 3.4.1 达到目标状态的计划示例

谓词逻辑会将相同的陈述表示为一个以对象为参数的布尔函数。我们的示例将变成类似 carrying(Bob, key) 的形式。这允许使用更加简洁的规划语言，并被大多数当代规划器采用。谓词逻辑是最著名的规划器 STRIPS [Fikes71] 的基础。STRIPS 规划语言至今仍在使用，并有许多变体和扩展。目前最广泛接受的规划语言是 PDDL，被大多数当代研究规划器采用 [McDermott98]。PDDL 使用类似 LISP 的语法，在游戏行业中并不广泛使用，因此我们开发了自己的语法和解析器，更适合整个行业，并且对可能只有有限编程经验的设计师来说更易读。

## 对象

谓词逻辑描述了一组对象上的真理陈述。对象是构成世界的实体。在我们之前的示例中，对象将包括“Bob”、“key”、“silver plate”、“den”、“kitchen”等。这些示例与面向对象（OO）意义上的对象不同；它们没有方法或任何关联的动态。然而，将规划对象与 OO 游戏引擎对象一对一关联是非常自然的（甚至是可取的），这样规划器提出的动作就可以直接转换为游戏对象操作。

对象确实具有类型，这与面向对象框架类似。这种机制提供了类型检查，因此可以在开发早期捕获错误。我们允许多重类型继承，因此类型形成一个格。我们识别一种特殊类型，“Object”，通常称为通用类型，所有其他类型都从中继承。这引出了第一种语句，用于向规划器声明类型。

```
type Locatable;
type Location;
type Creature isa Locatable;
type Person isa Creature;
type Item isa Locatable;
type Key isa Item;
type ValuablePlate isa Item, Decoration; // multiple inheritance
```

声明类型后，我们可以声明对象。

```
object alice isa Person;
object bob isa Person;
object cabinetkey isa Key;
object silverplate isa ValuablePlate;
object kitchen isa Location;
object den isa Location;
```

## 谓词

谓词帮助我们陈述关于世界中对象的事实。它们将对象元组映射为真或假值。例如，我们可以有一个名为 carrying 的谓词，它接受两个参数，第一个是 Creature，第二个是 Item。我们现在可以表达诸如 carrying(bob, cabinetkey) 或 carrying(bob, silverplate) 的想法。

以谓词形式表达的事实构成了我们规划器中的状态。状态只是关于世界的所有事实的集合。通常，我们只存储世界中的真事实：即求值为真的谓词。其他所有谓词表达式都被假定为假。这被称为封闭世界假设，其动机在于预期世界中假的谓词会比真的多，因此存储真实的谓词更高效。

使用谓词有几种不同的方式。在某些情况下，我们会断言谓词，使我们的表达式在当前状态中为真。因此，我们可能会断言 carrying(bob, cabinetkey) 以将该事实添加到状态中。或者，我们可以将谓词用作查询：“Bob 正在携带柜子钥匙吗？”如果这是当前状态中的一个事实，谓词将返回真。

在我们的规划语言中，谓词的参数具有类型，并且必须显式声明谓词。

```
predicate carrying(Creature, Item);
predicate inroom(Locatable, Location);
```

## 变量

谓词捕获对象之间的关系。我们可以询问某个关系是否存在，但我们可以进一步询问关系集。这是通过变量完成的。例如，如果我们想要 Bob 携带的物品列表，可以查询 carrying(bob, ?x)，其中 ?x 是我们用来指示 x 是变量的表示法。

将此过程视为模式匹配是最容易理解的。查询会检查状态中的所有 carrying 事实，只选取第一个参数为 Bob 的那些事实，并依次将 x 设置为第二个参数的每个值。如果查询找到一个或多个合适的匹配，它将为每个匹配返回真，并相应地绑定变量。

## 逻辑连接词

使用合取（逻辑 AND）和否定（逻辑 NOT），我们可以创建更有趣的查询。例如，我们可以检查 Bob 和钥匙是否在同一个房间中：

```
inroom(bob, ?x) and inroom(cabinetkey, ?x)
```

在这里，第一个 inroom() 查询找到与 Bob 对应的匹配，并将 ?x 绑定到 kitchen。第二个查询现在变为 inroom(cabinetkey, kitchen)。

还允许一种特殊的谓词来表示不等式，仅当其两个参数是不同对象时才为真；例如：?x != ?y。

## 算子

我们使用算子将一个状态转换为另一个状态。在最简单的形式中，算子具有前置条件（在执行动作前必须为真的查询）和效果（要对世界进行的一组更改）。两者都可以使用由谓词、合取和否定组成的简单逻辑表达式来陈述。

```
operator take(Creature ?c, Item ?i)
precondition: inroom (?c, ?r) and inroom(?i, ?r)
effect: not inroom (?i, ?r) and carrying(?c, ?i);
```

此算子接受两个参数（注意它们的类型）。前置条件指出生物必须与物品在同一位置。效果创建一个新状态，与原始状态相同，移除物品在房间中的事实，并添加生物正在携带物品的事实。

> 请注意，?r 变量不是算子的参数之一。这是因为它对动作并非真正必要，只是我们执行动作所需了解的一些信息。可以将其视为算子的局部变量。当游戏引擎需要实际执行动作时，它只需要知道生物和物品。

有了算子后，我们可以检查状态并通过测试每个动作的前置条件来自动确定哪些动作是可能的。每个算子的每个前置条件匹配都是一个可能的动作。现在我们拥有搜索计划所需的一切，除了实际的搜索算法。

## 多代理规划器示例

将所有这些结合起来，我们可以看一个清晰展示规划器强大功能的简单示例。在此示例中，我们创建一个具有平凡解的状态，然后将问题扩展到需要两个代理协作才能解决的问题。

```
type Locatable;
type Location;
type Creature isa Locatable;
type Person isa Creature;
type Dog isa Creature;
type Container isa Locatable;
type Item isa Locatable;
type Key isa Item;
type Plate isa Item;
type ValuablePlate isa Plate, Decoration;
// multiple inheritance
// type Food isa Item;
```

声明类型后，我们可以声明对象。

```
object alice isa Person;
object bob isa Person;
object cabinetkey isa Key;
object silverplate isa ValuablePlate;
object kitchen isa Location;
object den isa Location;
object cabinet isa Container;
object nelly isa Dog;
object lasagna isa Food;
object fridge isa Container;
```

```
predicate inroom(Location ?a, Location ?b);
// Object is in location
predicate carrying(Creature ?c, Item ?i);
// Creature carries item
predicate locked(Container ?c);
// Container is locked
predicate unlocked(Container ?c);
// Container is unlocked
predicate haskey(Creature ?c, Key ?k);
// Creature has key
predicate hungry(Creature ?c);
// Creature prepared
predicate prepared(Food ?f);
// Food is prepared
predicate inside(Item ?i, Container ?c);
// Item is inside container
```

```
// Pick up something in the room.
operator take(Person ?p, Item ?i)
precondition: inroom(?p, ?r) and inroom (?i, ?r)
effect: not inroom (?i, ?r) and carrying(?p, ?i);
```
