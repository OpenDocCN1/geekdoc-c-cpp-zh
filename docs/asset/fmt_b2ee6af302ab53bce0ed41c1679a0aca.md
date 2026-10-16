
# 第14章 异常处理和事件处理

```
// style of a string of text

namespace RadioB {

    using System;

    using System.Drawing;

    using System.Windows.Forms;

    public class RadioB : Form {

        private Label text = new Label();

        private RadioButton plain = new RadioButton();

        private RadioButton bold = new RadioButton();

        private RadioButton italic = new RadioButton();

        private RadioButton boldItalic = new RadioButton();

        // Constructor for RadioB

        public RadioB() {

            // Initialize the attributes of the text and radio

            // buttons

            text.AutoSize = true;

            text.Text = "In what font style should I appear?";

            plain.Location = new Point(220,0);

            plain.Text = "Plain";

            plain.Checked = true;

            bold.Location = new Point(350, 0);

            bold.Text = "Bold";

            italic.Location = new Point(480, 0);

            italic.Text = "Italics";

            boldItalic.Location = new Point(610, 0);

            boldItalic.Text = "Bold/Italics";

            // Add the text and the radio buttons to the form

            Controls.Add(text);

            Controls.Add(plain);

            Controls.Add(bold);

            Controls.Add(italic);

            Controls.Add(boldItalic);

            // Register the event handler for the radio buttons

            plain.CheckedChanged +=

                new EventHandler(rb_CheckedChanged);

        }

bold.CheckedChanged +=

    new EventHandler(rb_CheckedChanged);

italic.CheckedChanged +=

    new EventHandler(rb_CheckedChanged);

boldItalic.CheckedChanged +=

    new EventHandler(rb_CheckedChanged);

}

// The main method is where execution begins

static void Main() {

    Application.EnableVisualStyles();

    Application.SetCompatibleTextRenderingDefault (false);

    Application.Run(new RadioB());

}

// The event handler

private void rb_CheckedChanged (object o,

                                EventArgs e) {

// Determine which button is on and set the font

// accordingly

if (plain.Checked)

    text.Font =

        new Font( text.Font.Name, text.Font.Size,

                  FontStyle.Regular);

if (bold.Checked)

    text.Font =

        new Font(text.Font.Name, text.Font.Size,

                 FontStyle.Bold);

if (italic.Checked)

    text.Font =

        new Font(text.Font.Name, text.Font.Size,

                 FontStyle.Italic);

if (boldItalic.Checked)

    text.Font =

        new Font(text.Font.Name, text.Font.Size,

                 FontStyle.Italic ^ FontStyle.Bold);

} // End of radioButton_CheckedChanged

} // End of RadioB

}
```

该程序的输出与 图 14.2 所示完全相同。

## 摘要

C++ 没有预定义的异常（标准库中定义的除外）。C++ 异常是原始类型、预定义类或用户定义类的对象。异常通过将 `throw` 语句中表达式的类型连接到处理程序的形参类型来绑定到处理程序。处理程序都具有相同的名称——`catch`。C++ 方法的 `throw` 子句列出了该方法可能抛出的异常类型。

Java 异常是对象，其继承链必须追溯到继承自 `Throwable` 类的类。异常分为两类——已检查和未检查。已检查异常是用户程序和编译器关注的问题。未检查异常可能在任何地方发生，通常被用户程序忽略。

Java 方法的 `throws` 子句列出了它可能抛出但未处理的已检查异常。它必须包含它调用的方法可能引发并向其调用者传播的异常。

Java `finally` 子句提供了一种机制，保证某些代码无论 `try` 复合语句如何终止执行都会被执行。

Java 现在包含 `assert` 语句，这有助于防御性编程。

Python 的异常处理与 Java 类似，只是它在 `try` 构造中添加了 `else` 子句。此外，它使用 `except` 子句而不是 `catch` 子句来定义处理程序，并使用 `raise` 而不是 `throw`。通过 `as` 子句将对象赋给变量来访问异常对象的数据。Python 的 `assert` 语句是一个条件 `raise`。

Ruby 的异常处理与 Python 类似。每个异常类都有两个方法，`message` 和 `backtrace`。异常通常使用带有一个字符串参数的 `raise` 语句引发。这会创建一个新的 `RuntimeError` 对象，其消息为该字符串。`raise` 语句可以通过添加条件表达式使其成为条件语句。异常处理程序的范围通常用 `begin-end` 块指定。处理程序在 `rescue` 子句中定义。`begin-end` 块可以包含 `else` 子句和 `ensure` 子句，后者类似于 Python 和 Java 的 `finally` 子句。

事件是对发生需要特殊处理的事情的通知。事件通常由用户通过图形用户界面与程序的交互创建。Java 事件处理程序通过事件监听器调用。如果要被通知事件发生，事件监听器必须为该事件注册。两个最常用的事件监听器接口是 `actionPerformed` 和 `itemStateChanged`。

