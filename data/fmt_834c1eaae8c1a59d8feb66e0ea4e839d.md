
在玩弄了一段时间后，我们决定我们真正想要的是一个“弹出菜单”；也就是说，除了在使用时之外，我们不想在菜单上花费宝贵的屏幕空间。所以，我们添加了一个“color menu”按钮。当我们按下它时，颜色菜单会弹出来，当我们做出选择后，菜单再次隐藏，按钮重新出现。

首先这是在添加了几条线之后的窗口：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_604_0.png)

我们看到新的“color menu”按钮和一些（黑色）线条。按下“color menu”，菜单出现：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_604_1.png)

请注意，“color menu”按钮现在被隐藏了。在完成菜单之前我们不需要它。按下“blue”，我们得到

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_605_0.png)

线条现在是蓝色的，并且“color menu”按钮重新出现。

为了实现这一点，我们添加了“color menu”按钮并修改了“pressed”函数以调整菜单和按钮的可见性。这是我们在所有修改后的完整 `Lines_window`：

```cpp
struct Lines_window : Window {
    Lines_window(Point xy, int w, int h, const string& title);
private:
// 数据：
Open_polyline lines;

// 小部件：
Button next_button; // 将 (next_x,next_y) 添加到 lines
Button quit_button; // 结束程序
In_box next_x;
In_box next_y;
Out_box xy_out;
Menu color_menu;
Button menu_button;

void change(Color c) { lines.set_color(c); }

void hide_menu() { color_menu.hide(); menu_button.show(); }

// 由回调调用的动作：
void red_pressed() { change(Color::red); hide_menu(); }
void blue_pressed() { change(Color::blue); hide_menu(); }
void black_pressed() { change(Color::black); hide_menu(); }
void menu_pressed() { menu_button.hide(); color_menu.show(); }
void next();
void quit();

// 回调函数：
static void cb_red(Address, Address);
static void cb_blue(Address, Address);
static void cb_black(Address, Address);
static void cb_menu(Address, Address);
static void cb_next(Address, Address);
static void cb_quit(Address, Address);
};
```

注意除构造函数外所有内容都是私有的。基本上，`Window` 类就是程序。发生的一切都是通过其回调发生的，因此不需要窗口外部的代码。我们稍微整理了声明，希望使类更可读。构造函数为所有子对象提供参数并将它们附加到窗口：

```cpp
Lines_window::Lines_window(Point xy, int w, int h, const string& title)
    : Window(xy, w, h, title),
    next_button(Point{x_max()-150,0}, 70, 20, "Next point", cb_next),
    quit_button(Point{x_max()-70,0}, 70, 20, "Quit", cb_quit),
    next_x{Point{x_max()-310,0}, 50, 20, "next x:"},
    next_y{Point{x_max()-210,0}, 50, 20, "next y:"},
    xy_out{Point{100,0}, 100, 20, "current (x,y):"},
    color_menu{Point{x_max()-70,30},70,20,Menu::vertical,"color"},
    menu_button{Point{x_max()-80,30}, 80, 20, "color menu", cb_menu}
{
    attach(next_button);
    attach(quit_button);
    attach(next_x);
    attach(next_y);
    attach(xy_out);
    xy_out.put("no point");
    color_menu.attach(new Button{Point{0,0},0,0,"red",cb_red});
    color_menu.attach(new Button{Point{0,0},0,0,"blue",cb_blue});
    color_menu.attach(new Button{Point{0,0},0,0,"black",cb_black});
    attach(color_menu);
    color_menu.hide();
    attach(menu_button);
    attach(lines);
}
```

注意初始化器的顺序与数据成员定义的顺序相同。这是编写初始化器的正确顺序。事实上，成员初始化器始终按其数据成员声明的顺序执行。一些编译器（乐于助人地）如果在指定基类或成员构造函数时顺序错误，会给出警告。

## 16.8 调试 GUI 代码

一旦 GUI 程序开始工作，调试通常很容易：你看到的就是你得到的。然而，在第一个形状和小部件开始在窗口中显示之前，甚至在窗口出现在屏幕上之前，往往有一段最令人沮丧的时期。试试这个 `main()`：

```cpp
int main()
{
    Lines_window {Point{100,100},600,400,"lines"};
    return gui_main();
}
```

你看到错误了吗？无论你是否看到，你都应该尝试一下；程序将编译并运行，但 `Lines_window` 并没有给你画线的机会，你最多只能看到屏幕上的闪烁。你如何在这种程序中找到错误？

- 通过仔细使用经过考验的程序部分（类、函数、库）
- 通过简化所有新代码，通过从最简单的版本缓慢“生长”程序，通过仔细逐行检查代码
- 通过检查所有链接器设置
- 通过与已经正常工作的程序比较代码
- 通过向朋友解释代码

