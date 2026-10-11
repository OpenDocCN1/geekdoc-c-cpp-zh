
![](img/5e76fd429fabd2b62e16a7bfd8cf546f_477_1.png)

输入你想要编译的程序。输入以下加法程序：

```C
#include <p18f4321.h>
void main (void)
{
    int a = 5;
    int b = 1;
    int c;
    c = a + b;
    while(1);
}
```

输入程序后，查看以下界面：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_478_0.png)

接下来，点击 `File`，然后选择 `Save as` 以查看以下屏幕截图：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_479_0.png)

确保你向上滚动到桌面，然后点击 `plus`（之前创建的文件夹），查看以下界面：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_479_1.png)

接下来，双击（左击）`plus` 以查看以下界面：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_480_0.png)

删除 `Untitled`，输入与之前相同的文件名 `addition` 作为文件名，扩展名为 `.c`。点击 `保存`，查看以下屏幕截图（注意显示颜色的变化）：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_481_0.png)

接下来，通过点击 `addition.mcw` 顶部的蓝色区域进行高亮选择，查看以下界面：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_481_1.png)

右键点击 `Source Files` 以查看以下界面：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_482_0.png)

左击 `Add files` 以查看以下界面：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_483_0.png)

在窗口中左击一次 `addition.c` 以查看以下界面：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_484_0.png)

点击 `打开` 以查看以下界面：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_484_1.png)

接下来，执行以下操作：

- 点击 `Project`，点击 `Build options` 然后点击 `project`
- 在 `output directory` 中向下滚动到 `Linker.Script Search Path`，选择 `new`
- 点击 `...`（最右侧的三个点）
- 选择 `C:\MCC18, bin`，然后点击 `OK`
- 点击 `Project`，点击 `Build options` 然后点击 `project`
- 在 `output directory` 中向下滚动到 `Library Search Path`，选择 `new`
- 点击 `...`（最右侧的三个点）
- 选择 `C:\MCC18`，然后点击 `OK`
- 点击 `Project`，点击 `Build options` 然后点击 `project`
- 在 `output directory` 中向下滚动到 `Include Search Path`，选择 `new`
- 点击 `...`（最右侧的三个点）
- 选择 `C:\MCC18`，然后 `h`，点击 `OK`

注意 `addition.c` 列在 `Source Files` 下。接下来，点击 `Project` 然后 `build all`（或者只点击‘全部构建’图标，即调试工具栏右上角的第三个图标），查看以下界面：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_485_0.png)

这意味着编译 C 程序成功。接下来将使用调试器验证结果。

点击 `Debugger`，选择 `Tool`，然后 `MPLAB SIM` 以查看以下显示：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_486_0.png)

点击 `MPLAB SIM` 以查看以下内容：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_486_1.png)

点击 `View`，`toolbars`，然后 `Debug` 以查看带有调试工具栏的以下显示：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_487_0.png)

在上方，找到调试工具栏。如果出于某种原因，调试工具栏缺失，请转到 `view`，选择 `Toolbars`，点击 `Debug`。

接下来，点击 `View`，然后 `watch` 以查看以下内容：

在 `Watch list` 中，你现在可以包含位置 `a`, `b`, `c` 来监视它们的内容。例如，要添加 `a`，只需在 `Add Symbol` 窗口中通过箭头向下滚动选择 `a`，然后点击 `Add Symbol` 以查看以下显示：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_488_0.png)

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_489_0.png)

可以看到 `a` 显示在 `watch window` 中。类似地，显示 `b` 和 `c`，查看以下屏幕截图：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_489_1.png)

接下来，插入断点。为此程序将插入三个断点。一个用于 `int a = 5`，一个用于 `int b = 1`，一个用于 `c = a+b`。要插入断点，将光标移动到要插入断点的那一行的左侧。例如，要在 `int a = 5` 处插入断点，将光标移动到该行左侧，右键点击并查看以下显示：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_490_0.png)

接下来，点击 `Set Breakpoint` 以查看以下内容：

该行左侧红色的 B 表示断点已插入。类似地，为 `b` 和 `c` 插入断点，并获取以下显示：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_491_0.png)

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_492_0.png)

接下来，转到 `Debug` 菜单和 `Watch` 菜单，以查看每一行执行时 `a`, `b`, 和 `c` 的内容。

