
### DISPLAY

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_220_0.png)

此程序中使用的组件包括一个按钮、一个用于显示计数的标签、一个用于组织 GUI 的面板，以及一个用于显示面板的框架。面板由 `PushCounterPanel` 类定义，见第 4.11 节。

推按钮是一个允许用户通过鼠标按下发起操作的组件。我们在后面的章节中会探索其他类型的按钮组件。推按钮由 `JButton` 类定义。

### LISTING 4.11

```java

//***********************************************************

//  PushCounterPanel.java      Author: Lewis/Loftus

//

//  Demonstrates a graphical user interface and an event listener.

//***********************************************************

import java.awt.*;

import java.awt.event.*;

import javax.swing.*;

public class PushCounterPanel extends JPanel

{

    private int count;

    private JButton push;

    private JLabel label;

    //------------------------------------------------------------

    // Constructor: Sets up the GUI.

    //------------------------------------------------------------

    public PushCounterPanel ()

    {

        count = 0;

        push = new JButton ("Push Me!");

        push.addActionListener (new ButtonListener());

        label = new JLabel ("Pushes: " + count);

        add (push);

        add (label);

        setPreferredSize (new Dimension(300, 40));

        setBackground (Color.cyan);

    }

    //****************************************************************

    // Represents a listener for button push (action) events.

    //****************************************************************

    private class ButtonListener implements ActionListener

    {

        //------------------------------------------------------------

        // Updates the counter and label when the button is pushed.

        //------------------------------------------------------------

        public void actionPerformed (ActionEvent event)

        {

            count++;

            label.setText("Pushes: " + count);

        }

    }

}

```

`PushCounterPanel` 构造函数设置了 GUI。`JButton` 构造函数的调用接受一个 `String` 参数，该参数指定按钮上显示的文本。按钮和标签被添加到面板中。

此程序中唯一感兴趣的事件是按钮被按下时发生的事件。为了响应该事件，我们必须为该事件创建监听器对象，因此我们必须编写一个表示监听器的类。

`JButton` 在被按下时会生成一个动作事件。因此我们编写的监听器类将是一个动作事件监听器。在此程序中，我们定义了一个名为 `ButtonListener` 的类来表示该事件的监听器。

我们可以在自己的文件中编写 `ButtonListener` 类，甚至可以在同一文件中但在 `PushCounterPanel` 类之外编写它。然而，这样我们就必须设置监听器与监听器更新的 GUI 组件之间通信的方式。相反，我们将 `ButtonListener` 类定义为内部类，即在另一个类中定义的类。作为内部类，它自动可以访问包含它的类的成员。你只有在两个类之间存在密切关系并且内部类不被任何其他类访问的情况下才应创建内部类。监听器与其 GUI 之间的关系是内部类合适的少数情况之一。

> **KEY CONCEPT**
> 由于监听器与 GUI 组件之间存在密切关系，监听器通常被定义为内部类。

监听器类是通过实现接口编写的，接口是实现类必须定义的方法列表。Java 标准类库为许多类型的事件包含接口。通过实现 `ActionListener` 接口创建动作监听器；因此，我们在 `ButtonListener` 类中包含 `implements` 子句。接口将在第 7 章中更详细地讨论。

`ActionListener` 接口中列出的唯一方法是 `actionPerformed` 方法，因此 `ButtonListener` 类必须实现的也只有该方法。生成动作事件的组件（在本例中为按钮）会在事件发生时调用 `actionPerformed` 方法，并传入表示该事件的 `ActionEvent` 对象。有时我们会使用事件对象，有时仅知道事件发生了就足够了。在本例中，我们不需要与事件对象交互。当事件发生时，监听器递增 `count` 并使用 `setText` 方法重置标签的文本。

记住，我们不仅要为事件创建监听器，还必须设置监听器与将生成事件的组件之间的关系。为此，我们通过调用适当的方法将监听器添加到组件中。在 `PushCounterPanel` 构造函数中，我们调用 `addActionListener` 方法，并传入一个新实例化的 `ButtonListener` 对象。

仔细回顾此示例，注意它是如何完成创建交互式基于 GUI 程序的三个关键步骤的。它创建并设置 GUI 组件，创建感兴趣事件的适当监听器，并设置监听器与将生成事件的组件之间的关系。

### 自测题（答案见附录 N）

