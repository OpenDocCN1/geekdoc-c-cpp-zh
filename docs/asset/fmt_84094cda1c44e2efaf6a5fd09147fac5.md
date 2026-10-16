
`C#` 中的一个概念就是委托，我第一个承认这可能不太容易理解——但这毕竟也是它被放在高级部分的原因。用我能想到的最基本的话来说，`C#` 委托就是说它有一些必须完成的工作，并且它想把这项工作甩给能够完成它的某人或某物。委托会指明它们要移交什么信息，也就是需要完成的工作，以及它们想要得到什么回报。

它们通过声明以下内容来做到这一点：如果一个方法想要接手这项工作，它必须具有特定的参数，并且必须返回特定的类型。然而，与接口不同，方法名是什么并不重要；我们不关心这个，只关心参数和返回类型。

## 声明委托

现在你知道了委托是什么以及它做什么。是时候看看如何创建一个委托了，这将帮助你更好地理解它们。

我们要创建的委托将表示一个方法（任何方法），该方法可以在某种数学运算中使用两个数字。我们要说的是：我们有一些数字，我们需要某个人，任何人，不管是谁，用这些数字做一些数学运算，然后把结果还给我们。

很可能存在一个方法，可以将数字相加并返回结果，或者将它们相乘。也许有一个方法，接收这些数字，将它们平方，相加，然后返回平方根。等等，这不是勾股定理吗？我想说的是，我们想要的只是任何能对我们的数字做点什么并得到结果的方法。

我们知道我们想要什么，所以让我们来实现它。

我们在命名空间中创建委托，就像创建结构体、类和接口一样。和那些一样，你应该养成将每个委托放在单独文件中的习惯——为了便于阅读和维护，让它们彼此分开。

所以，创建一个新的 `.cs` 文件，并把它命名为你的委托的名字。我把它命名为 `MathDelegate.cs`，但你可以随意命名。现在添加下面的代码来创建你的委托：

```
public delegate float MathDelegate(float a, float b);
```

你的 `MathDelegate.cs` 文件（或你命名的任何名字）应该看起来像这样：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Delegates
{
    public delegate float MathDelegate(float a, float b);
}
```

我们现在有了 `delegate` 关键字，它表示我们在寻找一个方法，任何能够接受一对浮点数并返回一个浮点数的方法。

## 使用委托

要使用委托，我们需要一些能够匹配委托要求的方法。我们需要的是能够将浮点数作为参数（在我们的例子中是两个浮点数）并返回一个浮点数作为结果的方法。回到你的 `Program` 类中 `Main` 方法所在的位置，创建以下方法——这三个方法都将匹配我们的委托要求：

```
public static float Add(float a, float b)
{
    return a + b;
}

public static float Subtract(float a, float b)
{
    return a - b;
}

public static float Power(float baseNumber, float exponent)
{
    return (float)Math.Pow(baseNumber, exponent);
}
```

这三个方法都接受一对浮点数作为参数，并且都返回一个浮点数，但每个方法以不同的方式处理这些数字。

在更具体的情况下，你很可能在考虑为这些方法创建委托之前很久就已经定义了它们，但在我们的例子中，我们还没有走到那一步。

使用委托很像使用对象。在你的 `Main` 方法中，你可以添加一些代码，通过委托来使用这些方法中的任何一个。你不必把它放在 `Main` 方法中；你可以把它放在任何你想要的地方。为了本教程的目的，将以下内容添加到你的 `Main` 方法中：

```
MathDelegate mathOperation = Add;

float a = 5;
float b = 7;

float result = mathOperation(a, b);
```

我们在这里所做的是创建了一个类型为 `MathDelegate` 的“变量”，然后像对待任何普通变量一样给它命名。我们给它赋了一个值，这个值是我们某个方法的名称，该方法满足委托的需求——两个浮点参数和浮点返回类型。

在接下来的几行中，我们设置了 `a` 和 `b`，到现在为止，这些对你来说应该都很有意义了——我们所做的只是一些标准的设置。

在最后一行，我们使用了委托，这看起来很像方法调用。在很多方面，它确实就是；我们只是通过委托来调用。

因为我们将 `mathOperation` 赋值给了 `Add` 方法，所以 `Add` 方法将被调用，结果将是 12。

我们不必立即创建委托并给它赋值。我们可以通过一些逻辑来决定在所有可能性中我们想使用哪一个：

```
bool subtractionIsWayBetterThanAddition = true;

MathDelegate mathOperation;

if (subtractionIsWayBetterThanAddition)
{
    mathOperation = Subtract;
}
else
{
    mathOperation = Add;
}

float a = 5;
float b = 7;

