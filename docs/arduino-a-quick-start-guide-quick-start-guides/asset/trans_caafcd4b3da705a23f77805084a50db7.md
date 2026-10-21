

选择错误的串口或 Arduino 类型也是常见的错误。如果在上传草图时收到诸如“Serial port already in use”的错误消息，请检查是否已从 Tools > Serial Port 菜单中选择了正确的串口。如果收到诸如“Problem uploading to board”或“programmer is not responding”的消息，请检查是否已从 Tools > Board 菜单中选择了正确的 Arduino 板。

你的 Arduino 程序与所有程序一样，会包含错误。拼写错误和语法错误会被编译器检测到。在下一页的图 1.13 中，你可以看到一个典型的错误消息。我们本应调用 pinMode()，却调用了 pinMod()，由于编译器找不到该名称的函数，它便停止并显示错误消息。Arduino IDE 会高亮显示该行，用黄色背景标出错误，并打印出有用的错误消息。

其他错误可能更微妙，有时你需要仔细研究代码并使用一些老式的调试技术（在 Debug It! Find, Repair, and Prevent Bugs in Your Code [But09] 中你可以找到大量关于此主题的有用建议）。

虽然很少见，但也可能发生 LED 损坏的情况。如果上述技巧都不起作用，请尝试更换另一个 LED。

## 1.9 Exercises

- 尝试使用更多暂停并改变暂停长度来制作不同的闪烁模式（它们不一定都要相同）。另外，尝试使用非常短的暂停使 LED 以高频率闪烁。你能解释你观察到的效果吗？
- 让 LED 用摩尔斯电码输出你的名字。¹⁴

## 2.2 Managing Projects and Sketches

现代软件开发者可以从各种自动化重复和枯燥任务的开发工具中进行选择。对于 Arduino 这样的嵌入式系统也同样如此。你也可以使用集成开发环境（IDEs）来管理你的程序。其中最受欢迎的一个是由 Arduino 团队创建的。

Arduino IDE 管理项目所属的所有文件。它还为你创建将在 Arduino 板上运行的二进制文件所需的所有工具提供了便捷的访问。方便的是，它做得毫不显眼。例如，你可能已经注意到 Arduino IDE 会自动保存你输入的所有代码。这是为了防止初学者意外丢失数据或代码（更不用说即使是专业人士也会时不时丢失数据）。

自动组织项目所属的所有文件是 IDE 最重要的功能之一。在幕后，Arduino IDE 为每个新项目创建一个目录，并将项目所属的所有文件存储在此目录中。要向项目添加新文件，请点击右侧的标签按钮打开标签弹出菜单，然后选择 New Tab（见图 2.1）。要添加现有文件，请使用 Sketch > Add File 菜单项。

从菜单项的名称你可能已经猜到了，Arduino IDE 将项目称为草图。如果你没有选择名称，它会以 sketch_ 开头命名。你可以使用 Save As 命令随时更改名称。如果你没有显式保存草图，IDE 会将其存储在预定义的文件夹中，你可以在首选项菜单中查看

![](img/dcfd13a1bf99c4d3f9996627012a6526_46_0.png)

Figure 2.1: The tabs menu in action

该位置。你可以更改此行为，以便在创建新草图时 IDE 询问你名称。每当你迷路时，你可以使用 Sketch > Show Sketch Folder 菜单项检查当前草图位于哪个文件夹。

IDE 使用目录不仅用于组织项目。它还在以下文件夹中存储一些有趣的内容：

- examples 文件夹包含可作为你自己实验基础的示例草图。可通过 File > Open 对话框访问它们。花点时间浏览它们，即使你现在看不懂任何内容。
- libraries 目录包含用于各种目的和设备的库。每当你使用新传感器时，很可能需要将支持库复制到此文件夹。

Arduino IDE 通过为大量设置选择合理的默认值来让你的生活更轻松。但它也允许你更改其中大多数设置，你将在下一节中看到如何操作。

