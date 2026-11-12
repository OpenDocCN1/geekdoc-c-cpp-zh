

当您启动重建时，可能会提示保存项目。只需在项目名称末尾添加“_X86”并保存。项目将在64位环境下构建，并链接正确的库文件。

您也可能会遇到缺少库的问题，例如“cutil32.lib”。安装SDK时，它会设置一个环境变量$(CUDA_LIB_PATH)。这通常设置为：C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v4.0\lib\Win32。

您可能会发现默认项目文件中的路径设置没有将$(CUDA_LIB_PATH)作为条目之一。要添加它，请单击项目，然后选择“项目 -> 属性”。这将打开图4.3所示的对话框。

单击最右侧的“...”按钮将打开一个对话框，您可以在其中添加库路径（图4.4）。只需将“$(CUDA_LIB_PATH)”作为新行添加，项目现在应该可以链接了。

如果您希望同时构建64位CUDA应用程序和32位CUDA应用程序，则需要安装32位和64位CUDA工具包。SDK中的示例也需要安装32位和64位版本的SDK，才能构建32位和64位版本的示例。

您可以通过进入以下目录并构建解决方案文件来构建所需的库：

C:\ProgramData\NVIDIA Corporation\NVIDIA GPU Computing SDK 4.1\Common
C:\ProgramData\NVIDIA Corporation\NVIDIA GPU Computing SDK 4.1\shared

![](img/e0b192dbaf05f61ad420bee512a8c4e4_70_0.png)

图4.3 其他库路径。

![](img/e0b192dbaf05f61ad420bee512a8c4e4_71_0.png)

图4.4 添加库目录。

您将在 C:\ProgramData\NVIDIA Corporation\NVIDIA GPU Computing SDK 4.1\C\common\lib\x64 中找到所需的库。

您也可以手动将这些库添加到缺少它们的任何项目中。不幸的是，SDK示例未设置为在需要时自动构建所需的库。库的二进制文件也未提供，这使得实际构建SDK示例有点令人沮丧。

## 创建项目

要创建新的CUDA支持应用程序，只需使用“文件 -> 新建 -> 项目向导”创建CUDA应用程序，如图4.5所示。向导将创建一个包含文件“kernel.cu”的单个项目，该文件包含混合代码，部分代码在CPU上执行，部分代码在GPU上执行。GPU代码包含在函数addKernel中。该函数只需获取指向目标数组c的指针以及指向两个输入数组a和b的几个指针。然后它将a和b数组的内容相加，并将结果存储在目标数组c中。这是执行CUDA程序所需框架的一个非常简单的示例。

还包括将数据复制到设备、调用内核以及将数据从设备复制回主机的基本代码。这是一个非常有用的入门项目，可让您在CUDA下编译一些内容。我们将在后文中介绍使CUDA程序运行所需的标准框架。如果可能，查看代码并尝试理解它很有用。但是，如果此时还不明白，请不要担心，我们将逐步介绍如何为CUDA编写程序。

![](img/e0b192dbaf05f61ad420bee512a8c4e4_72_0.png)

图4.5 CUDA项目向导。

## Linux

CUDA支持以下Linux发行版。支持的版本将取决于您安装的CUDA工具包版本。

- Fedora 14
- Redhat 6.0 和 5.5 / CentOS 6.2（Redhat的免费版本）
- Ubuntu 11.04
- OpenSUSE 11.2

在Linux平台上安装CUDA的第一步是确保您拥有最新的内核软件。请从终端窗口使用以下命令：

```
sudo yum update
```

sudo命令将以管理员身份登录。yum命令是Linux RPM包的标准安装工具。您只是要求它检查所有已安装的包，并查看是否有可用的更新。这确保在安装任何驱动程序之前，您的系统已完全更新。许多基于GUI的安装也具有替代旧命令行更新界面的基于GUI的软件更新版本。

内核更新到最新级别后，请运行以下命令：

```
sudo yum install gcc-c++ kernel-devel
```

这将安装标准的GNU C++环境以及重建内核所需的内核源代码。请注意，包名区分大小写。这将提示您下载大约21 MB，安装需要几分钟。同样，如果您愿意，可以通过特定操作系统的GUI软件安装程序安装该包。

最后，由于您可能需要绘制一些图形输出，您需要一个OpenGL开发环境。请使用以下命令安装：

```
sudo yum install freeglut-devel libXi-devel libXmu-devel
```

现在您已准备好安装CUDA驱动程序。请确保安装至少4.1版本的CUDA工具包。有多种方法可以安装更新的NVIDIA驱动程序。NVIDIA不发布驱动程序的源代码，因此默认情况下大多数Linux发行版安装一个非常基本的图形驱动程序。

## 内核基础驱动程序安装（CentOS，Ubuntu 10.4）