float result = mathOperation(a, b);
```

根据布尔变量 `subtractionIsWayBetterThanAddition` 的状态，我们最终可能会调用我们的 `Subtract` 方法。

## 方法作为一等公民

你可能已经意识到，使用委托非常像使用变量或对象，这是有意为之的。

委托允许你像使用变量一样赋值一个方法；它允许你将一个方法作为参数传递给另一个方法，也允许你从另一个方法返回一个方法。

在计算机编程中，这有一个名字。委托将使方法成为“一等公民”，就像具有值类型的变量——`int`、`float`、`byte` 等——以及结构体和对象一样。

这是一种非常强大的能力，但前提是你确切地知道如何使用它。稍后，在本指南的下一部分中，我们将讨论事件，这些事件也非常有用，特别是对于那些想要参与 GUI 编程并创建比控制台好得多的界面的人来说。

除此之外，委托本身也非常强大，这使得它们值得了解。

## 一个更好的例子

为了彻底向你展示委托的力量和实用性，我将向你展示一个更复杂的例子；这个例子非常强大，而且很可能会让你感到困惑。

但是，我要告诉你的是：如果你到目前为止一直跟得上我，并且对到目前为止的一切都有基本的理解，如果你觉得自己真的准备好继续前进并研究事件，那么理解这部分其实并不是那么关键。如果你愿意，你现在就可以继续学习事件，但我建议你完成这一节，哪怕只是为了完善你的知识。

让我们先看看这个例子到底要实现什么。假设你有一个对象，任何对象，它是什么并不重要，你正在使用这个对象。你还有一个 `List`，其中装满你正在处理的其他对象。你还有很多操作，希望在各个不同的时间对列表中的每一项执行。

为简单起见，我们要使用的对象定义如下：

```
public class MagicNumber
{
    public int Number { get; set; }
    public bool IsMagic { get; set; }
}
```

这是一个非常简单的类，但我尽量保持它尽可能简单。

我们还有一些方法会处理 `MagicNumber`，比如这些：

```
public void Increment(MagicNumber magicNumber)
{
    magicNumber.Number++;
}

public void Decrement(MagicNumber magicNumber)
{
    magicNumber.Number--;
}

public void Magicify(MagicNumber magicNumber)
{
    magicNumber.IsMagic = true;
}

public void DeMagicify(MagicNumber magicNumber)
{
    magicNumber.IsMagic = false;
}
```

我仍然努力保持简单！

这些方法中的任何一个都可以用 `MagicNumber` 做很多不同的事情。

但是，所有这些方法都会接收 `MagicNumber` 作为输入，但都不会返回任何内容，这正是委托非常有用的地方。

我们的委托可以这样创建：

```
public delegate void MagicNumberModifier(MagicNumber magicNumber);
```

记住；在主程序中的某个地方，有一种容器会保存我们所有的 `MagicNumber` 对象。它可以是任何容器，但我们暂时使用 `List`。

```
List<MagicNumber> magicNumbers = new List<MagicNumber>();

magicNumbers.Add(new MagicNumber() { Number = 4, IsMagic = true });
magicNumbers.Add(new MagicNumber() { Number = 6, IsMagic = false });
magicNumbers.Add(new MagicNumber() { Number = 9, IsMagic = true });
magicNumbers.Add(new MagicNumber() { Number = 13, IsMagic = false });
magicNumbers.Add(new MagicNumber() { Number = 20, IsMagic = true });
```

我们可以这样做：

```
public static void ApplyModifierToAll(MagicNumberModifier modifier, List<MagicNumber> magicNumbers)
{
    foreach(MagicNumber number in magicNumbers)
    {
        modifier(number);
    }
}
```

然后，在 `Main` 方法中（或任何你想要的位置），这样：

```
public static void Main(string[] args)
{
    List<MagicNumber> magicNumbers = new List<MagicNumber>();

    magicNumbers.Add(new MagicNumber() { Number = 4, IsMagic = true });
    magicNumbers.Add(new MagicNumber() { Number = 6, IsMagic = false });
    magicNumbers.Add(new MagicNumber() { Number = 9, IsMagic = true });
    magicNumbers.Add(new MagicNumber() { Number = 13, IsMagic = false });
    magicNumbers.Add(new MagicNumber() { Number = 20, IsMagic = true });

    ApplyModifierToAll(Increment, magicNumbers);
    ApplyModifierToAll(Magicify, magicNumbers);
}
```

这是一个被称为访问者设计模式的绝佳示例。你现在可能还不知道这些是什么，但简而言之，设计模式是为相似问题设计的通用解决方案。这些并非所有程序员都会使用，但使用访问者模式，你可以在不担心它们所包含的结构的情况下，对一种对象类型执行各种操作。

## Quick Primer

- Real-world delegates are people or things that do something for people or things.

- `C#` delegates provide a way for methods to be passed like variables or objects giving you the ability to delegate methods as you go, as and when needed.

- The `delegate` keyword is needed to create them, i.e., `public delegate float MathDelegate(float a, float b);`. We could now use this to track methods that have the `float` return type and the same `float`, `float` list of parameters.

- Once created, delegates can be used in a similar way to a variable, i.e. `MathDelegate mathOperation = Add; float a = 5; float b = 7; float result = mathOperation(a, b);`. Of course, the implication here is that you have an `Add` method that already returns a `float` and takes a pair of `float`s as its parameters, thus matching what the delegate requires.

## What's Next?

Delegates are more than a little confusing but, like everything, you don’t need to have a thorough understanding of them, to begin with. At the end of the day, understanding the basics is enough to get you started and practice will improve your ability and understanding.

In order to move on to the next section, you must have that basic understanding. If you haven't, go back over this section until you feel ready to take on the next topic – events. These rely on delegates very heavily so make sure you know enough.

## Events

Events are one of the coolest features in `C#` because when a specific event occurs, they let classes notify others. This is one of the most common things in applications that are GUI based; you might have things like forms, checkboxes, and buttons. All of these can indicate that something has happened – a button was pressed, a form was completed, a box was checked, and so on – notifying other classes of what has happened so they can handle things as they need to.

Delegates are a key part of the events features – if you still don’t understand delegates, go back over the previous section because you need, at the very least, a basic understanding of them. Delegates are what we will use to receive the event notifications.

## Defining an Event

The first thing we need to do is create our event. We’ll assume that we have a class representing one point that is in two dimensions; thus it will have both an X and a Y coordinate or value. The class would look like this:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Events
{
    public class Point
    {
        private double x;
        private double y;
```
