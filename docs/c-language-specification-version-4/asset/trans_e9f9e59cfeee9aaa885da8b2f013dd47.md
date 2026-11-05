
在 Button 类的声明之外，Click 成员只能用于 += 和 -= 运算符的左侧，例如

```
b.Click += new EventHandler(...);
```

它会把一个委托追加到 Click 事件的调用列表中；而

```
b.Click -= new EventHandler(...);
```

它会从 Click 事件的调用列表中移除一个委托。

编译字段式事件时，编译器会自动创建用于保存委托的存储，并为该事件创建访问器，以便向委托字段添加或移除事件处理程序。为了保证线程安全，添加或移除操作会在持有锁（§8.12）的情况下执行：对于实例事件，该锁位于包含该事件的对象上；对于静态事件，该锁位于类型对象（§7.6.10.6）上。

因此，如下形式的实例事件声明：

```
class X
{
    public event D Ev;
}
```

可编译为与以下代码等效的形式：

```
class X
{
    private D __Ev; // field to hold the delegate
    public event D Ev {
        add {
            lock(this) { __Ev = __Ev + value; }
        }
        remove {
            lock(this) { __Ev = __Ev - value; }
        }
    }
}
```

在类 X 内部，对 Ev 的引用会被编译为改为引用隐藏字段 __Ev。名称“__Ev”是任意的；该隐藏字段可以具有任何名称，也可以完全没有名称。

类似地，如下形式的静态事件声明：

```
class X
{
    public static event D Ev;
}
```

可编译为与以下代码等效的形式：

```
class X
{
    private static D __Ev; // field to hold the delegate
    public static event D Ev {
        add {
            lock(typeof(X)) { __Ev = __Ev + value; }
        }
        remove {
            lock(typeof(X)) { __Ev = __Ev - value; }
        }
    }
}
```

Control 类为事件实现了一种内部存储机制。AddEventHandler 方法将委托值与键关联起来，GetEventHandler 方法返回当前与某个键关联的委托，RemoveEventHandler 方法移除作为指定事件的事件处理程序的委托。据推测，底层存储机制的设计使得将空委托值与键关联不会产生开销，因此未处理的事件不占用存储空间。

## 10.8.3 静态事件和实例事件

当事件声明包含 static 修饰符时，该事件称为静态事件。当不存在 static 修饰符时，该事件称为实例事件。

静态事件不与特定实例关联，并且在静态事件的访问器中引用 this 会导致编译时错误。

实例事件与类的给定实例关联，并且在该事件的访问器中可以通过 this（§7.6.7）访问该实例。

当在 E.M 形式的成员访问（§7.6.4）中引用事件时，如果 M 是静态事件，则 E 必须表示包含 M 的类型；如果 M 是实例事件，则 E 必须表示包含 M 的类型的实例。

静态成员与实例成员之间的差异将在 §10.3.7 中进一步讨论。

## 10.8.4 虚拟、密封、重写和抽象访问器

虚拟事件声明指定该事件的访问器是虚拟的。virtual 修饰符同时适用于事件的两个访问器。

抽象事件声明指定该事件的访问器是虚拟的，但不提供访问器的实际实现。相反，非抽象派生类必须通过重写该事件来为访问器提供自己的实现。由于抽象事件声明不提供实际实现，因此它不能提供用大括号分隔的事件访问器声明。

同时包含 abstract 和 override 修饰符的事件声明指定该事件是抽象的，并且重写一个基事件。此类事件的访问器也是抽象的。

抽象事件声明只允许在抽象类（§10.1.1.1）中。

通过包含指定 override 修饰符的事件声明，可以在派生类中重写继承的虚拟事件的访问器。这称为重写事件声明。重写事件声明不会声明新事件。相反，它只是特化现有虚拟事件的访问器实现。

重写事件声明必须指定与被重写事件完全相同的可访问性修饰符、类型和名称。

重写事件声明可以包含 sealed 修饰符。使用此修饰符可阻止派生类进一步重写该事件。密封事件的访问器也是密封的。

重写事件声明包含 new 修饰符会导致编译时错误。

