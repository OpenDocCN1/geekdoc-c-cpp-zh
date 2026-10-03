
- 验证你输入的文本已回显到控制台。
- 输入更多文本，再次按回车键。
- 验证该行也回显到了控制台。
- 按 `Ctrl+Z`，然后验证应用程序已结束。

### 任务 4：添加代码格式化数据并显示它

1. 在 `while` 循环体内，在下方代码示例的 `Console.WriteLine` 之前添加所示的加粗语句和注释。

```csharp
static void Main(string[] args)
{
    // 缓冲区用于存储读取的行
    string line;

    // 循环直到没有更多输入（控制台下的 Ctrl+Z 或文件结束）
    while ((line = Console.ReadLine()) != null)
    {
        // 格式化数据
        line = line.Replace(",", " y:");

        // 将结果输出到控制台窗口
        Console.WriteLine(line);
    }
}
```

- 将下方代码示例中所示的加粗语句添加到 `while` 循环体内的代码中。

```cs
static void Main(string[] args)
{
  // 缓冲区，用于存储读取的行
  string line;

  // 循环直到没有更多输入（在控制台中按 Ctrl-Z，或文件末尾）
  while ((line = Console.ReadLine()) != null)
  {
    // 格式化数据
    line = line.Replace(",", "y:");
    line = "x:" + line;

    // 将结果写入控制台
    Console.WriteLine(line);
  }
}
```

此代码通过字符串连接运算符 `+` 在 `line` 变量之前添加前缀 "x:"。`WriteLine` 语句期望 `line` 变量。

生成应用程序：

- 在生成菜单中，点击生成解决方案（Build Solution）。修复任何错误。
- 运行应用程序并验证其运行符合预期。应用程序预期的输入如下代码所示。`235467,25678` 你的代码应将输出格式化为如下代码示例。`x:235467,y:25678`
- 在调试菜单中，点击无调试启动（Start Without Debugging）。
- 在控制台窗口中，输入 `235467,25678` 并按回车。
- 验证 `x:235467,y:25678` 显示在控制台上。
- 包含更多由逗号分隔的数字对，再次按回车。
- 验证数据正确格式化并显示在控制台上。
- 按 `CTRL+Z`。
- 按回车返回 Visual Studio。

# 任务 5：使用文件测试应用程序

1. 执行以下步骤将包含示例数据的 DataFile.txt 文件添加到项目。此文件位于 `E:\Labfiles\Lab 1\Ex1\Starter` 文件夹。这些步骤指定在生成项目时将文件复制到文件夹：

  a. 在解决方案资源管理器中，右键点击 **ConsoleApplication** 项目，点击添加（Add），然后点击现有项（Existing Item）。
  b. 在“添加现有项 - ConsoleApplication”对话框中，转到 `E:\Labfiles\Lab 1\Ex1\Starter` 文件夹，在文件名文本框旁的下拉列表中选择**所有文件 (*.*)**，点击 **DataFile.txt**，然后添加。
  c. 在解决方案资源管理器中，选择 **DataFile.txt**。在属性窗口中，将生成操作（Build Action）属性更改为无（None），然后将输出（Output）属性更改为始终复制（Copy Always）。

2. 重生成应用程序：

- 在生成菜单中，点击重新生成解决方案（Rebuild Solution）。

3. 打开 Visual Studio 命令提示符窗口，转到 `E:\Labfiles\Lab 1\Starter\ConsoleApplication\bin\Debug` 文件夹：

  a. 点击启动（Start），指向所有程序（All Programs），点击 **Microsoft Visual Studio 2010**，点击 Visual Studio 工具（Visual Studio Tools），然后点击 **Visual Studio 命令提示符** (2010)。
  b. 在 Visual Studio 命令提示符 (2010) 窗口中，转到 `E:\Labfiles\Lab 1\Starter\ConsoleApplication\bin\Debug` 文件夹。

4. 运行 **ConsoleApplication** 应用程序并将输入重定向自 **DataFile.txt**。验证生成的输出如下代码：

```
x:238976 y:123218
x:257639 y:119463
x:248293 y:122134
```

在命令提示符窗口中，输入代码示例中的命令：

```
ConsoleApplication < DataFile.txt
```

5. 关闭命令提示符窗口，返回 Visual Studio。

6. 修改项目属性，在使用 Visual Studio 运行项目时重定向输入自 DataFile.txt：

  a. 在解决方案资源管理器中，右键点击 ConsoleApplication 项目，然后点击属性（Properties）。
  b. 在调试（Debug）选项卡中，在命令行（Command line）文本框中输入 DataFile.txt
  c. 在文件菜单中，点击保存。
  d. 关闭 ConsoleApplication 属性。

7. 从 Visual Studio 以调试模式运行应用程序：

- 点击调试（Debug），然后启动调试（Start Debug）。应用程序将运行，但窗口会在生成输出后立即关闭。这是因为 Visual Studio 仅在不调试的情况下运行程序时才会提示用户关闭控制台窗口。当以调试模式运行程序时，Visual Studio 会在程序结束后自动关闭控制台窗口。

