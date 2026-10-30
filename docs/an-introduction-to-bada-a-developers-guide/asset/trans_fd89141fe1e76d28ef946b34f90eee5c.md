

## 第 2.4 阶段：编程

在此阶段，设计应被转化为能够最终成功通过所有测试用例的程序代码。尽管移动设备变得越来越强大，但仍然强烈建议编写高效的代码，并以保守的计算为目标，以尽可能节省电池容量。延长电池电力的可用性至关重要，正如我们在第 1 章中所论证的那样。

bada IDE 理想地为你编写程序代码提供了一切所需，例如语法高亮、代码补全、全面的文档和示例材料，以及所有必要的编译、链接、部署和运行功能。

还必须理解，每款移动应用程序都受制于一种“技术”应用程序生命周期，其中包含初始化、运行、终止和已终止。bada 平台以及你用来访问它的 IDE 为处理此应用生命周期提供了支持，并在适当阶段做正确的事情（通过定义明确的方法）。

## 第 2.5 阶段：测试

在移动软件工程过程中，必须在测试阶段投入很大精力。重要的是区分测试平台和真实平台。测试平台通常是运行移动设备仿真的台式计算机。不幸的是，仿真器与真实移动设备存在很大差异。仿真器测试是在理想的实验室环境中进行的，其中上下文因素如位置或光照条件要么不被考虑，要么被模拟。因此，有必要在真实的目标移动设备上以及软件预期使用的真实环境中测试软件。所有“可控”变量都必须被软件捕获，例如根据设备功能的行为、适应屏幕尺寸、屏蔽网络中断或 GPS 信号丢失。

这最后三个阶段（定义测试用例、编程和测试）以许多微迭代为特征，实际上在现实中也是部分并行执行的。特别是，测试自然会与测试用例定义和编程阶段迭代。它通常也会与设计细化和需求审查阶段迭代。

## 第 2.6 阶段：用户验收测试

第二阶段结束时的用户验收测试再次是可选的但推荐的。这样，工程师可以确保真正满足用户需求，并且软件版本越来越接近最终状态。此类测试可以重复进行，其结果可以反馈到该阶段的早期步骤。诸如音视频记录、问卷、合作评估、焦点小组或受控实验等人类-计算机交互技术可以部署并有益。

在利益相关者接受移动软件的现有版本后，可以将其标记为发布。这意味着里程碑 版本已发布 得到满足，并且可以开始同一阶段的下一次迭代（以实现进一步的增量）或后续阶段。

## 第 3 阶段：分发

该阶段主要处理将移动软件产品带入市场供用户使用。该阶段比其他两个阶段迭代性更低。它由三个阶段组成：营销、准备部署、产品维护，以及阶段末的里程碑。

## 第 3.1 阶段：营销

营销阶段体现了移动软件工程和产品管理流程的重叠和互补之处。该阶段用于业务模式和分发政策的最终确定，以及为软件产品的实际市场进入做准备。营销部分与其它阶段并行，并在更早阶段开始。

## 第 3.2 阶段：准备部署

在此步骤中，软件必须被准备好（即认证），以便能够适当访问移动设备的所需功能。必须决定哪些组件和内容打包在一起，哪些部分可以按需下载或安装。还必须准备分发渠道，这通常涉及申请应用商店账户并熟悉相关政策。最后，移动软件在物理上分发并安装到终端用户的设备上。

## 第 3.3 阶段：产品维护

维护涵盖支持、错误修复和反馈集成。此步骤——取决于报告问题的严重性和应用程序提供商的政策——可能导致与准备部署阶段的额外迭代。此外，维护的水平和对它的承诺取决于提供商，可以从 24/7 服务到完全无支持不等。移动软件工程流程以利益相关者和项目经理定义的结束事件（里程碑：项目结束）结束。

## 索引