## 2.3 Changing Preferences

对于早期项目，IDE 的默认值可能合适，但迟早你会想更改一些内容。如图 2.2 所示，在下一页中，IDE 只允许你直接更改少数首选项。但对话框中提到了一个名为 preferences.txt 的文件，其中包含更多首选项。该文件是一个 Java 属性文件，由键/值对组成。这里显示了其中一些：

```
...
editor.external.bgcolor=#168299
preproc.web_colors=true
editor.font.macosx=Monaco,plain,10
sketchbook.auto_clean=true
update.check=true
build.verbose=true
upload.verbose=true
...
```

这些属性中的大多数控制用户界面；也就是说，它们更改字体、颜色等。但它们也可以更改应用程序的行为。例如，你可以为编译或上传草图等操作启用更详细的输出。编辑 preferences.txt，并将 build.verbose 和 upload.verbose 都设置为 true。然后从第 1 章 Welcome to the Arduino，第 23 页加载闪烁 LED 草图并

![](img/dcfd13a1bf99c4d3f9996627012a6526_48_0.png)

# Figure 2.2: The IDE lets you change some preferences.

再次编译它。消息面板中的输出应类似于下一页的图 2.3（在 IDE 的最新版本中，你可以通过在工具栏中点击 Verify/Compile 或 Upload 按钮时按住 Shift 键来实现相同效果）。

请注意，IDE 在关闭时会更新部分首选项的值。因此，在直接在 preferences.txt 文件中更改任何首选项之前，你必须先停止 Arduino IDE。

现在你已经熟悉 Arduino IDE，让我们做一些编程。我们将让 Arduino 与外部世界对话。

Arduino 使许多独立应用成为可能——这些项目不涉及任何额外的计算机。在这种情况下，你只需连接一次 Arduino 到计算机以上传软件，之后它只需要电源即可。更常见的是，人们使用 Arduino 通过传感器增强计算机的功能或提供对额外硬件的访问。通常，你通过串口控制外部硬件，因此学习如何与 Arduino 串行通信是个好主意。

![](img/dcfd13a1bf99c4d3f9996627012a6526_49_0.png)

Figure 2.3: IDE in verbose mode showing output of command-line tools

用于上传软件的 Arduino 具有串口，我们也可以用它将 Arduino 连接到其他设备（在第 1.6 节 Compiling and Uploading Programs，第 38 页，你将学习如何查找 Arduino 连接的串口）。在本节中，我们将使用它通过计算机键盘控制 Arduino 的状态 LED。LED 应在你按下 1 时打开，按下 2 时关闭。我们需要的所有代码如下：

```
Download welcome/LedSwitch/LedSwitch.pde
const unsigned int LED_PIN = 13;
const unsigned int BAUD_RATE = 9600;

void setup() {
  pinMode(LED_PIN, OUTPUT);
  Serial.begin(BAUD_RATE);
}

void loop() {
  if (Serial.available() > 0) {
    int command = Serial.read();
    if (command == '1') {
      digitalWrite(LED_PIN, HIGH);
      Serial.println("LED on");
    } else if (command == '2') {
      digitalWrite(LED_PIN, LOW);
      Serial.println("LED off");
    } else {
      Serial.print("Unknown command: ");
      Serial.println(command);
    }
  }
}
```

与之前的示例一样，我们为 LED 连接的引脚定义了一个常量，并在 setup() 函数中将其设置为 OUTPUT 模式。在第 6 行，我们使用 Serial 类的 begin() 函数初始化串口，传入波特率 9600（你可以在第 C.1 节 Learning More About Serial Communication，第 251 页了解波特率是什么）。这就是在程序中发送和接收串口数据的全部内容。

那么，让我们读取并解释数据。loop() 函数首先在第 10 行调用 Serial 的 available() 方法。available() 返回串口上等待的字节数。如果有数据可用，我们使用 Serial.read() 读取它。read() 如果有数据可用则返回第一个字节的传入数据，否则返回 -1。