Windows Forms 是在 .NET 语言中构建 GUI 组件和处理事件的原始方法。在这种方法中，C# 应用程序通过继承 `Form` 类来构建 GUI。所有 .NET 事件处理程序都使用相同的协议。通过创建 `EventHandler` 对象并将其分配给可以引发事件的 GUI 对象关联的预定义委托来注册事件处理程序。

关于异常处理最重要的与特定编程语言无关的论文之一是 Goodenough（1975）的著作。PL/I 设计中异常处理的缺陷已被涵盖 in MacLaren (1977). C++ 中的异常处理由 Stroustrup (1997) 描述。Java 中的异常处理由 Campione et al. (2001) 描述。

## 复习问题

1. 定义 `exception`、`exception handler`、`raising an exception`、`continuation`、`finalization`，和 `built-in exception`。
2. 早期编程语言是如何支持异常处理机制的？
3. 将异常处理支持内置到语言中的优势是什么？
4. 为什么有些语言不包含异常处理？
5. 给出一个硬件无法检测但由 Java 编译器生成的代码可以检测到的错误示例。
6. Fortran 中标签参数的用途是什么？
7. Java 中异常传播是如何工作的？
8. C++ 中没有操作数的 `throw` 语句如何工作？
9. 如何在 C++ 中编写一个异常处理器，使其处理任何异常？
10. 一个重写了带有 `throw` 子句的函数的函数会面临什么约束？
11. Java 是否包含内置异常？
12. C++ 中哪些库函数支持 `overflow_error` 异常？
13. Java 中 `Throwable` 类的两个系统定义的直接后代是什么？
14. Java 中包含 `ArrayIndexOutOfBoundsException` 的包是什么？
15. 如何在 Java 中编写一个异常处理器，使其处理任何异常？
16. C++ 异常处理器和 Java 异常处理器之间的区别是什么？
17. Java 异常处理器和 Python 异常处理器之间的区别是什么？
18. 一个方法如何处理从另一个方法收到的异常，而该方法在其 `throw` 子句中列出了特定的受检异常？
19. 在 Java 中，`try` 子句何时只有 `finally` 子句而没有异常处理器？
20. 在 Java 中，方法应包含什么子句以传播任何受检异常？
21. 解释 Python 中 `else` 块的作用。
22. `assert` 语句有什么优势？
23. 当 `assert` 语句求值为 false 时会发生什么？
24. Ruby 的 `StandardError` 类的 `message` 方法做什么？
25. 当执行带有字符串参数的 `raise` 语句时到底发生了什么？
26. Python 的 `__debug__` 标志做什么？
27. 异常处理和事件处理有何关联？
28. 定义事件和事件处理器。
29. 什么是事件驱动编程？
30. Java `JTextField` 的用途是什么？
31. Java `ButtonGroup` 的用途是什么？
32. 在 Java GUI 应用程序中，常常用作事件监听器的对象是什么？
33. Java 中事件处理器的协议的起源是什么？
34. 在 Java 中使用什么方法来注册事件处理器？
35. 使用 .NET 的 Windows Forms，构建 C# 应用程序的 GUI 需要什么命名空间？
36. 如何使用 Windows Forms 在窗体中定位组件？
37. .NET 事件处理器的协议是什么？
38. 必须创建什么类的对象来注册 .NET 事件处理器？
39. 委托在注册事件处理器的过程中扮演什么角色？

## 问题集

1. C 的设计者为了不要求下标范围检查，获得了什么回报？
2. 编写一个 Fortran `Read` 语句，如果发生错误则将控制转移到语句 200，如果读操作遇到文件结束条件则将控制转移到语句 950。
3. 从 PL/I 和 Ada 编程语言的教科书中查找各自的内置异常集。对两者进行比较评估，考虑完整性和灵活性。
4. 从 COBOL 的教科书中确定 COBOL 程序中是如何进行异常处理的。
5. 在没有异常处理设施的语言中，常见的做法是让大多数子程序包含一个 `error` 参数，可以将其设置为表示 `OK` 的某个值或表示 `procedure` 中出错的其他值。Java 这样的语言式异常处理设施与这种方法相比有什么优势？
6. 在没有异常处理设施的语言中，我们可以将错误处理过程作为参数传递给每个可能检测到必须处理的错误的程序。这种方法有什么缺点？
7. 比较问题 5 和 6 中提出的方法。你认为哪一种更好，为什么？
8. 编写 C++ 的 `throw` 子句与 Java 的 `throws` 子句的比较分析。
9. 考虑以下 C++ 骨架程序：

```cpp
class Big {

	int i;

	float f;

	void fun1() throw int {

		...

		try {

			throw i;

			throw f;

			...

		}

		catch(float) { ... }

	}

}

class Small {

	int j;

	float g;

	void fun2() throw float {

		...

		try {

			try {

				Big.fun1();

				...

				throw j;

				throw g;

				...

			}

			catch(int) { ... }

		}

		catch(float) { ... }

	}

}
```
