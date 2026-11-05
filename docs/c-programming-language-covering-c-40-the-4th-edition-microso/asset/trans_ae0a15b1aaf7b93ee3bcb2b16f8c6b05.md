
Click 在 Button 类中用作一个字段。如示例所示，该字段可以被检查、修改，并在委托调用表达式中使用。Button 类中的 OnClick 方法“引发” Click 事件。引发事件的概念与调用事件所表示的委托完全等价——因此没有用于引发事件的特殊语言构造。请注意，委托调用之前会进行检查以确保委托不为空。

在 Button 类的声明之外，Click 成员只能在 += 和 -= 运算符的左侧使用，如

```
    b.Click += new EventHandler(...);
```

它将委托附加到 Click 事件的调用列表中，并且

```
    b.Click -= new EventHandler(...);
```

它将委托从 Click 事件的调用列表中移除。

编译类字段的事件时，编译器会自动创建存储以保存委托，并为事件创建访问器以向委托字段添加或移除事件处理程序。添加和移除操作是线程安全的，并且可以在持有包含对象的锁（§8.12）——对于实例事件，或类型对象（§7.6.10.6）——对于静态事件的情况下执行（但不是必须的）。

因此，形式为

```
    class X
    {
        public event D Ev;
    }
```

的实例事件声明

将被编译为等效于

```
    class X
    {
        private D __Ev;  // Field to hold the delegate
        public event D Ev {
            add {
                /* Add the delegate in a thread-safe way */
            }
            remove {
                /* Remove the delegate in a thread-safe way */
            }
        }
    }
```

在类 X 内部，对 Ev 在 += 和 -= 运算符左侧的引用会导致 add 和 remove 访问器被调用。Ev 的所有其他引用都被编译为引用隐藏字段 __Ev。名称 "__Ev" 是任意的；隐藏字段可以有任何名称或根本没有名称。

## 10.8.2 事件访问器

事件声明通常省略事件访问器声明，如上面的 Button 示例所示。省略这样做的一种情况涉及每个事件一个字段的存储成本不可接受的情况。在这种情况下，类可以包含事件访问器声明并使用私有机制来存储事件处理程序列表。

事件的事件访问器声明指定与添加和移除事件处理程序相关联的可执行语句。

访问器声明由一个 add 访问器声明和一个 remove 访问器声明组成。每个访问器声明由标记 add 或 remove 后跟一个块组成。与 add 访问器声明关联的块指定在添加事件处理程序时要执行的语句，而与 remove 访问器声明关联的块指定在移除事件处理程序时要执行的语句。

每个 add 访问器声明和 remove 访问器声明对应于一个具有事件类型单个 value 参数和 void 返回类型的方法。事件访问器的隐式参数名为 value。当事件在事件赋值中使用时，会使用适当的事件访问器。具体来说，如果赋值运算符是 +=，则使用 add 访问器；如果赋值运算符是 -=，则使用 remove 访问器。在任何情况下，赋值运算符的右操作数都用作事件访问器的参数。add 访问器声明或 remove 访问器声明的块必须符合 §10.6.10 中描述的 void 方法规则。特别是，此类块中的 return 语句不允许指定表达式。

由于事件访问器隐式具有名为 value 的参数，因此在事件访问器中声明的局部变量或常量具有该名称是编译时错误。

在示例

```
class Control : Component
{
    // Unique keys for events
    static readonly object mouseDownEventKey = new object();
    static readonly object mouseUpEventKey = new object();

    // Return event handler associated with key
    protected Delegate GetEventHandler(object key) {...}

    // Add event handler associated with key
    protected void AddEventHandler(object key, Delegate handler) {...}

    // Remove event handler associated with key
    protected void RemoveEventHandler(object key, Delegate handler) {...}
    // MouseDown event
    public event MouseEventHandler MouseDown {
      add { AddEventHandler(mouseDownEventKey, value); }
      remove { RemoveEventHandler(mouseDownEventKey, value); }
    }
    // MouseUp event
    public event MouseEventHandler MouseUp {
      add { AddEventHandler(mouseUpEventKey, value); }
      remove { RemoveEventHandler(mouseUpEventKey, value); }
    }
    // Invoke the MouseUp event
    protected void OnMouseUp(MouseEventArgs args) {
      MouseEventHandler handler;
      handler = (MouseEventHandler)GetEventHandler(mouseUpEventKey);
      if (handler != null)
        handler(this, args);
    }
}
```

中，Control 类实现了事件的内部存储机制。AddEventHandler 方法将委托值与键关联，GetEventHandler 方法返回当前与键关联的委托，而 RemoveEventHandler 方法将委托作为指定事件的事件处理程序移除。推测底层存储机制设计为将 null 委托值与键关联没有成本，因此未处理的事件不消耗存储。

## 10.8.3 静态事件和实例事件

当事件声明包含 static 修饰符时，该事件称为静态事件。当没有 static 修饰符时，该事件称为实例事件。

静态事件与特定实例无关，在静态事件的访问器中引用 this 是编译时错误。

实例事件与类的给定实例关联，并且该实例可以在该事件的访问器中作为 this (§7.6.7) 访问。

当事件在形式为 E.M 的成员访问（§7.6.4）中被引用时，如果 M 是静态事件，则 E 必须表示包含 M 的类型；如果 M 是实例事件，则 E 必须表示包含 M 的类型的实例。

静态成员和实例成员之间的差异在 §10.3.7 中进一步讨论。

## 10.8.4 虚拟、密封、重写和抽象访问器

虚拟事件声明指定该事件的访问器是虚拟的。virtual 修饰符适用于事件的两个访问器。

抽象事件声明指定事件的访问器是虚拟的，但不提供访问器的实际实现。相反，非抽象派生类必须通过重写事件为访问器提供自己的实现。由于抽象事件声明不提供实际实现，因此它不能提供用大括号分隔的事件访问器声明。

包含 abstract 和 override 修饰符的事件声明指定该事件是抽象的并且重写了基事件。此类事件的访问器也是抽象的。

抽象事件声明仅允许在抽象类中（§10.1.1.1）。

继承的虚拟事件的访问器可以通过包含指定 override 修饰符的事件声明在派生类中被重写。这称为重写事件声明。重写事件声明不会声明新事件。相反，它只是专门化现有虚拟事件的访问器的实现。

重写事件声明必须指定与被重写事件完全相同的可访问性修饰符、类型和名称。

重写事件声明可以包含 sealed 修饰符。使用此修饰符可防止派生类进一步重写该事件。密封事件的访问器也是密封的。

重写事件声明包含 new 修饰符是编译时错误。

除了声明和调用语法上的差异外，virtual、sealed、override 和 abstract 访问器与 virtual、sealed、override 和 abstract 方法完全相同。具体来说，§10.6.3、§10.6.4、§10.6.5 和 §10.6.6 中描述的规则就好像访问器是相应形式的方法一样适用。每个访问器对应于一个具有事件类型单个 value 参数、void 返回类型以及与包含事件相同的修饰符的方法。

## 10.9 索引器

索引器是使对象能够像数组一样被索引的成员。索引器使用索引器声明进行声明：
