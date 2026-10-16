

支持这些活动的对象包含一个方法，该方法为展出的每只鸟绘制其鸟的图片。这看起来足够简单。当访客在其飞行笼中选择一只鸟时，系统会将与该鸟关联的对象的引用放置在一个列表中。在展览出口处，系统调用访客列表中每个对象的 draw 方法。过程的复杂性在于动物园只提供部分鸟对象。有些鸟对象是从第三方供应商购买的，有些则由动物园赞助人捐赠。由于鸟对象的来源多样，它们没有共同的基类（除了 Object）并且不实现共同的接口，那么可以保存什么类型的引用？一个明显的解决方案是使每个鸟对象成为基类的子类。基类类型的引用可以存储在列表中，并且可以使用动态绑定来调用 draw 方法。这种方法的缺点是每个鸟类都需要被修改以使新类成为共同基类的子类。最好是新的鸟类可以简单地添加到代码文件中而无需修改。另一种可能的解决方案是使用 instanceof 和类型转换来确定引用的具体类型。这将为系统增加大量代码，增加其复杂性和维护成本。更好的解决方案是使用反射所能实现的动态绑定。

## 12.6.3 Java 中的反射

Java 对反射提供了有限的支持。元数据的核心类在命名空间 java.lang.Class 中定义。15 该类具有令人困惑的名称 Class。Java 运行时系统为程序中的每个对象实例化一个 Class 实例。Class 类提供了一组方法来检查程序对象的类型信息和成员。Class 是所有反射 API 的访问点。

如果程序有一个对象（不是原始类型）的引用，则可以通过调用其 getClass 方法获得该对象的 Class 对象。所有类都从 Object 继承 getClass，所有对象都源自 Object。考虑以下示例：

```
float[] totals = new float[100];
Class fltlist = totals.getClass();
Class stg = "hello".getClass();
```

变量 fltlist 的值将是 totals 数组对象的 Class 对象。stg 的值将是 String 的 Class 对象（因为 "hello" 是 String 的一个实例）。

如果某个类的对象不存在，可以通过在其类名后附加 .class 来通过类名获得其 Class 对象。例如，我们可以有以下内容：

```
Class stg = String.class;
```

```
// A class to define the method that dynamically calls the
// methods of a passed class object
class Reflect {
    public static void callDraw(Object birdObj) {
        Class cls = birdObj.getClass();
        try {
            // Find the draw method of the given class
            Method method = cls.getMethod("draw");
            // Dynamically call the method
            method.invoke(birdObj);
        }
        // In case the given class does not support draw
        catch (NoSuchMethodException e) {
            throw new IllegalArgumentException (
                cls.getName() + "does not support draw");
        }
        // In case the callDraw cannot call draw
        catch (IllegalAccessException e) {
            throw new IllegalArgumentException (
                "Insufficient access permissions to call" +
                "draw in class " + cls.getName());
        }
        // In case draw throws an exception
        catch (InvocationTargetException e) {
            throw new RuntimeException(e);
        }
    }
}
class Bird1 {
    public void draw() {
        System.out.println("This is draw from Bird1");
    }
}
class Bird2 {
    public void draw() {
        System.out.println("This is draw from Bird2");
    }
}
class Bird3 {
    public void draw() {
        System.out.println("This is draw from Bird3");
    }
}
```

该程序的输出如下：

```
This is draw from Bird3
This is draw from Bird1
This is draw from Bird2
```

```
Console.WriteLine("This is draw from Bird1");
}
}
class Bird2 {
    public void draw() {
        Console.WriteLine("This is draw from Bird2");
    }
}
class Bird3 {
    public void draw() {
        Console.WriteLine("This is draw from Bird3");
    }
}
```

我们关于动态方法绑定的简单示例展示了反射的众多用途之一。

除了类的成员和方法之外，以下程序元素在 Java 和 C# 中都可以通过反射访问：类修饰符，例如 public、static 和 final，构造函数，方法参数类型，以及已实现的接口。此外，一个类的继承路径的描述可以被内省。在 C# 中但在 Java 中不能，方法的形参名称可以被发现。

Java 的反射与 C# 的反射之间一个显著的区别是 System.Reflection.Emit 命名空间，它是 .NET 的一部分。该命名空间提供了创建 CIL 代码和容纳该代码的程序集的能力。Java 没有提供此类功能，尽管可以使用其他供应商的工具来实现。

尽管反射为静态类型语言 Java 和 C# 增加了多种功能，但使用反射的用户必须意识到其缺点：

- 使用反射时性能几乎总是会下降。在运行时解析类型、方法和字段并不是非反射代码运行成本的一部分。此外，当类型被动态解析时，代码的一些优化无法完成。
- 反射暴露私有字段和方法，这违反了抽象和信息隐藏的规则，并且可能导致意外的副作用并对可移植性产生不利影响。
- 尽管早期类型检查的优势被广泛接受，但反射所能实现的后期绑定显然否定了该优势。
- 在某些安全管理器下运行代码时，一些反射操作可能无法工作，这也使其不可移植。一种这样的安全环境是运行小程序的环境。在大多数情况下，如果问题可以在不使用反射的情况下解决，就不应使用反射。

反射是大多数动态类型语言不可或缺的一部分。在 LISP 中，反射被常规使用，代码的动态构造和执行并不罕见。在其他解释型语言中，如 JavaScript、Perl 和

Python，符号表在解释期间被保留，提供所有有用的类型信息。

例如在 Python 中，type 方法返回给定值的类型。例如，type([1, 14, 21]) 是 list。isinstance 方法如果其第一个参数具有其第二个参数中命名的类型，则返回布尔值。例如，isinstance(17, int) 返回 True。callable 函数用于确定表达式是否返回函数对象。dir 函数返回其参数对象的属性列表，包括数据和方法。

面向对象编程基于三个基本概念：抽象数据类型、继承和动态绑定。面向对象编程语言通过类、方法、对象和消息传递来支持该范式。

本章中关于面向对象编程语言的讨论围绕七个设计问题展开：对象的排他性、子类和子类型、类型检查和多态性、单继承和多继承、动态绑定、对象的显式或隐式释放，以及嵌套类。

Smalltalk 是一种纯面向对象的语言——一切都是对象，所有计算都是通过消息传递完成的。所有类型检查和消息到方法的绑定都是动态的，所有继承都是单继承。Smalltalk 没有显式的释放操作。

C++ 提供了数据抽象、继承和消息到方法的可选动态绑定，以及 C 的所有传统特性。这意味着它有两个不同的类型系统。C++ 提供多重继承和显式对象释放。它包含对类中实体的一系列访问控制，其中一些阻止子类成为子类型。构造函数和析构函数方法都可以包含在类中；两者通常是隐式调用的。

虽然 Smalltalk 的动态类型绑定比混合语言 C++ 提供了稍多的编程灵活性，但效率远低于后者。

Objective-C 支持过程式和面向对象编程。它比 C++ 更简单，使用也更少。仅支持单继承，尽管它具有类别，允许将额外的 mixin 方法添加到类中。它还具有协议，与 Java 的接口类似。类可以采用任意数量的协议。构造函数可以有任何名称，但必须显式调用。通过预定义类型 id 支持多态。id 类型的变量可以引用任何对象。当通过 id 类型变量引用的对象调用方法时，绑定是动态的。

与 C++ 不同，Java 不是混合语言；它旨在仅支持面向对象编程。Java 既有原始标量类型也有类。所有对象都从堆中分配，并通过引用变量访问。没有显式的对象释放操作——使用垃圾回收。唯一的子程序是方法，并且它们只能通过对象调用。

