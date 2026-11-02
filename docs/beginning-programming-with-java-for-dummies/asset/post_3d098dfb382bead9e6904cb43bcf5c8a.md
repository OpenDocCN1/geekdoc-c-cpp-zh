
## 研究生学位论文答辩
## 基于深度学习的污水处理过程软测量建模方法研究
答辩人：李伟
指导教师：张敏教授
答辩时间：2024年5月20日
答辩地点：环境工程学院 301 会议室
## 汇报提纲
- 1. 研究背景与意义
- 2. 国内外研究现状
- 3. 主要研究内容与方法
- 4. 实验设计与结果分析
- 5. 结论与展望

![](img/f938eba5f15e231d828a6255e7ec5523_415_0.png)

> Calling `setVisible(true)` makes the frame appear on your screen. If you forget to call `setVisible(true)` (and I often do), when you run the code in Listing 20-1, you'll see nothing on your screen. It's always so disconcerting until you figure out what you did wrong.

## Constructor Calls
In Listing 17-3 (in Chapter 17), I created an instance of the Purchase class with the line

```
Purchase onePurchase = new Purchase();
```

The code in Listing 20-1 does the same kind of thing. In Listing 20-1, I create an instance of the JFrame class with the following line:

```
JFrame frame = new JFrame();
```

Compare Figure 17-4 in Chapter 17 with this chapter's Figure 20-4.

![](img/f938eba5f15e231d828a6255e7ec5523_415_1.png)

When you type `MyFrame extends JFrame`, you declare that your new `MyFrame` class has all the methods and other things that are built into Java’s own `JFrame` class, and possibly more. For example, a `JFrame` instance has `setDefaultCloseOperation`, `pack`, and `setVisible` methods, so every new `MyFrame` instance has `setDefaultCloseOperation`, `pack`, and `setVisible` methods (see Figure 20-6).

![](img/f938eba5f15e231d828a6255e7ec5523_419_0.png)

**Figure 20-6:** A `MyFrame` instance has many methods.

When you put the words `extends JFrame` in your code, you get all of the `JFrame` methods for free. The `MyFrame` class’s code doesn’t need declarations for methods, such as `setDefaultCloseOperation`, `pack`, and `setVisible`. Those declarations are already in the `JFrame` class in Java’s API. The only declarations in the `MyFrame` class’s code are for brand-new things — things that are specific to your newly declared `MyFrame` class. It’s as though Listing 20-2 contained the following information:

```java
public class MyFrame is a kind of JFrame {

    And in addition what's in JFrame, MyFrame also has
    a brand new constructor:
    public MyFrame() {
        // Etc.
    }
}
```

On a Mac, you get a .dmg file. Depending on your Mac web browser’s settings, the browser may or may not expand the .dmg file automatically. If not, double-click the .dmg file to begin the installation.

- 5. **Follow the installation routine’s instructions.**

On a Windows computer, you accept a bunch of defaults.

On a Mac, you drag the Scene Builder’s icon to the Applications folder.

That’s it! You’ve installed Scene Builder.

## Installing e(fx)clipse
Eclipse has its own elaborate facility for incorporating new functionality. An Eclipse tool is called an *Eclipse plug-in*. When you first install Eclipse, you get many plug-ins by default. Then, to enhance Eclipse’s power, you can install many additional plug-ins.

Eclipse’s e(fx)clipse plug-in facilitates the creation of JavaFX applications. You can add the plug-in to your existing installation of Eclipse, but it’s much simpler to download a new copy of Eclipse (a copy with e(fx)clipse already installed). Here’s how you get the new copy of Eclipse:

- 1. Visit `efxclipse.bestsolution.at`.
- 2. Look for the page containing All-in-One downloads.
- 3. On the All-in-One downloads page, look for a way to download a copy of Eclipse for your operating system.

Your Eclipse download’s word length (32-bit or 64-bit) must match your Java version’s word length. For the full lowdown on 32-bit and 64-bit word lengths, see Chapter 2.