8. 在 Main 方法末尾的大括号处设置断点：

- 在 Program.cs 文件中，将光标移动到对应 Main 方法末尾的大括号，右键点击，指向断点（Breakpoint），然后点击插入断点（Insert Breakpoint）。

9. 以调试模式运行应用程序。验证当程序从命令行运行时，输出是相同的：

  a. 点击调试（Debug），然后启动调试（Start Debug）。应用程序将运行，当控制到达 Main 方法末尾且 Visual Studio 焦点时，程序将停止。
  b. 在任务栏中，点击 ConsoleApplication.exe 的图标。
  c. 验证 ConsoleApplication.exe 窗口中显示的输出与之前相同。
  d. 返回 Visual Studio，然后在调试菜单中点击继续（Continue）。应用程序将完成。

## 练习 2：构建 WPF 应用程序

## 任务 1：创建一个新的 WPF 项目

使用 Windows Presentation Foundation (WPF) 应用程序模板在 `E:\Labfiles\Lab 1\Ex2\Starter` 文件夹中创建一个名为 WPFApplication 的新项目：

- 在 Visual Studio 中，在文件（File）菜单中，指向新建（New），然后点击项目（Project）。
- 在“新建项目”对话框中，在项目窗格中，展开 C#，然后点击 Windows。
- 在模板窗格中，点击 WPF 。
- 在对话框中指定以下值，然后点击：
  - 名称：WPFApplication
  - 位置：`E:\Labfiles\Lab 1\Ex2\Starter`
  - 项目：WPFApplication

### 任务 2：创建用户界面

将 TextBox、Button 和 TextBlock 控件添加到 MainWindow 窗口：

- 点击工具箱（Toolbox）选项卡。
- 如果尚未打开，展开常用控件（Common Controls）部分。
- 将 TextBox 控件拖到 MainWindow 窗口。
- 将 Button 控件拖到 MainWindow 窗口。
- 点击工具箱。
- 将 TextBlock 控件拖到 MainWindow 窗口。

2. 使用属性窗口根据下表设置控件的属性。其他属性保持默认值。

| 控件 | 属性 | 值 |
| :--- | :--- | :--- |
| TextBox | Name | test |
| | Height | 28 |
| | HorizontalAlignment | Left |
| | Margin | 12,12,0 |
| | VerticalAlignment | Top |
| | Width | 302 |
| Button | Name | testButton |
| | Content | Format Data |
| | Height | 23 |
| | HorizontalAlignment | Left |
| | Margin | 320,17,0 |
| | VerticalAlignment | Top |
| | Width | 80 |
| TextBlock | Name | formattedText |
| | Height | 238 |
| | HorizontalAlignment | Left |
| | Margin | 14,50,0 |
| | VerticalAlignment | Top |
| | Width | 384 |

a. 在 MainWindow 窗口中点击 TextBox 控件。
b. 在属性窗口中，点击 TextBox 旁的文本，然后将其更改为 testInput。
c. 在属性列表中找到 Height 属性，然后将其更改为 28。
d. 对 TextBox 控件的其余属性重复此过程。
e. 在 MainWindow 窗口中点击 Button 控件。
f. 按照 b 到 e 步骤描述的操作设置此控件的指定属性。
g. 在 MainWindow 窗口中点击 TextBlock 控件。
h. 按照 b 到 e 步骤描述的操作设置此控件的指定属性。

MainWindow 窗口应该如截图所示。

![](img/3ef84844c6ac82b838fffa6448b2346_481_0.png)

# 任务 3：添加格式化用户输入代码

1. 为按钮的 Click 事件创建事件处理程序：

  a. 在 MainWindow 窗口中点击 Button 控件。
  b. 在属性窗口中，点击事件（Events）选项卡。
  c. 在事件列表中，双击 Click。

2. 将下方代码示例中加粗的代码添加到事件处理方法中。

```cs
private void button_Click(object sender, RoutedEventArgs e)
{
    // 将 TextBox 的内容复制到字符串
    string line = testInput.Text;

    // 格式化字符串数据
    line = line.Replace(",", " y:");
    line = "x:" + line;

    // 将结果存储在 TextBlock 中
    formattedText.Text = line;
}
```

此代码读取 TextBox 的内容到名为 `line` 的字符串变量，并以练习 1 中控制应用程序相同的方式格式化该字符串，并将格式化后的结果显示在 TextBlock 控件中。注意可以使用 `Text` 属性访问 TextBox 控件和 TextBlock 控件的内容。

# 任务 4：修改应用程序以从文件读取数据

- 1. 为 Window_Loaded 事件创建一个事件处理程序。该事件在窗口即将显示时、应用程序启动后发生：

   a. 显示 MainWindow.xml 文件。
   b. 点击 MainWindow 窗口的标题栏。
   c. 在属性（Properties）窗口中，点击事件（Events）选项卡。
   d. 在事件列表中，双击 Loaded 事件。