除声明和调用语法不同外，虚拟、密封、重写和抽象访问器的行为与虚拟、密封、重写和抽象方法完全相同。具体而言，§10.6.3、§10.6.4、§10.6.5 和 §10.6.6 中描述的规则适用，就如同访问器是相应形式的方法一样。每个访问器对应于一个方法，该方法具有一个事件类型的值参数、void 返回类型，以及与包含该事件的事件相同的修饰符。

## 10.9 索引器

索引器是一种成员，它使对象能够像数组一样被索引。索引器使用 indexer-declarations 声明：

## C# 语言规范

```
indexer-declaration:
    attributes_opt indexer-modifiers_opt indexer-declarator { accessor-declarations }
indexer-modifiers:
    indexer-modifier
    indexer-modifiers indexer-modifier
indexer-modifier:
    new
    public
    protected
    internal
    private
    virtual
    sealed
    override
    abstract
    extern
indexer-declarator:
    type this [ formal-parameter-list ]
    type interface-type . this [ formal-parameter-list ]
```

indexer-declaration 可以包含一组特性（§17）以及四个访问修饰符（§10.3.5）、new（§10.3.4）、virtual（§10.6.3）、override（§10.6.4）、sealed（§10.6.5）、abstract（§10.6.6）和 extern（§10.6.7）修饰符的有效组合。

在修饰符的有效组合方面，索引器声明遵循与方法声明（§10.6）相同的规则，唯一的例外是索引器声明中不允许使用 static 修饰符。

virtual、override 和 abstract 修饰符互斥，只有一种情况例外。abstract 和 override 修饰符可以一起使用，以便抽象索引器可以重写虚拟索引器。

索引器声明的类型指定该声明所引入索引器的元素类型。除非该索引器是显式接口成员实现，否则该类型后跟关键字 this。对于显式接口成员实现，该类型后跟 interface-type、一个“.”以及关键字 this。与其他成员不同，索引器没有用户定义的名称。

formal-parameter-list 指定索引器的参数。索引器的形参列表对应于方法的形参列表（§10.6.1），不同之处在于必须至少指定一个参数，并且不允许使用 ref 和 out 参数修饰符。

索引器的类型以及 formal-parameter-list 中引用的每个类型，其可访问性必须至少与索引器本身相同（§3.5.4）。

accessor-declarations（§10.7.2）必须括在“{”和“}”标记中，它们声明索引器的访问器。访问器指定与读取和写入索引器元素相关联的可执行语句。

尽管访问索引器元素的语法与访问数组元素的语法相同，但索引器元素不会被归类为变量。因此，不能将索引器元素作为 ref 或 out 参数传递。

索引器和属性在概念上非常相似，但有以下不同之处：

- 属性由其名称标识，而索引器由其签名标识。
- 属性通过 *简单名称*（§7.6.2）或 *成员访问*（§7.6.4）访问，而索引器元素通过 *元素访问*（§7.6.2）访问。
- 属性可以是 `static` 成员，而索引器始终是实例成员。
- 属性的 `get` 访问器对应于没有参数的方法，而索引器的 `get` 访问器对应于与索引器具有相同形参列表的方法。
- 属性的 `set` 访问器对应于一个具有名为 `value` 的单个参数的方法，而索引器的 `set` 访问器对应于一个具有与索引器相同形参列表并额外具有名为 `value` 的参数的方法。
- 如果索引器访问器声明了与索引器参数同名的局部变量，则会导致编译时错误。
- 在重写属性声明中，继承的属性使用语法 `base.P` 访问，其中 P 是属性名。在重写索引器声明中，继承的索引器使用语法 `base[E]` 访问，其中 E 是逗号分隔的表达式列表。

除这些差异外，§10.7.2 和 §10.7.3 中定义的所有规则同样适用于索引器访问器和属性访问器。

当索引器声明包含 extern 修饰符时，该索引器称为外部索引器。由于外部索引器声明不提供实际实现，因此其每个访问器声明都由一个分号组成。

下面的示例声明了一个 BitArray 类，该类实现了一个索引器，用于访问位数组中的各个位。

```csharp
using System;
class BitArray
{
    int[] bits;
    int length;
    public BitArray(int length) {
        if (length < 0) throw new ArgumentException();
        bits = new int[((length - 1) >> 5) + 1];
        this.length = length;
    }

    public int Length {
        get { return length; }
    }
}
```