- SR 4.32 推按钮（`JButton` 对象）会生成什么类型的事件？
- SR 4.33 你将如何更改 `PushCounterPanel` 类，使其不再显示按钮被按下的次数计数，而是显示计数“轨迹”？按下一次后显示“01”；按下两次后显示“012”；按下五次后显示“012345”；以此类推。

## 4.9 文本字段

让我们看另一个使用另一个组件的示例：文本字段。第 4.12 节所示的 `Fahrenheit` 程序展示了一个 GUI，其中包含一个文本字段，用户可以在其中输入华氏温度。当用户按下 Enter（或 Return）键时，等效的摄氏温度将被显示。

`Fahrenheit` 程序的界面在 `FahrenheitPanel` 类中设置。文本字段是 `JTextField` 类的对象。`JTextField` 构造函数接受一个整数参数，该参数指定字段的大小，以字符数为单位，基于当前默认字体。

文本字段和各种标签被添加到面板以便显示。请记住，面板受流式布局管理器控制，该管理器尽可能在一行上放置尽可能多的组件。因此，如果你调整框架大小，标签和文本字段的方向可能会发生变化。我们将在第 7 章详细研究布局管理器，提供更多控制组件布局的选项。

如果光标当前位于文本字段中，按下 Enter 或 Return 键时，文本字段组件会生成一个动作事件。因此我们需要设置一个监听器对象来响应动作事件。正如我们在上一节的 PushCounter 程序中所做的那样，我们将监听器定义为实现 `ActionListener` 接口的内部类。

当用户按下 Enter 键时，文本字段组件会调用 `actionPerformed` 方法。该方法首先通过调用其 `getText` 方法从文本字段中检索文本，该方法返回一个字符字符串。然后使用 `Integer` 包装类的 `parseInt` 方法将文本转换为整数。随后该方法执行计算以确定等效的摄氏温度，并用结果设置相应标签的文本。

请注意，推按钮和文本字段会生成同一种事件：动作事件。因此，`Fahrenheit` 程序设计的另一种选择是向 GUI 添加一个 `JButton` 对象，当用户使用鼠标按下按钮时触发转换。更进一步，相同的监听器对象可以

### 代码清单 4.12

```java

//****************************************************************

//      Fahrenheit.java      Author: Lewis/Loftus

//

//  Demonstrates the use of text fields.

//****************************************************************

import javax.swing.JFrame;

public class Fahrenheit

{

    //-------------------------------------------------------------

    // Creates and displays the temperature converter GUI.

    //-------------------------------------------------------------

    public static void main (String[] args)

    {

        JFrame frame = new JFrame ("Fahrenheit");

        frame.setDefaultCloseOperation (JFrame.EXIT_ON_CLOSE);

        FahrenheitPanel panel = new FahrenheitPanel();

        frame.getContentPane().add(panel);

        frame.pack();

        frame.setVisible(true);

    }

}

```

### 显示效果

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_224_0.png)

### 代码清单 4.13

```java

//****************************************************************

// FahrenheitPanel.java      Author: Lewis/Loftus

//

// Demonstrates the use of text fields.

//****************************************************************

import java.awt.*;

import java.awt.event.*;

import javax.swing.*;

public class FahrenheitPanel extends JPanel

{

    private JLabel inputLabel, outputLabel, resultLabel;

    private JTextField fahrenheit;

    //-------------------------------------------------------------

    // Constructor: Sets up the main GUI components.

    //-------------------------------------------------------------

    public FahrenheitPanel()

    {

        inputLabel = new JLabel ("Enter Fahrenheit temperature:");

        outputLabel = new JLabel ("Temperature in Celsius: ");

        resultLabel = new JLabel ("---");

        fahrenheit = new JTextField (5);

        fahrenheit.addActionListener (new TempListener());

        add (inputLabel);

        add (fahrenheit);

        add (outputLabel);

        add (resultLabel);

        setPreferredSize (new Dimension(300, 75));

        setBackground (Color.yellow);

    }

    //****************************************************************

    // Represents an action listener for the temperature input field.

    //****************************************************************

    private class TempListener implements ActionListener

    {

        //------------------------------------------------------------

        // Performs the conversion when the enter key is pressed in

        // the text field.

        //------------------------------------------------------------

        public void actionPerformed (ActionEvent event)

        {

            int fahrenheitTemp, celsiusTemp;

            String text = fahrenheit.getText();

            fahrenheitTemp = Integer.parseInt (text);

            celsiusTemp = (fahrenheitTemp-32) * 5/9;

            resultLabel.setText (Integer.toString (celsiusTemp));

        }

    }

}
```