2. 在事件方法中，添加下方代码示例中**粗**显示的代码。

```cs
private void Window_Loaded(object sender, RoutedEventArgs e)
{
    // 用于存储从标准输入行读取的一行缓冲区；
    string line;

    // 循环直到文件结束
    while ((line = Console.ReadLine()) != null)
    {
        // 格式化缓冲区中的数据
        line = line.Replace(",", " ");
        line = "x:" + line + "\n";
        // 将结果放入 TextBlock 中
        formattedText.Text += line;
    }
}
```

此代码从标准输入读取文本，按与练习 1 相同的方式进行格式化，然后将结果追加到 TextBlock 控件的末尾。它会继续从标准输入读取所有文本直到检测到结束。

注意使用 `+=` 运算符将数据添加到 TextBlock 控件的 `Text` 属性，你可以添加换行符（`\n`）行进行格式化输出，以确保每个项目在 TextBlock 控件中显示在新的一行。

- 3. 执行以下步骤修改项目设置，将标准输入重定向到 DataFile.txt 文件。该文件的副本存在于 `E:\Labfiles\Lab1\Ex2\Starter` 文件夹中：

   a. 在解决方案管理器（Solution Explorer）中，右键点击 WPFApplication 项目，指向添加（Add），然后点击现有项（Existing Item）。

## 实验 1：介绍 C# 和 .NET 框架

- b. 在“添加现有项 - WPFApplication”对话框中，转到 `E:\Labfiles\Lab1\Ex2\Starter` 文件夹，在文件名文本框旁边的下拉列表中选择所有文件（** Files），点击 DataFile.txt，然后点击添加。
- c. 在解决方案管理器中，选择 DataFile.txt。在属性窗口中，将生成操作（Build action）属性更改为无（None），然后将复制到输出（Copy to Output）属性更改为始终复制（Copy Always）。
- d. 在解决方案管理器中，右键点击 WPFApplication 项目，然后点击属性。
- e. 在调试（Debug）选项卡上，在命令行参数（Command line arguments）文本框中输入 DataFile.txt
- f. 在文件菜单上，点击全部保存。
- g. 关闭 WPFApplication 窗口。

- 4. 在调试模式下生成并运行应用程序。验证当应用程序启动时，它从 DataFile.txt 读取数据，并在 TextBlock 控件中显示下方代码示例中的结果。

   * 在调试菜单上，点击启动调试（Start Debugging）

- 5. 关闭 MainWindow 窗口，返回 Visual Studio。

# 练习 3：验证应用程序

任务 1：修改 DataFile.txt 文件中的数据

- 按照下方代码示例所示修改 DataFile.txt 文件的内容。

```
1.2543,0.342
3255.7639,99811.9463
24.8293,12.2135
23.8976,12.3218
25.7639,11.9463
24.8293,12.2135
```

- a. 在解决方案管理器中，双击 DataFile.txt。

# L1-14 介绍 C# 和 .NET 框架

- b. 编辑文件中的数据，使其类似于所示数据。
c. 在文件菜单上，点击全部保存。
d. 关闭 DataFile.txt 窗口。

**注意：** DataFile.txt 末尾必须有一个空行。

## 任务 2：使用 Visual Studio 2010 逐步执行应用程序

- 1. 在 Window_Loaded 事件处设置断点：

   a. 显示 MainWindow.xaml.cs 文件。
   b. 滚动到 Window_Loaded 事件。
   c. 右键点击下方代码语句，指向断点，然后点击插入断点。

```cs
private void Window_Loaded(object sender, RoutedEventArgs e)
```

- 2. 以调试模式启动应用程序：

   - 在调试菜单上，点击启动调试

   当应用程序运行 Window_Loaded 事件时，它会到达断点并进入 Visual Studio。方法的开头被高亮。

- 3. 进入 Window_Loaded 方法中包含执行代码的第一条语句：

   - 在调试菜单上，点击逐语句进入（Step Into），或按 F11。

`while` 语句被高亮。这是因为声明 `line` 变量的语句不包含任何执行代码。

- 4. 检查 `line` 变量的值。尚未赋值：

   - 在本地（Locals）窗口中，验证 `line` 的值为 `null`。

- 5. 进入下一个语句：

   - 在调试菜单上，点击逐语句进入（Step Into），或按 F11。

   * 光标移动到 `while` 循环体的大括号。

6. 检查 `line` 变量的值。应该是 `1.2543,0.342`。这是来自 DataFile.txt 第一行的文本。`while` 语句中的 `Console.ReadLine` 语句从文件中读取此内容：

   * 在本地窗口中，验证 `line` 的值为 `1.2543,0.342`。

- 7. 进入下一个语句：

   * 在调试菜单上，点击逐语句进入（Step Into），或按 F11。

   光标移动到下方代码行：

```
line = line.Replace(",", " y:");
```

8. 进入下一个语句：
