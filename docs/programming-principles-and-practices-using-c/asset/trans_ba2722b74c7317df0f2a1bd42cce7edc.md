

- 该技术处理各种类型的交互（不仅仅限于我们的小按钮操作）。
- 一个窗口可以有多个按钮；一个程序可以有多个窗口。

然而，一旦我们理解了 `next()` 是如何被调用的，我们基本上就理解了如何处理具有 GUI 界面的程序中的每个操作。

## 16.3.2 等待循环

因此，在这个——我们最简单的——情况下，每当按钮被“按下”时，我们希望通过 `Simple_window` 的 `next()` 完成什么？基本上，我们希望有一个操作，使程序的执行在某一点停止，从而让我们有机会查看到目前为止完成的工作。并且，我们希望 `next()` 在该等待之后重新启动我们的程序：

```cpp
// create some objects and/or manipulate some objects, display them in a window
win.wait_for_button();    // next() causes the program to proceed from here
// create some objects and/or manipulate some objects
```

实际上，这很容易做到。让我们首先定义 `wait_for_button()`：

```cpp
void Simple_window::wait_for_button()
    // modified event loop:
    // handle all events (as per default), quit when button_pushed becomes true
    // this allows graphics without control inversion
{
    while (!button_pushed) Fl::wait();
    button_pushed = false;
    Fl::redraw();
}
```

就像大多数 GUI 系统一样，FLTK 提供了一个函数，用于暂停程序直到某事发生。FLTK 版本称为 `wait()`。实际上，`wait()` 处理了很多事情，因为我们的程序会在任何影响它的事件发生时被唤醒。例如，在 Microsoft Windows 下运行时，当窗口被移动或在被其他窗口遮挡后变得可见时，重绘其窗口是程序的责任。处理窗口大小的调整也是 `Window` 的职责。`Fl::wait()` 以默认方式处理所有这些任务。每次 `wait()` 处理完某事，它都会返回，给我们的代码一个机会去做某事。

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_591_0.png)

因此，当有人点击我们的“Next”按钮时，**wait()** 调用 **cb_next()** 并返回（回到我们的“等待循环”）。为了在 **wait_for_button()** 中继续，**next()** 只需要将布尔变量 **button_pushed** 设置为 **true**。这很简单：

```cpp
void Simple_window::next()
{
    button_pushed = true;
}
```

当然，我们还需要在某个地方定义 **button_pushed**：

```cpp
bool button_pushed;    // initialized to false in the constructor
```

等待之后，**wait_for_button()** 需要重置 **button_pushed** 并对窗口进行 **redraw()**，以确保我们在屏幕上可以看到所做的任何更改。这就是它所做的。

## 16.3.3 将 lambda 表达式用作回调

因此，对于 **Widget** 上的每个操作，我们必须定义两个函数：一个用于从系统的回调概念进行映射，另一个用于执行我们期望的操作。考虑：

```cpp
struct Simple_window : Graph_lib::Window {
    Simple_window(Point xy, int w, int h, const string& title);
    void wait_for_button();    // simple event loop
    private:
    Button next_button;        // the “Next” button
    bool button_pushed;        // implementation detail
    static void cb_next(Address, Address);    // callback for next_button
    void next();              // action to be done when next_button is pressed
};
```

通过使用 lambda 表达式（§ 15.3.3），我们可以消除显式声明映射函数 **cb_next()** 的需要。相反，我们在 **Simple_window** 的构造函数中定义映射：

```cpp
Simple_window::Simple_window(Point xy, int w, int h, const string& title)
:Window(xy,w,h,title),
next_button(Point{x_max()-70,0}, 70, 20, "Next",
[](Address, Address pw) {
    reference_to<Simple_window>(pw).next();
}
),
button_pushed(false)
{
    attach(next_button);
}
```

## 16.4 按钮和其他组件

我们这样定义 **Button**：

```cpp
struct Button : Widget {
    Button(Point xy, int w, int h, const string& label, Callback cb);
    void attach(Window&);
};
```

