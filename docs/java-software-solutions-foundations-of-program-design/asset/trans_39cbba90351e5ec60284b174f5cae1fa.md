

## 第11章 异常
### 清单 11.12

```java
//******************************
// JukeBoxControls.java  Author: Lewis and Loftus
// Represents the control panel for the juke box.
//******************************

import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import java.applet.*;
import java.net.URL;

public class JukeBoxControls extends JPanel
{
    private JComboBox musicCombo;
    private JButton stopButton, playButton;
    private AudioClip[] music;
    private AudioClip current;

    // Sets up the GUI for the juke box.
    public JukeBoxControls()
    {
        URL url1, url2, url3, url4, url5, url6;
        url1 = url2 = url3 = url4 = url5 = url6 = null;

        // Obtain and store the audio clips to play
        try
        {
            url1 = new URL("file", "localhost", "westernBeat.wav");
            url2 = new URL("file", "localhost", "classical.wav");
            url3 = new URL("file", "localhost", "jeopardy.au");
            url4 = new URL("file", "localhost", "newAgeRhythm.wav");
            url5 = new URL("file", "localhost", "eightiesJam.wav");
            url6 = new URL("file", "localhost", "hitchcock.wav");
        }
        catch (Exception exception) {}

        music = new AudioClip[7];
        music[0] = null; // Corresponds to "Make a Selection..."
        music[1] = JApplet.newAudioClip (url1);
        music[2] = JApplet.newAudioClip (url2);
        music[3] = JApplet.newAudioClip (url3);
        music[4] = JApplet.newAudioClip (url4);
        music[5] = JApplet.newAudioClip (url5);
        music[6] = JApplet.newAudioClip (url6);
        JLabel titleLabel = new JLabel ("Java Juke Box");
        titleLabel.setAlignmentX (Component.CENTER_ALIGNMENT);
        // Create the list of strings for the combo box options
        String[] musicNames = {"Make A Selection...", "Western Beat",
        "Classical Melody", "Jeopardy Theme", "Eighties Jam", "Alfred Hitchcock's Theme"};
        musicCombo = new JComboBox (musicNames);
        musicCombo.setAlignmentX (Component.CENTER_ALIGNMENT);
        // Set up the buttons
        playButton = new JButton ("Play", new ImageIcon ("play.gif"));
        playButton.setBackground (Color.white);
        playButton.setMnemonic ('p');
        stopButton = new JButton ("Stop", new ImageIcon ("stop.gif"));
        stopButton.setBackground (Color.white);
        stopButton.setMnemonic ('s');
        JPanel buttons = new JPanel();
        buttons.setLayout (new BoxLayout (buttons, BoxLayout.X_AXIS));
        buttons.add (playButton);
        buttons.add (Box.createRigidArea (new Dimension(5,0)));
        buttons.add (stopButton);
        buttons.setBackground (Color.cyan);
        // Set up this panel
        setPreferredSize (new Dimension (300, 100));
        setBackground (Color.cyan);
        setLayout (new BoxLayout (this, BoxLayout.Y_AXIS));
        add (Box.createRigidArea (new Dimension(0,5)));
        add (titleLabel);
        add (Box.createRigidArea (new Dimension(0,5)));
        add (musicCombo);
        add (Box.createRigidArea (new Dimension(0,5)));
        add (buttons);
        add (Box.createRigidArea (new Dimension(0,5)));
        musicCombo.addActionListener (new ComboListener());
        stopButton.addActionListener (new ButtonListener());
        playButton.addActionListener(new ButtonListener());

        current = null;
    }

    //************************************************************************
    // Represents the action listener for the combo box.
    //************************************************************************
    private class ComboListener implements ActionListener
    {
        //-------------------------------------------------------------
        // Stops playing the current selection (if any) and resets
        // the current selection to the one chosen.
        //-------------------------------------------------------------
        public void actionPerformed(ActionEvent event)
        {
            if (current != null)
                current.stop();

            current = music[musicCombo.getSelectedIndex()];
        }
    }

    //************************************************************************
    // Represents the action listener for both control buttons.
    //************************************************************************
    private class ButtonListener implements ActionListener
    {
        //-------------------------------------------------------------
        // Stops the current selection (if any) in either case. If
        // the play button was pressed, start playing it again.
        //-------------------------------------------------------------
        public void actionPerformed(ActionEvent event)
        {
            if (current != null)
                current.stop();

            if (event.getSource() == playButton)
                if (current != null)
                    current.play();
        }
    }
}
```