你会发现很难做到的一件事是跟踪代码的执行。如果你学会了使用调试器，你还有机会，但在这种情况下仅仅插入“输出语句”行不通——问题是没有输出出现。即使是调试器也会有问题，因为同时有许多事情在发生（“多线程”）– 你的代码不是唯一试图与屏幕交互的代码。简化代码和系统地理解代码是关键。

那么问题出在哪里呢？以下是正确的版本（见 §16.5）：

```cpp
int main()
{
  Lines_window win{Point{100,100},600,400,"lines"};
  return gui_main();
}
```

我们“忘记”了 `Lines_window win` 这个名称。由于实际上并不需要那个名称，这似乎很合理，但编译器随后决定，既然我们没有使用那个窗口，它就可以立即将其销毁。哎呀！那个窗口仅存在了大约一毫秒的时间。难怪我们没看到它。

另一个常见问题是将一个窗口*精确地*放置在另一个窗口之上。这显然（或者更准确地说，完全不显然）看起来就像只有一个窗口。另一个窗口去哪了？我们可能会花大量时间去寻找代码中并不存在的 bug。如果我们将一个图形放置在另一个图形之上，也会发生同样的问题。

最后——使情况变得更糟的是——当我们使用 GUI 库时，异常并不总是像我们希望的那样工作。由于我们的代码由 GUI 库管理，我们抛出的异常可能永远无法到达我们的处理程序——库或操作系统可能会“吞掉”它（也就是说，它们可能依赖于与 C++ 异常不同的错误处理机制，并且可能完全不知道 C++ 的存在）。

在调试过程中发现的常见问题包括 `Shapes`（形状）和 `Widgets`（控件）因为没有附加（`attach`）而没有显示，以及对象因为超出了作用域而出现行为异常。让我们考虑一下程序员可能如何提取菜单中按钮的创建和附加过程：

```cpp
// helper function for loading buttons into a menu
void load_disaster_menu(Menu&m)
{
  Point orig {0,0};
  Button b1 {orig,0,0,"flood",cb_flood};
  Button b2 {orig,0,0, "fire",cb_fire};
  // . . .
  m.attach(b1);
  m.attach(b2);
  // . . .
}
```

```cpp
int main()
{
    // ... 
    Menu disasters {Point{100,100},60,20,Menu::horizontal,"disasters"};
    load_disaster_menu(disasters);
    win.attach(disasters);
    // ... 
}
```

这样行不通。所有这些按钮都是 `load_disaster_menu` 函数的局部变量，将它们附加到菜单不会改变这一事实。可以在 §18.6.4（*不要返回指向局部变量的指针*）中找到解释，§8.5.8 展示了局部变量的内存布局图解。故事的核心是，在 `load_disaster_menu()` 返回后，这些局部对象已被销毁，而 `disasters` 菜单指向的是不存在（已销毁）的对象。结果可能是令人惊讶且并不好看的。解决方案是使用由 `new` 创建的未命名对象，而不是命名的局部对象：

```cpp
// helper function for loading buttons into a menu
void load_disaster_menu(Menu& m)
{
    Point orig {0,0};
    m.attach(new Button{orig,0,0,"flood",cb_flood});
    m.attach(new Button{orig,0,0,"fire",cb_fire});
    // ... 
}
```

正确的解决方案甚至比（非常常见的）bug 还要简单。

## 练习

- 1. 创建一个完全新项目，配置用于 FLTK 的链接器设置（如附录 D 中所述）。
- 2. 使用 `Graph_lib` 的功能，输入 §16.5 中的线条绘制程序并使其运行。
- 3. 修改该程序，使用 §16.7 中描述的弹出式菜单，并使其运行。
- 4. 修改程序，添加一个用于选择线条样式的第二个菜单，并使其运行。

## 复习题

- 1. 为什么你需要图形用户界面？
- 2. 什么时候你会需要非图形用户界面？
- 3. 什么是软件层？
- 4. 为什么要分层软件？
- 5. 从 C++ 与操作系统通信时的根本问题是什么？
- 6. 什么是回调（callback）？
- 7. 什么是控件（widget）？
- 8. 控件的另一个名称是什么？
- 9. 缩写 FLTK 代表什么？
- 10. 你如何发音 FLTK？
- 11. 你还听说过哪些其他 GUI 工具包？
- 12. 哪些系统使用*控件*（widget）一词，哪些更喜欢使用*控制*（control）？
- 13. 控件的例子有哪些？
- 14. 什么时候使用收件箱（inbox）？
- 15. 存储在收件箱中的值的类型是什么？
- 16. 什么时候使用按钮？
- 17. 什么时候使用菜单？
- 18. 什么是控制反转？
- 19. 调试 GUI 程序的基本策略是什么？
- 20. 为什么调试 GUI 程序比调试“使用流进行 I/O 的普通程序”更困难？

## 术语

- 按钮（button）
- 回调（callback）
- 控制台 I/O（console I/O）
- 控制（control）
- 控制反转（control inversion）
- 对话框（dialog box）
- GUI（图形用户界面）
- 菜单（menu）
- 软件层（software layer）
- 用户界面（user interface）
- 可见/隐藏（visible/hidden）
- 等待输入（waiting for input）
- 等待循环（wait loop）
- 控件（widget）