- 4. **Follow the appropriate links or click the appropriate buttons to begin the download.**
- 5. **Follow the instructions in Chapter 2 to install this new copy of Eclipse on your computer.**

![](img/f938eba5f15e231d828a6255e7ec5523_424_0.png)

Place the new copy of Eclipse in a brand-new folder. That way, you don’t have to uninstall your old copy of Eclipse (in fact, it’s helpful to have two separate Eclipse installations on your computer.) On my Windows computer, I have a `c:\eclipse` folder and a `c:\eclipsefx` folder. Both folders have their own subfolders with names like `configuration`, `features`, and `plugins`. Both folders have their own eclipse.exe file. Similarly, my Mac has both eclipse and the e(fx)clipse folders inside the Applications folder.

![](img/f938eba5f15e231d828a6255e7ec5523_425_0.png)

When you open any copy of `eclipse`, the program prompts you for a place on your hard drive for the Eclipse workspace (your collection of Eclipse projects). At this point, you have a choice:

- **You can have two different folders for two different workspaces — one workspace for your original copy of Eclipse, and a second workspace for your new copy of Eclipse.**

Doing so keeps your original work (for preceding chapters) separate from this chapter’s work. Also, with two different workspaces, you can run both copies of Eclipse simultaneously.

- **Alternatively, you can point both versions of Eclipse to the same folder (and thus, to the same workspace).**

Doing so keeps all your work in one place. You don’t have to change workspaces in order to change from your original work to this chapter’s work. On the minus side, you can’t run two copies of Eclipse using the same workspace simultaneously.

![](img/f938eba5f15e231d828a6255e7ec5523_425_1.png)

Don’t fret over the decision you make about Eclipse workspaces. In any copy of Eclipse, you can switch from one workspace to another. You can decide on a particular workspace whenever you launch Eclipse. You can also move from one workspace to another by selecting File>Switch Workspace in Eclipse’s main menu.

![](img/f938eba5f15e231d828a6255e7ec5523_425_2.png)

You need at least JDK 7u7 in order to run `e(fx)clipse`.

## Creating a bare-bones JavaFX project
There’s a wise old saying, “A picture is worth 50 words.” And if you count things like `javafx.application.Application` objects, the association as three separate words, the same picture is worth 70 words. In this section, you create a picture from which Eclipse builds a 70-word Java program.

- 1. **Follow the instructions in the previous sections (the “Installing Scene Builder” and “Installing e(fx)clipse” sections).**
- 2. **Launch your new copy of Eclipse and click the Welcome screen’s Workbench icon.**
- 3. **From Eclipse’s menu bar, choose File>New>Project.**
  The New Project dialog box appears.
- 4. **In the dialog box’s list, expand the JavaFX branch. Within that branch, select JavaFX project and then click Next.**
  A New Java Project dialog box appears.

- 5. In the New Java Project dialog box, type a name for your project.

If you're following my instructions to the letter, name the project MyFirstJavaFXProject.

- 6. In the New Java Project dialog box, select JavaSE-1.7 or JavaSE-1.8.

You can run JavaFX programs with earlier versions of Java, but life is easier with Java 7 update 7 (JDK 7u7), or later.

- 7. Click Finish to close the New Java Project dialog box.

After clicking Finish, you may or may not see a dialog box warning you that Mercurial (whatever that is) is not configured correctly. If you see this dialog box, look for the box's Restore Defaults button. Click that button and then click OK.

You see the Eclipse workbench with your newly created project in Eclipse's Package Explorer.

![](img/f938eba5f15e231d828a6255e7ec5523_426_0.png)

## Running your bare-bones JavaFX project
In the previous section, you use e(fx)clipse to create a brand-new JavaFX project. When you run the new project's code, you see the stuff in Figure 20-8. You see a window with nothing inside it.

![](img/f938eba5f15e231d828a6255e7ec5523_426_1.png)

Figure 20-8:
An empty window.
