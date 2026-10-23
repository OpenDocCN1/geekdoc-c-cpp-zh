

更重要的是，如果该方法抽象且你未实现它，除非将类标记为 abstract，否则会产生语法错误。

为了帮助你理解这个第二个原因，让我们看一个 Scala 在你重写方法时为何首先要求 override 关键字的例子。考虑 Rectangle 的这个版本。

```
class Rectangle(val width: Double, val height: Double, c: Color) extends Shape(c) {
  def area: Double = width * height
  def circumference: Double = 2.0 * (width + height)
  override def draw(g: Graphics) { // ERROR: Not really an override
    g.setPaint(color)
    g.fill(new Rectangle2D.Double(0.0, 0.0, width, height))
  }
}
```

override 关键字已从 area 和 circumference 中去掉，因为它们在超类型中是抽象的。draw 方法上有一条注释告诉你它无法编译。你能看出哪里错了吗？这里有一个非常微妙的错误，大多数人如果没有注释会忽略它，即使有注释，你也可能很难识别出来。错误在于 `g` 被列为 Graphics 类型而不是 Graphics2D。编码时出现这种小笔误很容易，如果它不是语法错误，就可能产生很难追踪的逻辑错误。Scala 在这种用法中要求 override，这样如果你更改了类型，就会成为语法错误。在 override 不是必需的情况，即超类型中的方法是抽象的，参数或方法名的笔误会使该方法未实现，这会产生不同的错误，指出类必须为 abstract，因为某个方法是抽象的。

## 19.2.6 traits

class 和 object 构造并不是在 Scala 中创建新类型的唯一方式。第三种选择，对本章而言很重要，是 trait。trait 在很多方面都非常类似于抽象类。两个主要区别是 trait 不能接受参数，并且你可以继承多个 trait。

上面没有明确说明，但你可能已经注意到没有描述如何在 extends 之后列出多个类。这不是疏忽，你不允许在那里列出多个类。你可以让类后面跟多个 trait，或者只有一个或多个 trait。你继承的各种类型由 with 关键字分隔。

为了理解你为什么会想要这样做，请考虑以下示例。想象你在编写软件来模拟人们在建筑物中的移动，以帮助设计空间。你有一个名为 Person 的类型，表示模拟中可以出现的每个人。你工作的公司知道有某些类别的人，其行为与模拟必须处理的方式显著不同。例如，他们需要 Parent、Child 和 GeneralAdult 的类型。出于建筑设施的需求，他们还需要 Male 和 Female 的类型。这最后一部分为单继承带来了问题，因为你希望能够通过继承 Parent 和 Male 来表示 Father 类型。子类型关系在那里是有意义的，但如果这两个类型都写成类，你将无法同时使用它们。

你可以用 trait 以两种方式解决这个问题。一个相当标准的继承方案可能使用以下结构。

```
trait Person { ... }
trait Parent extends Person { ... }
trait Male extends Person { ... }
class Father extends Parent with Male { ... }
```

这里 Parent 和 Male 都是 Person 的子类型，而 Father 同时继承自两者。在这种情况下 Person 必须是一个 trait。这是因为 trait 只能继承自其他 trait，不能继承类。在其下方，Parent 或 Male 中的任何一个都可以是类，但不能同时是类，因为 Father 然后就不能同时继承它们。没有迫切理由将其中一个设为类，选择 trait 提供了统一性。

构造这些类型的另一种方法可以是使用 trait 作为 mix-in 类型。代码可能如下所示。

```
class Person { ... }
trait Parent { ... }
trait Male { ... }
class Father extends Person with Parent with Male { ... }
```

在这个构造中，Parent 和 Male 类型都是不继承自 Person 的 trait。相反，它们与 Person 混合以创建 Father。这种方法可能有点更高级，如果 Parent 和 Male 类型涉及需要它们知道将与 Person 一起使用的代码，你将需要使用 self-types，这在附录 B 中讨论。现在重要的是你要意识到这个选项的存在，这样在我们构建不同的继承层次结构时，你就能理解发生了什么。

### trait or abstract class?

程序员在 Scala 中编写将用于继承的抽象类型时经常遇到的一个标准问题是，在编码抽象类型时选择抽象类还是 trait。经验法则是优先选择 trait，因为它允许多重继承的灵活性。虽然它不能接受参数，但你希望作为参数提供的任何值都可以放入 trait 中并保持未定义，这样最终实现它们的类就必须提供这些值。

## 19.2.7 final

当某物是抽象的时，这基本上意味着它必须在子类中“被重写”。¹ 也有时候有用的是能够说某物不能被重写，或在子类型中被更改。final 关键字可以强制执行这一要求。你可以使用 final 来修改你不希望在子类型中更改的成员数据或方法。它也可以用来修改整个类，当你不希望允许该类有任何子类型时。

你可能会想知道为什么你会想要使某物 final。对这个问题的回答之一是，你希望在当前实现中保留某种行为，而不希望在子类型中被更改。它也可以作为一种方式告诉使用该类的事物，不可能从该类型的对象获得与该特定类型不同的行为。

在类定义不可变类型时，你应该使用 **final** 来保留类型行为的最常见示例。不可变类型的优势，以及它们如何简化代码，在本书中已经相当多地讨论过。没有继承，如果你编写一个类型使其不可变，你就知道该类型的任何对象都可以安全地传递给其他代码，而不用担心它被更改。² 有了继承，除非你使 **class** final，否则这不自动成立。原因在于子类型可以添加可变数据和/或重写方法，使得新实现包含对可变状态的引用。

为了帮助你理解这一点，请考虑以下示例类。

```
class CharInStrComp(str: String) {
    def positionCompare(str2: String, index: Int): Int = {
        if (index >= str.length) {
            if (index >= str2.length) 0 else 1
        } else if (index >= str2.length) -1 else {
            str(index).compareTo(str2(index))
        }
    }
}
```

这个类是不可变的。从技术上讲，它甚至没有可变成员数据。因此，如果你从这个类创建了一个对象，它可以自由传递。有了继承，情况就不同了，可以这样做。

```
class CntCharInStrComp(str: String) extends CharInStrComp(str) {
    var cnt = 0
    override def positionCompare(str2: String, index: Int): Int = {
        cnt += 1
        super.positionCompare(str2, index)
    }
}
```

如果你创建 CntCharInStrComp 的一个实例，它可以在任何想要 CharInStrComp 的地方使用。唯一的问题是，如果这是在依赖对象不可变的代码中完成，该代码现在可能会中断，因为它被传递了一个可变对象。为了防止这种情况发生，原版本应设为 **final**，如下所示。

```
final class CharInStrComp(str: String) {
    def positionCompare(str2: String, index: Int): Int = {
        if (index >= str.length) {
            if (index >= str2.length) 0 else 1
        } else if (index >= str2.length) -1 else {
            str(index).compareTo(str2(index))
        }
    }
}
```

现在任何尝试创建子类型，无论是可变还是不可变，都会产生错误。

**final** 关键字在编程中经常被低估。然而，养成在不应该有子类型或某物不应该被重写时使之 **final** 的习惯是好的。这不仅是一种安全的实践；标记为 **final** 的代码有时也可以被编译为更快的实现。

2. 我们将在第 21 章中看到，这样的对象可以在多个线程间安全使用。

