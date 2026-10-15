

```java
/**************************************************************
//  BullseyePanel.java        Author: Lewis/Loftus
//
//  Demonstrates the use of conditionals and loops to guide drawing.
**************************************************************/

import javax.swing.JPanel;
import java.awt.*;

public class BullseyePanel extends JPanel
{
    private final int MAX_WIDTH = 300, NUM_RINGS = 5, RING_WIDTH = 25;

    //------------------------------------------------------------
    //  Sets up the bullseye panel.
    //------------------------------------------------------------
    public BullseyePanel ()
    {
        setBackground (Color.cyan);
        setPreferredSize (new Dimension(300,300));
    }

    //------------------------------------------------------------
    //  Paints a bullseye target.
    //------------------------------------------------------------
    public void paintComponent (Graphics page)
    {
        super.paintComponent (page);

        int x = 0, y = 0, diameter = MAX_WIDTH;

        page.setColor (Color.white);

        for (int count = 0; count < NUM_RINGS; count++)
        {
            if (page.getColor() == Color.black)   // alternate colors
                page.setColor (Color.white);
            else
                page.setColor (Color.black);

            page.fillOval (x, y, diameter, diameter);
```

## LISTING 6.6 continued

```
diameter -= (2 * RING_WIDTH);
    x += RING_WIDTH;
    y += RING_WIDTH;
}

// Draw the red bullseye in the center
page.setColor (Color.red);
page.fillOval (x, y, diameter, diameter);
}
```

覆盖较大圆的内部部分，从而产生环形效果。最后，绘制一个红色的圆作为靶心。

让我们再看一个例子。清单 6.7 显示了 Boxes 类，它实例化并显示了清单 6.8 中所示的 BoxesPanel。此程序的目的是在随机位置绘制若干个随机大小的矩形。如果矩形的宽度低于某个厚度阈值（5 像素），则该框用黄色填充。如果高度小于相同的最小厚度，则该框用绿色填充。否则，该框以白色绘制，且不填充。

## LISTING 6.7

```
//****************************************************************
// Boxes.java        Author: Lewis/Loftus
//
// Demonstrates the use of loops to draw.
//****************************************************************

import javax.swing.JFrame;

public class Boxes
{
    //---------------------------------------------------------------
    // Creates the main frame of the program.
    //---------------------------------------------------------------
    public static void main (String[] args)
    {
        JFrame frame = new JFrame ("Boxes");
        frame.setDefaultCloseOperation (JFrame.EXIT_ON_CLOSE);
```

## LISTING 6.7 continued

```
BoxesPanel panel = new BoxesPanel();

frame.getContentPane().add(panel);
frame.pack();
frame.setVisible(true);
}
}
```

### DISPLAY

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_316_0.png)

## LISTING 6.8

```
//***************************************************************************
// BoxesPanel.java Author: Lewis/Loftus
//
// Demonstrates the use of conditionals and loops to guide drawing.
//***************************************************************************

import javax.swing.JPanel;
import java.awt.*;
import java.util.Random;
```

## LISTING 6.8 continued

```
public class BoxesPanel extends JPanel
{
    private final int NUM_BOXES = 50, THICKNESS = 5, MAX_SIDE = 50;
    private final int MAX_X = 350, MAX_Y = 250;
    private Random generator;

    //-------------------------------------------------------------
    // Sets up the drawing panel.
    //-------------------------------------------------------------
    public BoxesPanel ()
    {
        generator = new Random();

        setBackground (Color.black);
        setPreferredSize (new Dimension(400, 300));
    }

    //-------------------------------------------------------------
    // Paints boxes of random width and height in a random location.
    // Narrow or short boxes are highlighted with a fill color.
    //-------------------------------------------------------------
    public void paintComponent(Graphics page)
    {
        super.paintComponent (page);

        int x, y, width, height;

        for (int count = 0; count < NUM_BOXES; count++)
        {
            x = generator.nextInt(MAX_X) + 1;
            y = generator.nextInt(MAX_Y) + 1;

            width = generator.nextInt(MAX_SIDE) + 1;
            height = generator.nextInt(MAX_SIDE) + 1;

            if (width <= THICKNESS) // check for narrow box
            {
                page.setColor (Color.yellow);
                page.fillRect (x, y, width, height);
            }
            else
                if (height <= THICKNESS) // check for short box
                {

```

## LISTING 6.8 continued

```
page.setColor (Color.green);
page.fillRect (x, y, width, height);
}
else
{
page.setColor (Color.white);
page.drawRect (x, y, width, height);
}
}
}
}
```

## 6.6 Dialog Boxes

一个名为对话框的组件有助于辅助 GUI 处理。对话框是一个图形窗口，它会弹出在任何当前活动窗口之上，以便用户可以与其交互。对话框可以用于多种目的，例如传达某些信息、确认操作或允许用户输入某些信息。通常对话框只有一个单一目的，并且用户与之的交互是短暂的。

> KEY CONCEPT
> 对话框是一个弹出窗口，允许简短、特定的用户交互以提供信息或验证操作。

Java 类库的 Swing 包包含一个名为 JOptionPane 的类，它简化了基本对话框的创建和使用。图 6.3 列出了 JOptionPane 的一些方法。

```
static String showInputDialog (Object msg)
Displays a dialog box containing the specified message and an input text field. The contents of the text field are returned.

static int showConfirmDialog (Component parent, Object msg)
Displays a dialog box containing the specified message and Yes/No button options. If the parent component is null, the box is centered on the screen.

static void showMessageDialog (Component parent, Object msg)
Displays a dialog box containing the specified message. If the parent component is null, the box is centered on the screen.
```

FIGURE 6.3 Some methods of the JOptionPane class

JOptionPane 对话框的基本格式分为三类。*消息对话框*仅显示一个输出字符串。*输入对话框*呈现一个提示和一个单一的输入文本字段，用户可以在其中输入一个字符串数据。*确认对话框*向用户提出一个简单的是否问题。

让我们看一个使用这三种类型对话框的程序。清单 6.9 显示了一个程序，它首先向用户呈现一个输入对话框，要求用户输入一个整数。在用户按下输入对话框上的 OK 按钮后，会出现第二个对话框（这次是消息对话框），告知用户输入的数字是偶数还是奇数。在用户关闭该对话框后，会出现第三个对话框，以确定用户是否想测试另一个数字。如果用户按下标记为 Yes 的按钮，对话框系列会重复。否则程序终止。

```java
/*******************************************************/
//  EvenOdd.java        Author: Lewis/Loftus
//
//  Demonstrates the use of the JOptionPane class.
/*******************************************************/

import javax.swing.JOptionPane;

public class EvenOdd
{
   //----------------------------------------------------
   // Determines if the value input by the user is even or odd.
   // Uses multiple dialog boxes for user interaction.
   //----------------------------------------------------
   public static void main (String[] args)
   {
      String numStr, result;
      int num, again;

      do
      {
         numStr = JOptionPane.showInputDialog ("Enter an integer: ");
         num = Integer.parseInt(numStr);

         result = "That number is " + ((num%2 == 0) ? "even" : "odd");

         JOptionPane.showMessageDialog (null, result);
         again = JOptionPane.showConfirmDialog (null, "Do Another?");
      }
      while (again == JOptionPane.YES_OPTION);
   }
}
```

