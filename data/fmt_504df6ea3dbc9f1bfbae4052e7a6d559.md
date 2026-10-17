
<html>

<head></head>

<body>

{% if latest_GPS %}

<ul>

    {% for co in latest_GPS %}

    <li>

        I am located at <a href="http://geohash.org/?q={{co.lat}},{{co.long}}">URL.</a>.

    </li>

    {% endfor %}

</ul>

{% else %}

    No coordinates

{% endif %}

</body>

</html>

```

这使用了 geohash.org，这是一种由 Gustavo Niemeyer 在编写 geohash.org Web 服务时发明的经纬度地理编码系统，并已进入公共领域。它提供了短 URL 来唯一标识地球上的位置，因此在电子邮件、论坛和网站中引用它们会更加方便。

图 6-10 显示了我们在编写这段代码（以及编写此书）时所在的位置。

![](img/001c747b841ab338ed35c50dbdd0c933_180_0.png)

图 6-10

## 总结

本章强调了 OEM（原始设备制造商）在考虑设备的“外观和感受”时可以针对的一些潜在用户群体。这并不是一个全的列表，还有其他重要的群体。例如，Ubuntu Mobile 团队成员识别出的一类用户位于亚洲，特别是日本，那里有许多人在乘坐公共交通工具时仅使用设备阅读电子书。如何针对这类群体留由你决定。这种挑战要求 OEM 创造性地思考如何与市场上的其他产品区分来。本章希望对这一过程提供一些见解。

---

# 第 7 章：主题（Theming）

这将根据可用设置显示界面。除了使用前端的 `gconf-editor` 外，还可以美观地检查设置。运行以下命令：

```
$ gconftool-2 -R /desktop/gnome
```

这会显示 Ubuntu 移动桌面的设置。运行以下命令：

```
$ gconftool-2 --get-default-source
```

这会显示 XML 后端的位置，GConf 使用其作为数据库。

## 修改主题

自定义主题通常是必要的，特别是在与 OEM 厂商合作时。在《GNOME 首页界面指南》发布之前，你可能想阅读《[视觉设计](http://library.gnome.org/devel/hig-book/stable/)》，该书开头如下：

> 视觉设计不仅仅是为了让你的应用程序美观。一个良好的应用程序会让使用户更容易地理解所呈现的信息，并清晰地向他们展示如何与信息进行交互。

将上述引言中的“应用程序”替换为“主题”，你就会对主题定制的目标有一个直观的理解。

## 处理主题时的实用工具

以下 bash 脚本显示了当前主题的信息。这在处理主题和 Gconf 时非常有用。

首先，安装 zenith，它是一个用于 GTK 组件的方便工具包：

```
$ sudo apt-get install zenith
```

调用名为 `get_theme_info.sh` 的脚本并像 `./get_theme_info.sh` 一样执行（需先赋予权限）：

```bash
#!/bin/bash

icons=$(gconftool-2 -g /desktop/gnome/interface/icon-theme)
theme_gtk=$(gconftool-2 -g /desktop/gnome/interface/gtk-theme)
theme_metacity=$(gconftool-2 -g /apps/metacity/general/theme)
font_gtk=$(gconftool-2 -g /desktop/gnome/interface/font_name)
font_meta=$(gconftool-2 -g /apps/metacity/general/titlebar_font)

echo "icons: $icons"
echo "GTK theme: $theme_gtk"
echo "metacity theme: $theme_metacity"
echo "gtk font: $font_gtk"
echo "metacity font: $font_meta"
```

结果显示了图 7-1 所示的信息。

![](img/001c747b841ab338ed35c50dbdd0c933_186_0.png)

图 7-1

## 主题结构

本节探讨了 Ubuntu MID 的移动主题。该主题基于 Hildon 的主题结构，Ubuntu 从上游继承了该结构。布局（位于 `/usr/share/themes/mobilebasic`）如下：

- `/usr/share/themes/mobiletheme/gtk-20/`
  - `index.theme`
  - `gtkrc`
  - `gtkrc.cache`
  - `images/`
    - `*.png`
  - `matchbox/`
    - `theme.xml`

该结构中的两个主要文件是 `theme.xml` 和 `gtkrc`。

### theme.xml 文件

通过修改 `theme.xml` 文件中的内容，可以实现简单的窗口装饰自定义。它还定义了主栏装饰和一些对话框装饰。

`theme.xml` 文件中的三个基本资源是：

- 颜色（Colors）
- 字体（Fonts）
- 图像（Images）

在使用它们之前，以以下格式声明它们：

```
id :definition
```

例如：

```
<type id="object name" definition="data" />
```

其中 `type` 是颜色、字体或位图，`id` 是对象的唯一名称，`definition` 是要设置的元数据。

颜色定义如下：

```
<color id="osso-DialogTextColor" def="#ffffff" />
```

字体定义如下：

```
<font id="osso-TitleFont" def="Nokia Sans-17.85" />
```

图像定义如下：

```
<pixmap id="dialogoptile" filename="../qgn_plat_dialog_frame_tile_top.png" />
```

### gtkrc 文件

涉及 `gtkrc` 文件的复杂自定义。该文件对于 Ubuntu Netbook Remix 和 Ubuntu MID 的主题是通用的；从概念上讲，可以认为 GTK 主题“存在”于 `gtkrc` 文件内部。文件格式对大小写敏感，注释用 `#`（井号）标记。也可以使用类似于 `/* * */` 的注释进行多行注释。