显示在组合框中的歌曲列表是在一个字符串数组中定义的。数组的第一个条目默认会出现在组合框中，通常用于指导用户。我们必须确保程序的其余部分不会尝试将该选项用作有效的歌曲。

播放和停止按钮同时显示文本标签和图像图标。它们还被赋予了助记符，以便可以通过键盘部分控制点唱机。

每当用户从中做出选择时，组合框就会生成一个动作事件。JukeBox 程序为组合框使用一个动作监听器类，为两个推送按钮使用另一个动作监听器类。它们本可以合并，使用代码来区分哪个组件触发了事件。

当从组合框中做出选择时，ComboListener 类的 actionPerformed 方法会被执行。如果有正在播放的当前音频选择，则会停止。当前剪辑随后会更新以反映新的选择。请注意，音频剪辑在此时不会立即播放。该程序的设计方式是，用户必须按下播放按钮才能听到新的选择。

当按下任一按钮时，ButtonListener 类的 actionPerformed 方法会被执行。如果有正在播放的当前音频选择，则会停止。如果按下的是停止按钮，任务就完成了。如果按下的是播放按钮，则当前音频选择会从头开始再次播放。

## 自我复习问题 *(见附录 N 中的答案)*

- SR 11.23  什么是组合框？
- SR 11.24  JukeBox 程序如何确保它不会尝试播放与“请选择...”组合框选项关联的歌曲？
- SR 11.25  JukeBox 程序中定义了多少个动作监听器，它们各自监听什么？
- SR 11.26  详细描述 JukeBox 程序如何将用户在组合框中做出的选择与特定的音频剪辑关联起来。

## 11.9 滚动窗格

有时我们需要处理图像或信息太大而无法放入合理区域的情况。在这些情况下，滚动窗格通常很有帮助。滚动窗格是一个容器，它提供对组件的有限视图，并提供垂直或水平滚动条来更改该视图。在任何时候，只能看到底层组件的一部分，但滚动条允许用户导航到组件的任何部分。当 GUI 中的空间有限或正在查看的组件很大或大小会动态变化时，滚动条很有用。

### 关键概念

滚动窗格对于查看大型对象或大量数据很有用。

清单 11.13 中的程序展示了一个包含单个滚动窗格的框架。滚动窗格用于查看费城及其周边地区相当大的地铁地图的图像。该图像被放入一个标签中，然后使用 JScrollPane 构造函数将该标签添加到滚动窗格中。

### 清单 11.13

```
//************************************************************************
//  TransitMap.java        Author: Lewis/Loftus
//
//  Demonstrates the use of a scroll pane.
//************************************************************************

import java.awt.*;
import javax.swing.*;

public class TransitMap
{
    //-------------------------------------------------------------
    //  Presents a frame containing a scroll pane used to view a large
    //  map of the Philadelphia subway system.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        // SEPTA = SouthEast Pennsylvania Transit Authority
        JFrame frame = new JFrame ("SEPTA Transit Map");

        frame.setDefaultCloseOperation (JFrame.EXIT_ON_CLOSE);

        ImageIcon image = new ImageIcon ("septa.jpg");
        JLabel imageLabel = new JLabel (image);

        JScrollPane sp = new JScrollPane (imageLabel);
        sp.setPreferredSize (new Dimension (450, 400));
        frame.getContentPane().add (sp);
        frame.pack();
        frame.setVisible(true);
    }
}
```
