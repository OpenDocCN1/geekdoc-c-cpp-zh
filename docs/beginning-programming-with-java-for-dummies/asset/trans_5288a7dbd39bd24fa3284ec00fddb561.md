
如果你不相信表2-1（坦白说，你不应该相信书中看到的一切），你可以在自己的计算机上进行测试，以发现Java是否存在，以及（如果你的Mac装有Java）Java的版本号。下面是一个适用于较旧版本Macintosh操作系统的测试：

- 1. 在Spotlight的搜索框中，输入“Java Preferences”。
- 2. 当Spotlight的“Top Hit”是Java Preferences时，按Enter键。

Java Preferences窗口随即出现（参见图2-3）。

![](img/f938eba5f15e231d828a6255e7ec5523_50_0.png)

图2-3：
Java Preferences应用程序。

3. Java Preferences窗口会列出你计算机上安装的Java版本。

如图2-3所示，该计算机有四个Java版本——32位（i386）版本的Java 6和Java 7，以及64位（x86_64）版本的Java 6和Java 7。

对于较新版本的Macintosh操作系统，请尝试以下测试：

- 1. 在Apple菜单中，选择“系统偏好设置”。
- 2. 在“系统偏好设置”应用程序窗口中，查找Java图标（参见图2-4）。
- 3. 点击Java图标。

Java控制面板随即出现（参见图2-5）。

图2-4：
系统偏好设置应用程序中的Java图标。

![](img/f938eba5f15e231d828a6255e7ec5523_51_0.png)

图2-5：
Java控制面板。

![](img/f938eba5f15e231d828a6255e7ec5523_51_1.png)

4. 在Java控制面板中，选择Java标签页（参见图2-6）。

![](img/f938eba5f15e231d828a6255e7ec5523_52_0.png)

图2-6：
Java控制面板中的Java标签页。

5. 在Java标签页中，点击“查看”。

Java运行时环境设置窗口随即出现（参见图2-7）。

![](img/f938eba5f15e231d828a6255e7ec5523_52_1.png)

图2-7：
Java运行时环境设置窗口中的“用户”标签页。

根据Eclipse基金会的网站，*Eclipse*是“一个通用工具平台——一种开放、可扩展的IDE，可用于任何事物，也并非专门针对某一特定事物。”实际上，Eclipse确实用途广泛。程序员通常将Eclipse视为开发Java程序的IDE，但Eclipse还提供了使用C++、PHP和许多其他语言进行编程的工具。我甚至见过与程序开发毫无关系的Eclipse版本。（其中一款产品是*Lively Browser*——一种Web浏览器，其标签页由Eclipse组件构建而成。）

## 下载Eclipse

以下是下载Eclipse的方法：

![](img/f938eba5f15e231d828a6255e7ec5523_54_0.png)

- 1. 访问www.eclipse.org。
- 2. 寻找适合你操作系统的Eclipse下载方式。
  今天，我访问www.eclipse.org，看到一个醒目的按钮，上面写着“Get Started Now... Download Eclipse”（参见图2-8）。明天，谁知道这个不断变化的网站会是什么样子！
  点击“Download Eclipse”按钮后，我会看到针对我计算机操作系统的下载列表（参见图2-9）。
  Eclipse的下载页面会引导你选择特定于你计算机操作系统的Eclipse版本。例如，如果你在Windows计算机上访问该页面，页面只会显示适用于Windows的下载。如果你下载Eclipse是为了在另一台计算机上使用，你可能希望覆盖自动选择的操作系统。查找一个包含你计算机操作系统名称的小型下拉列表。你可以在该下拉列表中更改所选操作系统。
- 3. 从可用包中选择一个Eclipse发行版。
  无论使用何种操作系统，Eclipse都有多种形态、大小和颜色。Eclipse网站提供了Eclipse IDE for Java Developers、Eclipse IDE for Java EE Developers、Eclipse Classic以及许多其他专门下载（参见图2-9）。我通常选择Eclipse IDE for Java Developers，我推荐你也这样做。

图2-8：
eclipse.org的主页。

![](img/f938eba5f15e231d828a6255e7ec5523_54_1.png)

![](img/f938eba5f15e231d828a6255e7ec5523_55_0.png)

图2-9：
Eclipse.org列出了适用于Windows的下载。

4. 在Eclipse的32位和64位版本之间进行选择。

如果你知道自己所装的Java版本是32位还是64位，请务必下载对应的Eclipse版本。如果你不知道自己的Java版本，请下载64位版本的Eclipse并尝试启动它。如果你能启动64位Eclipse，那就没问题。但如果出现“No Java virtual machine was found”（未找到Java虚拟机）错误消息，请尝试下载并启动32位版本的Eclipse。

有关32位和64位字长的完整详细信息，请参阅本章的“你的计算机有多少位？”侧边栏。