`gtkrc` 文件是一个由一系列声明组成的文本文件。在解析 `gtkrc` 时，井号字符会删除注释并忽略 `#` 之后的部分。

> 此 gtkrc 对拼写错误和错误的容忍度较低，更改代码时要小心。

## 自定义 gtkrc 文件

以下 `gtkrc` 文件将主题应用到所有组件（按钮、滚动条、编辑框）。

从技术上讲，每个组件都派生自 `GtkWidget`。这意味着对 `GtkWidget` 的更改将影响所有组件。

（注：此处原文示例代码未翻译，保持格式）

结果显示了图 7-1 所示的信息。

![](img/001c747b841ab338ed35c50dbdd0c933_186_0.png)

图 7-1

## 第 7 章：主题定制

打开此文件夹下的 `theme.xml`，并将元数据的第一行更改为：

```xml
<theme name="pumdtheme" author="Ian Lawrence" desc="A theme created for the book Professional Ubuntu Mobile Development, published by Wiley version="0.1*" engine_version="1" cache="false">
```

接下来，修改以下内容：

```xml
<color id="osso-TitleTextColor" def="#eec73e" />
<color id="osso-DialogTextColor" def="#403008" />
```

对于新的 MID，将 `gtk-20` 文件夹下 `gtkrc` 文件中的颜色定义更改为：

```bash
color["DefaultTextColor"] = "#eec73e"
color["EmTextColor"] = "#204a87"
color["PaintedDefaultTextColor"] = "#ffffff"
color["DisabledTextColor"] = "#babdb6"
color["ProgressText1"] = "#000000"
color["ProgressText2"] = "#000000"
color["SecondaryTextColor"] = "#5a5a5a"
color["TitleTextColor"] = "#000000"
color["DialogTextColor"] = "#403008"
```

这些步骤会更改主题中的字体颜色。

打开主目录下的 `theme.index` 文件并将其更改为：

```ini
[Desktop Entry]
Type=X-Hildon-Metatheme
Name=PUMTheme
Icon=/usr/share/themes/pumdtheme/Images/qn_plat_theme_thumbnail.png
Encoding=UTF-8

[X-Hildon-Metatheme]
GtkTheme=pumdtheme
IconTheme=gnome
X-MatchboxTheme=pumdtheme
X-OperaSkin=default.zip
```

同时，修改 `images` 文件夹中相应的图像。处理图像时可以使用一个名为 `xmag` 的实用工具，它由 `x11-apps` 软件包提供：

```
apt-install x11-apps
```

`x11-apps` 提供了系列随 X Window System 附带的杂项 X 应用，包括 `xmag`、`x11` 和 `x11forcomp`，这些都是用于测试 X Window System 下图形操作性能的工具（参见“主题性能测试”章节）。

完成上述所有更改并修改相应的图像将创建一个新主题。例如，图 7-2 所示的主题是基于 Ubuntu MID 的 Intrepid 发布版本。如果你没有新图像要添加，也可以清楚地看到终端带来的更改（终端颜色发生了变化）。

![](img/001c747b841ab338ed35c50dbdd0c933_191_0.png)

图 7-2

可以在默认主目录中包含一个 `.gtkrc-2.0` 文件来加载主题（这之所以有效是因为它加载了用于图标的 XSETTINGS）。

> XSETTINGS 是 Linux 上的一种机制，允许配置设置，并在运行时在所有应用程序中准备好这些设置。

用户主目录下的一个简单的 `gtkrc-2.0` 文件可以包含一个文件，如下所示：

```
$ cat ~/.gtkrc-2.0
include "/usr/share/themes/pumhtheme/gtk-2.0/gtkrc"
```

## 自动为 MID 设置主题

在上一节中，我们手动为 Ubuntu MID 设置了主题。可以通过 `hilden-theme-tools` 软件包来自动化此过程。使用 `apt` 安装：

```
$ sudo apt-get install hilden-theme-tools
```

该软件包包含了多种用于 Ubuntu MID 主题定制的工具。首先安装 `subprocess` 软件包：

