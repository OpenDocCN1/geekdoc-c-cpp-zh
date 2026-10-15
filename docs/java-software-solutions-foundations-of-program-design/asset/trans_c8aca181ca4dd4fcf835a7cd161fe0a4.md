

## 代码清单 4.12

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

## 显示效果

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_224_0.png)

## 代码清单 4.13

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

同一个监听器可以同时用于监听多个组件。因此，可以将该监听器同时添加到文本框和按钮上，给用户提供选择。按下按钮或 Enter 键都会执行转换。这些变体作为编程项目留给读者。

## 自测题（答案见附录 N）

- SR 4.34 描述在 Fahrenheit 程序中，当用户在界面的文本框中输入一个数字并按 Enter（或 Return）键时会发生什么。
- SR 4.35 修改 FahrenheitPanel 类，使得当用户在文本字段中输入数字时，文本字段下方会出现形如“X 华氏度 = Y 摄氏度”的语句。例如，如果用户输入 223，则显示“223 华氏度 = 106 摄氏度”，而不是“摄氏温度：106”。

## 关键概念总结

- 面向对象编程的核心是定义类，这些类表示具有良好定义的状态和行为的对象。
- 变量的作用域决定了它可以在何处被引用，它取决于变量声明的位置。
- UML 类图帮助我们直观地了解程序中各类的内容以及它们之间的关系。
- 对象应该被封装，以保护其数据不被不恰当地访问。
- 实例变量应声明为私有可见性，以促进封装。
- 大多数对象包含访问器和修改器方法，以便客户端以受控方式管理数据。
- 方法返回的值必须与方法头中指定的返回类型一致。
- 调用方法时，实际参数会被复制到形式参数中。
- 在方法中声明的变量是该方法的局部变量，不能在方法之外使用。
- 构造函数不能有任何返回类型，即使是 void 也不行。
- GUI 由组件、表示用户操作的事件以及响应这些事件的监听器组成。
- 监听器通常定义为内部类，因为监听器与 GUI 组件之间存在密切关系。

## 练习

访问 www.myprogramminglab.com 在线完成这些练习中的许多题目，并获得即时反馈。

- **EX 4.1** 对于以下每一对，哪一个是类，哪一个是该类的对象？
  - a. Superhero, Superman
  - b. Justin, Person
  - c. Rover, Pet
  - d. Magazine, Time
  - e. Christmas, Holiday
- **EX 4.2** 列出可能为表示相框的名为 PictureFrame 的类定义的一些属性和操作。
- **EX 4.3** 列出可能为表示商务会议的名为 Meeting 的类定义的一些属性和操作。
- **EX 4.4** 列出可能为表示大学课程的名为 Course 的类定义的一些属性和操作（不是某一次具体的课程开设，而是泛指这门课程）。
- **EX 4.5** 编写一个名为 lyrics 的方法，调用时打印一首歌的歌词。该方法不应接受任何参数，也不应返回任何值。
- **EX 4.6** 编写一个名为 cube 的方法，接受一个整数参数，并返回该值的三次幂。
- **EX 4.7** 编写一个名为 random100 的方法，返回 1 到 100（含）之间的随机整数。
- **EX 4.8** 编写一个名为 randomInRange 的方法，接受两个表示范围的整数参数。该方法应返回指定范围（含）内的随机整数。假设第一个参数小于第二个参数。
- **EX 4.9** 编写一个名为 randomColor 的方法，创建并返回一个表示随机颜色的 Color 对象。回想一下，Color 对象可以由三个 0 到 255 之间的整数值定义，分别表示红、绿、蓝的贡献（即其 RGB 值）。
- **EX 4.10** 绘制一个 UML 类图，显示 Transactions 程序中所用类之间的关系。
- **EX 4.11** 绘制一个 UML 类图，显示 PushCounter 程序中所用类之间的关系。
- **EX 4.12** 绘制一个 UML 类图，显示 Fahrenheit 程序中所用类之间的关系。

## 编程项目

访问 www.myprogramminglab.com 在线完成这些编程项目中的许多题目，并获得即时反馈。

- **PP 4.1** 设计并实现一个名为 Sphere 的类，该类包含表示球体直径的实例数据。定义 Sphere 构造函数以接收并初始化直径，并为直径提供 getter 和 setter 方法。包含计算并返回球体体积和表面积的方法（公式见 PP 3.5）。包含一个 toString 方法，返回球体的一行描述。创建一个名为 MultiSphere 的驱动类，其 main 方法实例化并更新多个 Sphere 对象。
- **PP 4.2** 设计并实现一个名为 Dog 的类，包含表示狗的姓名和年龄的实例数据。定义 Dog 构造函数以接收并初始化实例数据。为姓名和年龄提供 getter 和 setter 方法。包含一个计算并返回狗的“人类年龄”（狗龄的七倍）的方法。包含一个 toString 方法，返回狗的一行描述。创建一个名为 Kennel 的驱动类，其 main 方法实例化并更新多个 Dog 对象。
- **PP 4.3** 设计并实现一个名为 Car 的类，包含表示汽车品牌、型号和年份的实例数据。定义 Car 构造函数以初始化这些值。为所有实例数据提供 getter 和 setter 方法，并提供一个 toString 方法返回汽车的一行描述。创建一个名为 CarTest 的驱动类，其 main 方法实例化并更新多个 Car 对象。
- **PP 4.4** 设计并实现一个名为 Box 的类，包含表示盒子的高度、宽度和深度的实例数据。另外包含一个名为 full 的布尔变量作为实例数据，表示盒子是否已满。定义 Box 构造函数以接收并初始化盒子的高度、宽度和深度。每个新创建的 Box 都是空的（构造函数应将 full 初始化为 false）。为所有实例数据提供 getter 和 setter 方法。包含一个 toString 方法，返回盒子的一行描述。创建一个名为 BoxTest 的驱动类，其 main 方法实例化并更新多个 Box 对象。
- **PP 4.5** 设计并实现一个名为 Book 的类，包含标题、作者、出版社和版权日期的实例数据。定义 Book 构造函数以接收并初始化这些数据。为所有实例数据提供 getter 和 setter 方法。包含一个 toString 方法，返回格式良好、多行的书籍描述。创建一个名为 Bookshelf 的驱动类，其 main 方法实例化并更新多个 Book 对象。
- **PP 4.6** 设计并实现一个名为 Flight 的类，表示一次航班。它应包含表示以下内容的实例数据：

  ![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_229_0.png)