CUDA版本应与特定的一组开发驱动程序配合使用。使用此处列出的方法以外的方法安装驱动程序可能会导致CUDA无法工作。请注意给定CUDA工具包版本支持的操作系统版本。这些可能不是特定Linux发行版的最新版本。使用较新的发行版可能无法工作。因此，第一个安装步骤是使用特定Linux发行版指定的版本替换任何现有驱动程序。请参见图4.6。

下载完成后，您需要以纯文本模式启动Linux。与始终处于图形模式的Windows不同，在Linux下安装驱动程序需要文本模式。您可以在大多数发行版上使用以下命令从终端窗口（通常位于GUI的系统菜单下）使系统以文本模式启动：

```
sudo init 3
```

这将重新启动Linux计算机并以文本模式重新启动。您可以稍后使用sudo init 5恢复图形模式。

如果出现诸如“用户<user_name>不在sudoers文件中”之类的错误，请使用su命令以root身份登录。编辑“/etc/sudoers”文件并追加以下行：

```
your_user_name ALL=(ALL) ALL
```

请务必将your_user_name替换为您的登录名。

某些发行版（例如Ubuntu）坚持启动到GUI，无论init模式如何。一种解决方法如下，从文本窗口开始。编辑grub启动文件：

```
sudo chmod +w /etc/default/grub
sudo nano /etc/default/grub
```

更改以下行：

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
GRUB_CMDLINE_LINUX_DEFAULT=""
```

改为

```
# GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
GRUB_CMDLINE_LINUX_DEFAULT="text"
```

## CUDA下载

## CUDA工具包4.2

当前生产版本

![](img/e0b192dbaf05f61ad420bee512a8c4e4_74_0.png)

![](img/e0b192dbaf05f61ad420bee512a8c4e4_74_1.png)

图4.6 截至2012年9月支持的Linux下载和支持的驱动程序版本。

现在使用以下命令更新grub：

```
sudo update-grub
```

最后，重新启动计算机，它应该以纯文本模式启动。安装驱动程序后，使用原始行再次启动到GUI。

现在导航到您从NVIDIA网站下载的“.run”文件所存储的位置。

然后键入

```
sudo sh NVIDIA-Linux-x86_64-285.05.33.run
```

您下载的驱动程序的具体版本当然会有所不同。系统会要求您同意NVIDIA许可证，然后需要等待几分钟，直到所有内容安装完毕。在此过程中，安装程序将尝试用必要的NVIDIA驱动程序替换默认的Nouveau驱动程序。如果询问您是否要执行此操作，请选择“是”。这是一个容易出错的过程，并非每个发行版都开箱即用。如果NVIDIA安装程序无法删除Nouveau驱动程序，则可能需要将该驱动程序列入黑名单，以便NVIDIA安装程序可以安装正确的驱动程序。

当您正确安装NVIDIA驱动程序后，请键入

```
sudo init 5
```

计算机将随后重新启动到常规图形模式。有关Ubuntu，请参见前文。

下一项任务是安装工具包。有多种可用——根据您的发行版选择Fedora、Red Hat、Ubuntu、OpenSUSE或SUSE。与之前一样，只需导航到安装SDK的位置，并通过键入以下命令运行它：

```
sudo sh <sdk_version>.run
```

其中<sdk_version>是您下载的文件。它将安装所有所需的工具并打印一条消息，指示安装成功。然后它提到您需要手动更新PATH和LD_LIBRARY_PATH环境变量。为此，您需要编辑“/etc/profile”启动文件。添加以下行：

```
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```

请注意，该文件必须可写。如果需要，请使用“sudo chmod +w /etc/profile”使其可写。您可以使用喜欢的编辑器编辑此文件，例如使用命令“sudo nano /etc/profile”。

现在注销并重新登录，然后键入

```
env
```

这将列出所有当前的环境变量设置。检查您刚刚修改的两个新条目。CUDA现在已安装到“/usr/local/bin”目录。

接下来我们需要GNU C++编译器。从系统上使用的任何软件安装程序安装“g++”包。

下一步是安装SDK示例代码，以便我们有东西可以构建和测试。从NVIDIA网站下载这些代码，并再次使用`sh sdk_version.run`命令运行它们（将`sdk_version`替换为您实际下载的版本）。不要以root身份运行此安装，否则您将需要以root身份登录才能构建任何示例。

默认情况下，SDK将安装到用户帐户区域的子目录中。它可能会抱怨找不到CUDA安装，并将使用默认目录（即之前安装CUDA的同一目录）。您可以安全地忽略此消息。

安装GPU计算SDK后，您需要进入“Common”子目录并运行`make`来创建一组库。

完成此操作后，SDK示例应该可以构建，从而允许您在Linux上执行第一个CUDA程序，并当然可以查看驱动程序是否正常工作。