首先转到 `Debug` 菜单，左击 `reset`（最右侧的第一个符号），然后点击称为 `Run` 箭头的单个箭头（调试菜单最左侧的箭头），接下来将执行代码 `int a = 5;`。再次左击单个箭头，代码被执行，并显示以下内容：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_493_0.png)

注意 `a` 包含 `5`。接下来，左击单个箭头，将显示以下内容：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_493_1.png)

注意执行 `int b = 1;` 后，`b` 包含 `1`。

接下来，左击单个箭头，然后左击 `Halt`（调试菜单从左数第二个带两条垂直线的图标），以查看执行完该行 `c = a + b;` 后的最终结果如下：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_494_0.png)

在上方，可以看到 `c` 包含 `6`（最终答案）。

调试现已完成。

### 附录 H：

使用 `PICKit™ 3` 将 `PIC18F4321`

连接至个人电脑

或笔记本电脑

附录 D 包含了如何将编译后的 C 程序（使用附录 G 中的 `MPLAB_C18` 编译器编译）从个人电脑或笔记本电脑下载到 `PIC18F4321` 内存中的步骤。使用 Microchip 的 `PICKit3` 来完成此任务。`PIC18F4321` 包含在面包板上。请注意，面包板上的 `PIC18F4321` 硬件是由设计者为特定应用设计和构建的。

成功下载所需程序后，可以将基于 `PIC18F` 的面包板从个人电脑或笔记本电脑断开。然后，面包板上的 `PIC18F4321` 芯片可以在激活 `RESET` 按钮后执行已下载到其内存中的程序。因此，可以实现所需任务。

附录 H 包含以下内容：

- H.1 `PIC18F4321` 的初始硬件设置
- H.2 通过 `PICkit™ 3` 将个人电脑（PC）或笔记本电脑连接到 `PIC18F4321`
- H.3 使用 `PICKit™ 3` 从个人电脑或笔记本电脑为 `PIC18F4321` 编程

#### H.1 PIC18F4321 的初始硬件设置

图 H.1 显示了 `PIC18F4321` 微控制器的初始设置。`PIC18F4321` 的 `#1` 引脚是微控制器的 `RESET` 输入。`MCLR`（`#1` 引脚）必须连接到图中所示的复位电路。`PIC18F4321` 上有两对引脚必须连接到电源和地。例如，引脚 `11` 和 `32` 必须直接连接到 `+5 V`，而引脚 `12` 和 `31` 直接接地。务必不要在这些引脚上连接任何电容，将它们直接连接到地或 `+5 V`。对于名称中包含 `F` 的任何 `PIC18` 系列微控制器，例如 `PIC18F4321`，其工作 `Vdd` 范围在 `4.2 V` 到 `5.5 V` 之间。图 H.1 还显示了将连接到编程器的排针的正确连接方式。注意编程器有六个引脚，但第六个引脚（`Aux` 引脚）不进行任何连接。在正确连接 `PIC18F4321` 之后，必须安装相应的软件。

为了与 `PIC18F` 进行接口，必须安装两个程序。第一个程序称为 `MPLAB`，最新版本可从 `www.microchip.com/MPLAB` 下载。第二个称为 `MPLAB_C18`，是 `PIC18F` 的 C 编译器，可在 `www.microchip.com/c18` 找到。请注意，在该站点上

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_496_0.png)

**图 H.1** `PIC18F4321` 初始设置

一个供学术用途使用 C18 编译器的链接；请务必点击该链接并下载学生版 C18 编译器。软件安装完成后，即可准备实现 `PIC18F`。

#### H.2 通过 PICkit3 将个人电脑 (PC) 或笔记本电脑连接到 PIC18F4321

首先，应实现面包板上的 `PIC18F4321` 初始设置电路。接下来，使用 `PICkit™ 3` 将个人电脑或笔记本电脑连接到 `PIC18F4321`。图 H.2 展示了实现的简化框图。

图 H.3 展示了实现的示意图。以下图片展示了上述框图的初始设置及复位电路在面包板上搭建完成后的样子：

电路搭建完成后，如图 H.4 所示，可以将 `PICkit™ 3` 连接到电脑的 `USB` 端口。接下来，如图 H.5 所示，可以将 `PICkit™ 3` 的接头部分连接到面包板上的插针上。

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_496_1.png)

**图 H.2** 使用 `PICkit™ 3` 的 `PIC18F4321` 计算机接口