A
abstract methods, 69
ad hoc Wi-Fi network, 401–406
AddControl() method, container, 76
AddItem() method, List control, 94
Addressbook class, 195–196, 235–236
AdhocService class, 191–192, 404–405
AesSecureRandom class, 193
agile software development, 15–17
Alarm class, 201–202
Amazon S3 (Simple Storage Service), 131, 153–155, 417–421
AMOLED display (Samsung), 11, 30, 89
Animation control, 75
App namespace, 160–162
app store, 13, 14
AppAssert() macro, 29
AppAssertIf() macro, 29
AppControl class (Application Control), 161, 162, 228–236
Append() method, strings, 119
Application class, 64, 161–162
Application Control (AppControl class), 161, 162, 228–236
Application Manager (AppManager class), 161, 229
application registry, 213–216
applications. See also mobile software
base applications. See base application
building, 25–26, 46
certifying, 61
creating, 21–22
described, 20–21
development of. See mobile software development
folder structure of, 23–25
GUI for. See GUI (Graphical User Interface)
icon for, 46–47
ID for, 51, 52
lifecycle of, 65–69
localisation for. See localisation
logging, 28–29
package for, creating, 60
privileges for, 53, 125–127, 160
profile for, 51–53
publishing, 61–62
running in Simulator, 26–27, 46
secret key for, 52
splash screen for, 27
testing. See testing
application.xml file, 25–26, 51–53
AppLog() macro, 28
AppLogDebug() macro, 28
AppLogException() macro, 28
AppManager class (Application Manager), 161, 229
AppRegistry class, 214–216
architecture of bada, 98, 101–103
ARGB colour model, 89
ArrayList class, 122, 164–165
arrays, 106, 121. See also Buffer class

ASCII encoding, 120
audio
playing, 369–374
recording, 366–369
AudioRecorder class, 183–184, 367–369
azimuth measurement, 332

Bluetooth namespace, 187–188
Bluetooth profiles, 388–395
BluetoothDevice class, 187–188, 389
BluetoothManager class, 187–188, 389
BluetoothOppClient class, 389
books about user interface design, 29
Boolean class, 118
browser
downloading files in, 315–319
launching using Application Control, 229–231
launching using Web control, 314–315
Browser base application, 229–231
buddy lists. See also Social service
adding buddy to, 446–450
described, 31
requests of, 142–146
BuddyFix application example
app icon for, 46–47
building, 25–26
creating, 21–22
folder structure for, 23–24
Form for, 33–38
GUI for, 33–41
list for, creating, 38–41
list for, populating, 94–96
metadata for, 24–25
Option menu for, 77–78, 90–93
running in Simulator, 26–27
soft key for, 93–94
BuddyService class, 197–199
Buffer class, 121
BufferBase class, 118
BufferType class, 121
building applications, 25–26, 46
built-in memory, 229
Button control
adding to Form, 263–269
containing an image, 267–268
containing text, 263–267
described, 72
ByteBuffer class, 121, 163

B
bada. See also specific topics
architecture of, 98, 101–103
features of, 2–5, 98–99
history of, 99–100
bada developer programme, 51
bada SDK
downloading and installing, 453–455
help system for, 457
running sample projects, 455–456
system requirements for, 453
bada Server. See also mobile services
creating content for, 417–421
described, 102
privileges for, 160, 161
Ballard, Barbara (author)
Designing the Mobile User Experience, 29
base application
Browser base application, 229–231
Contact base application, 231–235
described, 229
launching from bada application, 228–236
Player base application, 373
Base namespace, 117–118, 162–168
Base::Collection namespace, 118, 164–166
Base::Runtime namespace, 166–167
Base::Utility namespace, 118, 167
battery capacity, of mobile hardware, 12
Binaries folder, 26
Bitmap class, 84–88, 171–172, 350–351, 354–355
bitmaps. See also graphics
creating from a file, 86–87
described, 83–85
displaying an image as, 350–351
drawing onto Canvas, 87–88, 354–355
transparency colour of, 366
blocking sockets, 401

C
C++
alternatives to, 104
described, 103
exception handling, 111–114