### 习题

- 1. 创建一个 `My_window`，它有点像 `Simple_window`，但它有两个按钮：`next` 和 `quit`。
- 2. 制作一个基于 `My_window` 的窗口，其中包含一个 4x4 的方形按钮棋盘。按下按钮时，执行一个简单的操作，例如在输出框中打印其坐标，或者变成略有不同的颜色（直到按下另一个按钮）。
- 3. 将一个 `Image` 放置在一个 `Button` 上方；当按下按钮时，两者一起移动。使用 `std_lib_facilities.h` 中的这个随机数生成器为“图像按钮”选择一个新位置：

```cpp
#include<random>

inline int rand_int(int min, int max)
{
    static default_random_engine ran;
    return uniform_int_distribution<>(min,max)(ran);
}
```

它返回 `[min,max)` 范围内的一个随机 `int`。
- 4. 制作一个菜单，项目分别用于创建圆形、正方形、等边三角形和六边形。制作一个输入框（或两个）用于输入坐标对，并将按下菜单项所创建的图形放置在该坐标处。抱歉，不支持拖放。
- 5. 编写一个程序，绘制你选择的形状，并在每次点击“Next”时将其移动到一个新点。新点应由从输入流读取的坐标对确定。
- 6. 制作一个“模拟时钟”，即一个指针会移动的时钟。你通过库调用从操作系统获取时间。这个练习的一个重要部分是找到给你提供一天中时间的函数，以及一种等待短时间的（例如，时钟滴答一秒）方法，并根据你找到的文档学习如何使用它们。提示：`clock()`, `sleep()`。
- 7. 使用前面练习中开发的技术，让一架飞机图像在窗口中“飞行”。设有一个“Start”和一个“Stop”按钮。
- 8. 提供一个货币转换器。启动时从文件读取汇率。在输入窗口中输入金额，并提供一种选择要转换的源货币和目标货币的方法（例如，一对菜单）。
- 9. 修改第 7 章中的计算器，使其从输入框获取输入，并在输出框中返回结果。
- 10. 提供一个程序，你可以从中选择一组函数（例如，`sin()` 和 `log()`），为这些函数提供参数，然后绘制它们的图形。

## 跋

GUI 是一个巨大的主题。其中很多涉及风格以及与现有系统的兼容性。此外，很多涉及令人眼花缭乱的控件多样性（例如，GUI 库提供数十种替代的按钮样式），这会让一位传统的植物学家感到宾至如归。然而，其中很少有涉及基本编程技术的，所以我们不会朝那个方向深入。其他主题，如缩放、旋转、变形、三维对象、阴影等，需要我们在图形和/或数学方面的专业知识，而这里我们不作假设。

你应该意识到的一件事是，大多数 GUI 系统都提供一个“GUI 构建器”，允许你以图形方式设计窗口布局，并将回调和操作附加到按钮、菜单等。以图形方式指定。对于许多应用程序，使用这样的 GUI 构建器来减少编写“脚手架代码”（如我们的回调）的繁琐工作是非常值得的。然而，始终要试图理解结果程序是如何工作的。有时，生成的代码与你在本章中看到的内容等价。有时则使用更复杂和/或成本更高的机制。

# 第三部分

# 数据与算法

*此页故意留白*

## 17 向量与自由存储区

> “让 vector 成为默认选择！”
> — Alex Stepanov

本章及接下来的四章将介绍 C++ 标准库中的容器和算法部分，传统上被称为 STL（标准模板库）。我们将描述 STL 的关键设施及其一些用途。此外，我们还会呈现用于实现 STL 的关键设计和编程技术，以及为此使用的一些低级语言特性。这些特性包括指针、数组和自由存储区。本章及接下来两章的重点是最常见且最实用的 STL 容器——`vector`（向量）的设计和实现。

### 17.1 引言

C++ 标准库中最有用的容器是 `vector`。`vector` 提供了一组给定类型的元素序列。你可以通过索引（下标）引用某个元素，使用 `push_back()` 扩展 `vector`，使用 `size()` 询问 `vector` 中元素的数量，并可以访问 `vector`，同时系统会检查是否有试图访问越界元素的行为。标准库中的 `vector` 是一个方便、灵活、高效（在时间和空间上）且静态类型安全的元素容器。标准字符串（`string`）具有类似的特性，其他有用的标准容器类型也是如此，例如我们将在第 20 章中介绍的 `list` 和 `map`。然而，计算机的内存并不直接支持如此有用的类型。硬件直接支持的是字节序列。例如，对于 `vector<double>`，操作 `v.push_back(2.3)` 会将 2.3 添加到 `double` 序列中，并使 `v` 的元素计数（`v.size()`）增加 1。在最低层级，计算机并不知道像 `push_back()` 这样复杂的东西；它只知道如何一次读写几个字节。