现在可以将其他必要的 I/O 设备（如开关、LED、LCD 和七段显示器）连接到面包板上的 `PIC18F4321`，以进行一些有意义的实验。在实现所需的硬件后，可以使用 `MPLAB` 软件对 `PIC18F4321` 进行编程。

#### H.3 使用 PICKIT3 从个人电脑或笔记本电脑对 PIC18F4321 进行编程

为了从个人电脑或笔记本电脑配置 `PICkit3`，用户需要点击 `Programmer`，然后选择 `PICkit3`，如下所示：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_497_0.png)

**图 H.3** 面包板实现的示意图

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_498_0.png)

**图 H.4** 将 `PICkit™ 3` 连接到 `USB` 端口的示意图

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_498_1.png)

**图 H.5** 将 `PICkit™ 3` 连接到面包板

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_499_0.png)

将出现以下带有警告标志的屏幕截图。请确保 `PIC18F4321` 微控制器连接到正确的电压，然后点击 `OK`，如下所示：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_499_1.png)

`PICkit3` 现在已连接。

顶部菜单会出现多个用于对 `PIC18F4321` 进行编程的选项。屏幕截图如下所示：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_500_0.png)

成功汇编或编译程序后，点击 `program` 选项，`MPLAB` 将把程序下载到微控制器中。将出现以下消息，表明代码已成功编程并验证到 `PIC18F` 上：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_500_1.png)

这将完成从电脑向 `PIC18F4321` 微控制器下载程序的过程。

### 参考文献

- **Avinash**, *Using the ADC (Analog to Digital Converter) of PIC Microcontroller* (使用 PIC 微控制器的 ADC [模数转换器]), 2010 年 7 月 21 日。 http://extremeelectronics.co.in/author/Avinash
- **bestmicrocontrollerprojects.com** *PIC Microcontroller hardware programming methods* (PIC 微控制器硬件编程方法).
- **byteparadigm.com** *Introduction to I2C and SPI protocols* (I2C 和 SPI 协议简介).
- **exploreembedded.com/wiki/PIC18F4520_Timer** *PIC18F4520 Timer* (PIC18F4520 定时器)
- **Gaonkar, Ramesh S.**, *Fundamentals of Microcontrollers and Applications in Embedded Systems (with the PIC18F Microcontroller Family* (微控制器基础及嵌入式系统中的应用 [基于 PIC18F 微控制器家族], *Thomson Delmar Learning*, 2007 年.
- **Geek Stuff and the geekstuff.com** *C Arrays basics* (C 数组基础).
- **Huang, Han-Way**, *PIC Microcontroller: An Introduction to Software and Hardware Interfacing* (PIC 微控制器：软硬件接口简介). *Thomson Delmar Learning*, 2005 年.
- **Johnsonbaugh, R. and Kalin, M.**, *C for Scientists and Engineers* (面向科学家和工程师的 C 语言), *Prentice Hall*, 1997 年.
- **Majidi, M. A., Mckinlay, R. D., and Causer, D.**, *PIC Microcontroller and Embedded Systems using assembly and C for PIC18* (使用汇编和 C 语言的 PIC18 微控制器及嵌入式系统), *Prentice Hall*, 2008 年.
- **Majidi, M. A., Mckinlay, R. D., and Causer, D.**, *PIC Microcontroller and Embedded Systems using assembly and C for PIC18* (使用汇编和 C 语言的 PIC18 微控制器及嵌入式系统), *Muhammad Ali Majidi*, 2016 年.
- **Microchip**, *Using the PIC Devices’ SSP and MCCP modules for slave I2C Communication* (使用 PIC 器件的 SSP 和 MCCP 模块进行从机 I2C 通信), 2008 年.
- **Microchip**, *PIC18F46K20 Starter Kit C18 Lessons* (PIC18F46K20 入门套件 C18 教程), 2007 年.
- **Microchip Technology, Inc.**, *PIC18F4321 Family Data Sheet* (PIC18F4321 系列数据手册), 2009 年.
- **microchipdeveloper.com**, *External clock oscillator mode* (外部时钟振荡器模式).
- **microchipdeveloper.com**, *Internal oscillator* (内部振荡器).
- **microcontrollerboard.com**. *PIC Analog Digital Converter Tutorial* (PIC 模数转换器教程).
- **Mikroelektronika**, *Clock Oscillator* (时钟振荡器), learn.mikroe.com.
