
| java.util.prefs.Preferences 1.4 *（续）* |
|---|
| • `String get(String key, String defval)`<br>• `int getInt(String key, int defval)`<br>• `long getLong(String key, long defval)`<br>• `float getFloat(String key, float defval)`<br>• `double getDouble(String key, double defval)`<br>• `boolean getBoolean(String key, boolean defval)`<br>• `byte[] getByteArray(String key, byte[] defval)`<br>返回与给定键关联的值；如果该键没有关联的值、关联值类型不正确或偏好设置存储不可用，则返回提供的默认值。<br>• `void put(String key, String value)`<br>• `void putInt(String key, int value)`<br>• `void putLong(String key, long value)`<br>• `void putFloat(String key, float value)`<br>• `void putDouble(String key, double value)`<br>• `void putBoolean(String key, boolean value)`<br>• `void putByteArray(String key, byte[] value)`<br>将键/值对存储到此节点中。<br>• `void exportSubtree(OutputStream out)`<br>将此节点及其子节点的偏好设置写入指定流。<br>• `void exportNode(OutputStream out)`<br>将此节点（但不包括其子节点）的偏好设置写入指定流。<br>• `void importPreferences(InputStream in)`<br>导入指定流中包含的偏好设置。 |

这结束了我们对图形用户界面编程的介绍。下一章将向你展示如何使用最常见的Swing组件。

## 第11章：使用Swing的用户界面组件

### 本章内容

- 11.1 Swing与模型-视图-控制器设计模式，第632页
- 11.2 布局管理简介，第636页
- 11.3 文本输入，第643页
- 11.4 选择组件，第651页
- 11.5 菜单，第671页
- 11.6 复杂的布局管理，第690页
- 11.7 对话框，第706页

上一章主要向你展示了如何在Java中使用事件模型。在此过程中，你迈出了学习如何构建图形用户界面的第一步。本章将向你展示构建功能更完整的图形用户界面所需的最重要工具。

我们首先概述Swing的架构基础。了解“幕后”发生的事情对于有效地使用一些更高级的组件非常重要。然后，我们向你展示Swing中最常见的用户界面组件，例如文本字段、单选按钮和菜单。接下来，你将学习如何使用布局管理器来排列这些组件。最后，你将看到如何在Swing中实现对话框。

本章涵盖基本Swing组件，如文本组件、按钮和滑块。这些是你最常需要的基本用户界面组件。我们将在第二卷中介绍高级Swing组件。

### 11.1 Swing与模型-视图-控制器设计模式

让我们退一步想一想，构成一个用户界面组件的各个部分，例如按钮、复选框、文本字段或复杂的树控件。每个组件都有三个特性：

- 它的*内容*，例如按钮的状态（是否按下）或文本字段中的文本
- 它的*视觉外观*（颜色、大小等）
- 它的*行为*（对事件的反应）

即使是像按钮这样一个看似简单的组件，在这些特性之间也表现出一定程度的复杂交互。显然，按钮的视觉外观取决于*外观风格*。Metal按钮看起来与Windows按钮或Motif按钮不同。此外，外观取决于按钮状态；当按钮被按下时，需要重新绘制以使其看起来不同。状态取决于按钮接收到的事件。当用户在按钮内按下鼠标时，按钮就被按下了。

当然，当你在程序中使用按钮时，你只是把它当作一个*按钮*；你不会过多考虑其内部工作原理和特性。毕竟，这是实现按钮的程序员的工作。然而，实现按钮和所有其他用户界面组件的程序员有必要对它们多加思考，以便无论采用何种*外观风格*，它们都能很好地工作。

为此，Swing设计者采用了一种著名的设计模式：*模型-视图-控制器*（MVC）模式。这种设计模式要求我们提供三个独立的对象：

- *模型*，存储内容
- *视图*，显示内容
- *控制器*，处理用户输入

自动刷新自身。当然，对于像按钮这样简单的用户界面组件，你不会拥有同一模型的多个视图。

![](img/127bccebb2cfadea3f02579edaad63c3_660_0.png)

**图11.2** 同一模型的两种不同视图

控制器处理用户输入事件，例如鼠标点击和按键。然后它决定是将这些事件转换为模型或视图的变化。例如，如果用户在文本框中按下一个字符键，控制器会调用模型的“插入字符”命令。然后模型告诉视图更新自身。视图永远不会知道文本为什么改变。但如果用户按下光标键，控制器可能会告诉视图滚动。滚动视图对底层文本没有影响，因此模型永远不知道这个事件发生了。

图11.3显示了模型、视图和控制器对象之间的交互。

![](img/127bccebb2cfadea3f02579edaad63c3_661_0.png)

**图11.3** 模型、视图和控制器对象之间的交互

对于大多数Swing组件，模型类实现了一个名称以`Model`结尾的接口；在这种情况下，该接口被称为`ButtonModel`。实现该接口的类可以定义各种按钮的状态。实际上，按钮并不那么复杂，Swing库中包含一个名为`DefaultButtonModel`的类来实现该接口。

通过查看`ButtonModel`接口的属性，你可以了解按钮模型维护的数据类型——参见表11.1。

每个`JButton`对象都存储一个按钮模型对象，你可以获取它。

```java
var button = new JButton("Blue");
ButtonModel model = button.getModel();
```

在实践中，你并不关心——按钮状态的细节只对绘制它的视图有意义。所有重要的信息——例如按钮是否启用——都可以从`JButton`类中获取。（当然，然后`JButton`会请求其模型来检索该信息。）

**表11.1** `ButtonModel`接口的属性

| 属性名 | 值 |
|---|---|
| `actionCommand` | 与此按钮关联的操作命令字符串 |
| `mnemonic` | 此按钮的键盘助记符 |
| `armed` | 如果按钮被按下且鼠标仍在按钮上，则为true |
| `enabled` | 如果按钮可选择，则为true |
| `pressed` | 如果按钮被按下但鼠标按钮尚未释放，则为true |
| `rollover` | 如果鼠标位于按钮上方，则为true |
| `selected` | 如果按钮已被切换为打开状态（用于复选框和单选按钮），则为true |

再看一下`ButtonModel`接口，看看它*没有*什么。模型不存储按钮标签或图标。仅仅通过查看模型，无法知道按钮表面上是什么。（实际上，正如你将要在第11.4.2节“单选按钮”第654页看到的，这种设计上的纯粹性给程序员带来了些许烦恼。）

同样值得注意的是，相同的模型（即`DefaultButtonModel`）被用于普通按钮、单选按钮、复选框甚至菜单项。当然，这些按钮类型中的每一种都有不同的视图和控制器。当使用Metal外观风格时，`JButton`使用名为`BasicButtonUI`的类作为视图，并使用名为`ButtonListener`的类作为控制器。通常，每个Swing组件都有一个以UI结尾的关联视图对象。但并非所有Swing组件都有专门的控制器对象。

所以，在阅读了关于`JButton`幕后情况的简短介绍后，你可能会想：`JButton`到底是什么？它只是一个继承自`JComponent`的包装类，保存着`DefaultButtonModel`对象、一些视图数据（如按钮标签和图标），以及一个负责按钮视图的`BasicButtonUI`对象。

### 11.2 布局管理简介

在我们继续讨论单独的Swing组件（如文本字段和单选按钮）之前，我们先简要介绍如何在一个窗口内排列这些组件。