5. 按照相关链接开始下载。

你点击的链接取决于Eclipse众多镜像站点中哪个为你的下载提供服务。只需在这些选项中找出可行路径，并开始下载。

## 安装Eclipse

安装Eclipse的具体方式取决于你的操作系统以及下载Eclipse时获得的文件类型。以下是一个简要总结：

- 如果你运行Windows且下载的是.exe文件：
  双击.exe文件的图标。
- 如果你运行Windows且下载的是.zip文件：
  将文件内容解压到你所选的目录。

换句话说，在Windows资源管理器（也称为文件资源管理器）中找到.zip文件的图标，然后双击.zip文件的图标。（结果，资源管理器会显示.zip文件的内容，其中只有一个文件夹——名为eclipse的文件夹。）将eclipse文件夹拖到你计算机硬盘上方便的位置。

有关.zip文件的更多信息，请参阅本章的“压缩归档文件”侧边栏。

我最喜欢将eclipse文件夹直接拖到C:驱动器上。因此，我的C:驱动器上有Program Files、Windows、eclipse等文件夹。我避免将eclipse文件夹作为Program Files的子文件夹，因为有时在处理Program Files名称中的空格时遇到过问题。

### 如果你运行Mac OS X：

下载Eclipse时，你会获得.tar.gz文件或.dmg文件。

- .tar.gz文件是一种压缩归档文件。下载该文件时，你的Web浏览器可能会自动为你进行一些解压缩。如果是这样，你不会在下载文件夹中找到.tar.gz文件。相反，你会找到一个.tar文件（因为你的Web浏览器解压了.gz部分）或一个eclipse文件夹（因为你的Web浏览器同时解压了.tar和.gz部分）。

  如果你在下载文件夹中发现了新的.tar文件或.tar.gz文件，请双击该文件，直到看到eclipse文件夹。将这个新的eclipse文件夹拖到你的应用程序文件夹中，就大功告成了。
- 如果你下载的是.dmg文件，你的Web浏览器可能会为你打开该文件。如果没有，请在下载文件夹中找到.dmg文件并双击。按照双击后出现的任何说明操作。如果需要你将Eclipse拖入应用程序文件夹，请照做。

### 如果你运行Linux：

你可能会获得.tar.gz文件，但也有可能获得自解压的.bin文件。将.tar.gz文件解压到你喜欢的目录，或执行自解压的.bin文件。

## 首次运行Eclipse

你第一次启动Eclipse时，需要执行几个额外的步骤。要让Eclipse运行起来，请执行以下操作：

- 1. 启动Eclipse。

  在Windows中，“开始”菜单可能没有Eclipse图标。在这种情况下，请在Windows资源管理器（又称文件资源管理器）中查找包含你解压后Eclipse文件的文件夹。双击代表eclipse.exe文件的图标。（如果你看到的是eclipse文件而不是eclipse.exe文件，请查阅本章的“那些讨厌的文件扩展名”侧边栏。）

![](img/f938eba5f15e231d828a6255e7ec5523_57_0.png)

在Mac上，前往Spotlight，在搜索框中输入Eclipse。当Eclipse在Spotlight列表中成为“Top Hit”时，按Enter键。

第一次尝试在Mac上运行Eclipse时，你可能会看到一条消息，提示Eclipse不是来自App Store，也不是来自已识别的开发者。这个世界上没有什么是100%安全的，但我下载并安装Eclipse的次数数不胜数，从未遇到过问题。因此，要绕过这个障碍，请在应用程序文件夹（或你安装Eclipse的任何其他位置）中找到Eclipse应用条目。按住Control键点击该应用条目，并在出现的上下文菜单中选择“打开”。此时会出现一个对话框。对话框询问你是否确定要打开该应用程序。你当然确定，因此点击“打开”。

启动Eclipse时，你会看到“Workspace Launcher”对话框（参见图2-10）。该对话框询问你希望在计算机硬盘上的哪个位置存储使用Eclipse创建的代码。

![](img/f938eba5f15e231d828a6255e7ec5523_57_1.png)

图2-10：Eclipse的Workspace Launcher。

- 2. 在“Workspace Launcher”对话框中，点击“确定”接受默认设置（或者不接受默认设置！）。

无论如何，这都不是什么大问题！

因为这是你第一次使用某个特定的Eclipse工作区，Eclipse会以欢迎屏幕开始（参见图2-11）。一直以来，大多数Eclipse欢迎屏幕都显示图标，但几乎没有或没有有用的文本。

- 3. 将鼠标悬停在Eclipse欢迎屏幕的图标上，直到找到一个工具提示中包含“Workbench”字样的图标。

- 4. 点击“Workbench”图标以打开Eclipse的主屏幕。

使用全新工作区打开Eclipse后，主屏幕的视图如图2-12所示。