因此，**Button** 是一个具有位置 (**xy**)、大小 (**w,h**)、文本标签 (**label**) 和回调 (**cb**) 的 **Widget**。基本上，任何出现在屏幕上并附带操作（例如回调）的东西都是 **Widget**。

### 16.4.1 组件

是的，*widget*（组件）确实是一个技术术语。一个更具描述性但不够生动的组件名称是 *control*（控件）。我们使用组件来定义通过 GUI（图形用户界面）与程序交互的形式。我们的 **Widget** 接口类看起来像这样：

```cpp
class Widget {
    // Widget is a handle to an FL_widget — it is "not" an FL_widget
    // we try to keep our interface classes at arm's length from FLTK
    public:
    Widget(Point xy, int w, int h, const string& s, Callback cb);
    virtual void move(int dx, int dy);
    virtual void hide();
    virtual void show();
    virtual void attach(Window&) = 0;
    Point loc;
    int width;
    int height;
    string label;
    Callback do_it;
    protected:
    Window* own; // every Widget belongs to a Window
    Fl_Widget* pw; // connection to the FLTK Widget
};
```

**Widget** 有两个有趣的函数，我们可以将其用于 **Button**（也可以用于任何其他从 **Widget** 派生的类，例如 **Menu**；参见 § 16.7）：

- **hide()** 使 **Widget** 不可见。
- **show()** 使 **Widget** 再次可见。

**Widget** 开始时是可见的。

就像 **Shape** 一样，我们可以移动（**move()**）窗口中的 **Widget**，并且在使用之前必须将其 **attach()** 到 **Window**。注意，我们将 **attach()** 声明为纯虚函数（§ 14.3.5）；从 **Widget** 派生的每个类都必须定义其附着到 **Window** 的含义。实际上，系统级组件是在 **attach()** 中创建的。**attach()** 函数是从 **Window** 调用的，作为其自身 **attach()** 实现的一部分。基本上，将窗口和组件连接起来是一种精致的小舞蹈，各方都必须完成自己的一部分。结果是，窗口知道它的组件，每个组件都知道它的窗口：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_594_0.png)

注意，**Window** 不知道它处理的是哪种 **Widget**。如 § 14.4 所述，我们使用基本的面向对象编程来确保 **Window** 可以处理任何类型的 **Widget**。同样，**Widget** 也不知道它处理的是哪种 **Window**。

我们稍显随意，保留了可访问的数据成员。**own** 和 **pw** 成员严格用于派生类的实现，因此我们将它们声明为 **protected**（受保护）。

**Widget** 以及我们在此使用的组件（**Button**、**Menu** 等）的定义位于 **GUI.h** 中。

### 16.4.2 按钮

**Button** 是我们处理的最简单的 **Widget**。它所做的只是在点击时调用回调：

```cpp
class Button : public Widget {
    public:
    Button(Point xy, int ww, int hh, const string& s, Callback cb)
        :Widget{xy,ww,hh,s,cb} {}

    void attach(Window& win);
};
```

就是这样。**attach()** 函数包含所有（相对）杂乱的 FLTK 代码。我们将解释推迟到附录 E（不要在阅读第 17 章和第 18 章之前阅读）。目前，请只需注意定义一个简单的 **Widget** 并不特别困难。

我们并不处理按钮（和其他 **Widget**）在屏幕上看起来如何这一相对复杂和杂乱的问题。问题在于选择近乎无穷，且某些系统规定了某些样式。此外，从编程技术的角度来看，表达按钮的外观并不需要真正的新东西。如果你急不可耐，我们注意到将 **Shape** 放在按钮上方不会影响按钮的功能——而且你知道如何让形状看起来像任何东西。

### 16.4.3 In_box 和 Out_box

我们提供两个 **Widget** 用于文本的输入和输出我们的程序：

```cpp
struct In_box : Widget {
    In_box(Point xy, int w, int h, const string& s)
        :Widget{xy,w,h,s,0} {}
    int get_int();
    string get_string();

    void attach(Window& win);
};
```