```
$ sudo apt-get install subprocess
```

然后运行以下命令：

```
$ hilden-theme-bootstrap
```

这将一个骨架主题下载到指定的目录。进入模板目录，并在使用 GIMP 等图像编辑器时根据需要编辑 `template.svg`。

> 请确保你选择了第二个选项，2) hilden-theme-layout-4，因为 MID 不支持 layout-3。

接下来，为了构建该包的 debian 包，需要修改 `debian` 文件夹中的几处内容。在 `control` 文件中，删除对 `hilden-theme-cacher` 的依赖。在 `postinst` 文件中，删除 `DEBUILD` 之上调用主题缓存实用工具的行：

```
hilden-theme-cacher 用于缓存 gtkrc 文件 —— 在 Ubuntu MID 上不使用它。
```

接下来，安装构建主题包所需的依赖项：

```
$ sudo apt-get install fakeroot hildon-theme-layout-4 cdbs debhelper dpkg-dev
```

运行以下命令构建包：

```
$ dpkg-buildpackage -tc -rfakeroot
```

这将创建一个 `.tar.gz` 和一个 `.deb` 文件——例如，`hildon-theme-pumd_4.2.0-1_all.deb`。

`data` 目录下的 `Makefile` 会调用 `hildon-theme-subst`（`hilden-theme-tools` 软件包中的另一个工具），它会对 `gtkrc` 文件进行替换。

生成的 `deb` 文件可以部署到 PPA 或使用以下命令进行本地安装：

```
$ dpkg -i hildon-theme-pumd_4.2.0-1_all.deb
```

## 主题性能测试

可以对主题运行一系列性能测试。最简单的测试方法是使用 `metacity-theme-viewer`。

Metacity 是 GNOME 默认使用的复合式窗口管理器。

在 Ubuntu 上运行以下命令：

```
$ metacity-theme-viewer Human
```

它将输出以下结果：

- 在 0.02 秒内加载了主题 "Human"
- 在 0.61 客户端秒内绘制了 100 帧（每帧 16.1 毫秒），包括 X 服务器资源在内的墙钟时间为 3.4817 秒（每帧 34.8167 毫秒）

### 测试 Human Metacity 主题

该主题在所有标签页中都能正常渲染。还有一个 Benchmark（基准）标签页，用于与其他主题比较速度。例如，Ubuntu Remix 上的 Human 主题绘制一个窗口框需要 34.8167 毫秒，而 Simple 主题需要 84.8415 毫秒。

另一个用于 GTK+ 主题的基准测试工具叫做 GtkPerf。它可以通过 apt 安装（`sudo apt-get install gtkperf`）。该工具也适用于 Ubuntu MID。

可以像这样运行它：

```
gtkperf -a c 1000
```

### 比较

以下是在 LPIA 架构上对主题和网络启动器的测试结果。该设备是华硕 Acer Aspire One：

| 指标 | 结果 |
| :--- | :--- |
| GtkPerf 0.40 - 开始测试：2009年6月7日 周日 21:00:09 | |
| GtkEntry - 时间 | 1.31 |
| GtkComboBox - 时间 | 53.03 |
| GtkComboBoxEntry - 时间 | 35.79 |
| GtkSpinButton - 时间 | 7.05 |
| GtkProgressBar - 时间 | 15.13 |
| GtkToggleButtonButton - 时间 | 9.06 |
| GtkCheckButton - 时间 | 7.59 |
| GtkRadioButton - 时间 | 11.90 |
| GtkTextView - 添加文本 - 时间 | 17.83 |
| GtkTextView - 滚动 - 时间 | 17.47 |
| GtkDrawingArea - 线条 - 时间 | 25.75 |
| GtkDrawingArea - 圆形 - 时间 | 34.02 |
| GtkDrawingArea - 文本 - 时间 | 31.43 |
| GtkDrawingArea - Pixbufs - 时间 | 3.89 |
| **总时间** | **424.30** |

以下是在 XFACE 架构上对相同的 `xfce-ubuntu-golden` 主题和自定义启动器进行相同测试的结果：

```
GtkPerf 0.40 Starting testing: Sun Jun 14 13:56:20009

GtkEntry - time: 1.16
GtkComboBox - time: 27.28
GtkComboBoxEntry - time: 20.25
GtkSpinButton - time: 2.94
GtkProgressBar - time: 2.19
GtkToggleButton - time: 2.77
GtkCheckButton - time: 2.25
GtkRadioButton - time: 3.02
GtkTextView - Add text - time: 160.87
GtkTextView - Scroll - time: 12.03
GtkDrawingArea - Lines - time: 32.52
GtkDrawingArea - Circles - time: 33.27
```
