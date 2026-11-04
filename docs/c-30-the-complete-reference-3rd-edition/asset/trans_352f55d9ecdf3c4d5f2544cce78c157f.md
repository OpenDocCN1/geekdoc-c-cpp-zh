
注意，处理程序是使用 += 运算符添加的。事件只支持 += 和 -=。在这个例子中，Handler() 是一个静态方法，但事件处理程序也可以是实例方法。最后，事件的触发方式如下所示：

```
// Fire the event.
evt.OnSomeEvent();
```

调用 OnSomeEvent() 会导致所有已注册的事件处理程序被调用。在这个例子中，只有一个已注册的处理程序，但也可以有更多，正如下一节所解释的那样。

## 多播事件示例

与委托一样，事件也可以是多播的。这使多个对象能够响应一个事件通知。下面是一个事件多播示例：

```
// An event multicast demonstration.
using System;

// Declare a delegate type for an event.
delegate void MyEventHandler();

// Declare a class that contains an event.
class MyEvent {
public event MyEventHandler SomeEvent;

// This is called to fire the event.
public void OnSomeEvent() {
if(SomeEvent != null)
SomeEvent();
}
}

class X {
public void Xhandler() {
Console.WriteLine("Event received by X object");
}
}

class Y {
public void Yhandler() {
Console.WriteLine("Event received by Y object");
}
}

class EventDemo2 {
static void Handler() {
Console.WriteLine("Event received by EventDemo");
}
}

static void Main() {
MyEvent evt = new MyEvent();
X xOb = new X();
Y yOb = new Y();
```

```
// Add handlers to the event list.
evt.SomeEvent += Handler;
evt.SomeEvent += xOb.Xhandler;
evt.SomeEvent += yOb.Yhandler;

// Fire the event.
evt.OnSomeEvent();
Console.WriteLine();

// Remove a handler.
evt.SomeEvent -= xOb.Xhandler;
evt.OnSomeEvent();
}
```

该程序的输出如下所示：

```
Event received by EventDemo
Event received by X object
Event received by Y object

Event received by EventDemo
Event received by Y object
```

这个示例创建了两个额外的类，分别称为 X 和 Y，它们也定义了与 MyEventHandler 兼容的事件处理程序。因此，这些处理程序也可以成为事件链的一部分。注意，X 和 Y 中的处理程序不是静态的。这意味着必须创建每个类的对象，并且必须将与每个实例关联的处理程序添加到事件链中。实例处理程序与静态处理程序之间的差异将在下一节中探讨。

## 实例方法与静态方法作为事件处理程序

尽管实例方法和静态方法都可以用作事件处理程序，但它们在一个重要方面确实有所不同。当静态方法用作处理程序时，事件通知适用于类。当实例方法用作事件处理程序时，事件会发送到特定的对象实例。因此，类中每个希望接收事件通知的对象都必须单独注册。在实践中，大多数事件处理程序都是实例方法，但当然，这取决于具体的应用。让我们看一个各自的示例。

下面的程序创建了一个名为 X 的类，该类定义了一个实例方法作为事件处理程序。这意味着每个 X 对象都必须单独注册才能接收事件。为了演示这一点，该程序将事件多播到三个 X 类型的对象。

```
/* Individual objects receive notifications when instance event handlers are used. */

using System;

// Declare a delegate type for an event.
delegate void MyEventHandler();

// Declare a class that contains an event.
class MyEvent {
```

```
public event MyEventHandler SomeEvent;

// This is called to fire the event.
public void OnSomeEvent() {
    if(SomeEvent != null)
        SomeEvent();
}

class X {
    int id;
    public X(int x) { id = x; }
    // This is an instance method that will be used as an event handler.
    public void XHandler() {
        Console.WriteLine("Event received by object " + id);
    }
}

class EventDemo3 {
    static void Main() {
        MyEvent evt = new MyEvent();
        X o1 = new X(1);
        X o2 = new X(2);
        X o3 = new X(3);
        evt.SomeEvent += o1.XHandler;
        evt.SomeEvent += o2.XHandler;
        evt.SomeEvent += o3.XHandler;
        // Fire the event.
        evt.OnSomeEvent();
    }
}
```

该程序的输出如下所示：

```
Event received by object 1
Event received by object 2
Event received by object 3
```

如输出所示，每个对象分别注册自己对一个事件的兴趣，并且每个对象都收到单独的通知。

或者，当静态方法用作事件处理程序时，事件的处理独立于任何对象，如下面的程序所示：

```
/* A class receives the notification when a static method is used as an event handler. */

using System;

// Declare a delegate type for an event.
```

```
delegate void MyEventHandler();

// Declare a class that contains an event.
class MyEvent {
    public event MyEventHandler SomeEvent;

    // This is called to fire the event.
    public void OnSomeEvent() {
        if(SomeEvent != null)
            SomeEvent();
    }
}

class X {

    /* This is a static method that will be used as
       an event handler. */
    public static void Xhandler() {
        Console.WriteLine("Event received by class.");
    }
}

class EventDemo4 {
    static void Main() {
        MyEvent evt = new MyEvent();

        evt.SomeEvent += X.Xhandler;

        // Fire the event.
        evt.OnSomeEvent();
    }
}
```

该程序的输出如下所示：

```
Event received by class.
```

在该程序中，注意从未创建 X 类型的对象。然而，由于 Xhandler() 是 X 的静态方法，因此它可以附加到 SomeEvent，并在调用 OnSomeEvent() 时执行。

## 使用事件访问器

前面示例中使用的事件形式创建的事件会自动管理事件处理程序调用列表，包括在列表中添加和移除事件处理程序。因此，你不需要自己实现任何列表管理功能。由于它们为你管理细节，这些类型的事件是迄今为止最常用的。然而，你也可以自己提供事件处理程序列表操作，也许是为了实现某种专用的事件存储机制。

要控制事件处理程序列表，你将使用 event 语句的扩展形式，它允许使用事件访问器。这些访问器让你控制事件处理程序列表的实现方式。这种形式如下所示：

```
event event-delegate event-name {
    add {
        // code to add an event to the chain
    }

    remove {
        // code to remove an event from the chain
    }
}
```

这种形式包括两个事件访问器 add 和 remove。当通过使用 += 将事件处理程序添加到事件链时，会调用 add 访问器。当通过使用 -= 从链中移除事件处理程序时，会调用 remove 访问器。

当调用 add 或 remove 时，它接收要添加或移除的处理程序作为参数。与其他类型的访问器一样，此参数称为 value。通过实现 add 和 remove，你可以定义自定义的事件处理程序存储方案。例如，你可以使用数组、栈或队列来存储处理程序。

下面是一个使用 event 的访问器形式的示例。它使用一个数组来保存事件处理程序。由于该数组只有三个元素长，因此任何时候链中只能保存三个事件处理程序。

```
// Create a custom means of managing the event invocation list.
using System;

// Declare a delegate type for an event.
delegate void MyEventHandler();

// Declare a class that holds up to 3 events.
class MyEvent {
    MyEventHandler[] evt = new MyEventHandler[3];

    public event MyEventHandler SomeEvent {
        // Add an event to the list.
        add {
            int i;

            for(i=0; i < 3; i++)
                if(evt[i] == null) {
                    evt[i] = value;
                    break;
                }
            if (i == 3) Console.WriteLine("Event list full.");
        }

        // Remove an event from the list.
        remove {
            int i;

            for(i=0; i < 3; i++)
                if(evt[i] == value) {

