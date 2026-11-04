

```csharp
public void SetCountdown(int numTicks) {
    isCountdown = numTicks > 0;
    ticks = numTicks;
    tickCounter = ticks;
}

public void Tick() {
    if (!isActive)
        return;

    // Call any custom function
    remoteHandler(this, payload);

    // decrement the counter
    if (isCountdown)
        if (tickCounter > 0)
            tickCounter--;
        else
            isActive = false;
}

public void Reset() {
    tickCounter = ticks;
    isActive = true;
}

// Dummy for default tick-handler
public void DoNothing(TimedEvent e, Object o) {}
}
```

## Utils.cs

Utils.cs 文件中的 Utils 类是基础实用工具的集合，重点在于使用 Windows 多媒体功能生成声音。它旨在简化我们的 Windows Forms 和 GDI+ 游戏中对声音的引用，并作为 DirectSound 的备份/替代方案（参见示例 5.76）。

### 示例 5.76. Utils.cs

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Windows.Forms;
using System.Runtime.InteropServices;
using System.Threading;

namespace GameClasses {
    public class Utils {
        // External function to play sounds
        [DllImport("winmm.dll")]
        public static extern long PlaySound(String lpszName, long hModule,
            long dwFlags);

        // Static Variable .config file's contents
        public static System.Collections.Specialized.NameValueCollection
            Config =
            System.Configuration.ConfigurationSettings.AppSettings;

        // Error-handling LoadImage function
        public static Image LoadImage(String strFileName) {
            Image imgLoad = null;
            try {
                imgLoad = Image.FromFile(strFileName);
            } catch (FileNotFoundException ex) {
                MessageBox.Show("Please check that the following file " +
                    "exists:\n\n" + ex.Message + "\n\nCorrect the file " +
                    "referenced in the config file.", "File Not Found!");
                Application.Exit();
            }

            return imgLoad;
        }

        // PlaySound simple pass-through function. Removes dependency for
        // other classes to reference winmm.dll.
        public static void PlaySound(String strFileName) {
            ThreadedSound snd = new ThreadedSound(strFileName);
            Thread worker = new Thread(new ThreadStart(snd.Play));
            worker.Start();
        }
    }
}
```

```csharp
class ThreadedSound {
    public string strFileName;

    public ThreadedSound(string file) {
        strFileName = file;
    }

    public void Play() {
        //Console.WriteLine("Playing: " + strFileName);
        PlaySound(strFileName, 0, 0);
    }
}
```

## Wall.cs

Wall 是一个基本概念，用于限制我们角色（包括友方和敌方）的路径。墙的构造基于其宽度、长度和厚度。墙使用标准笛卡尔坐标定位。画笔用于绘制 GDI+ 模型，而 DirectX 仅检索坐标并在游戏内部处理绘制（参见示例 5.77-5.79）。

### 示例 5.77. Wall.cs

```csharp
using System;
using System.Drawing;

namespace GameClasses {
    public class Wall {
        public const int HORIZONTAL = 1;
        public const int VERTICAL = 2;
        public const int DEF_THICKNESS = 8;

        public int orientation;
        public Point start;
        public int length;
        public int thickness;

        private Brush brush;
        private Color color;
        private Rectangle rect;

        public Wall(int orientation, Point start, int length,
            Color color) :
            this(orientation, start, length, DEF_THICKNESS, color) {}

        public Wall(int orientation, Point start, int length,
            int thickness, Color color) {
            this.orientation = orientation;
            this.start = start;
            this.length = length;
            this.thickness = thickness;
            this.color = color;

            rect = new Rectangle(start, (orientation == HORIZONTAL) ?
                new Size(length, thickness) : new Size(thickness,
                length));
            this.brush = new SolidBrush(this.color);
        }
    }
}
```

### 示例 5.78. Intersects.

```csharp
public bool Intersects(AnimatedImage obj) {
    int x = obj.imagePosX, y = obj.imagePosY;
    int x2 = obj.imagePosX + obj.imageWidth;
    int y2 = obj.imagePosY + obj.imageHeight;
    int _x = rect.X, _y = rect.Y;
    int _x2 = rect.X + rect.Width, _y2 = rect.Y + rect.Height;

    return ((x >= _x && x <= _x2) || (x2 >= _x && x2 <= _x2)) ||
        (_x >= x && _x <= x2) || (_x2 >= x && _x2 <= x2) &&
        ((y >= _y && y <= _y2) || (y2 >= _y && y2 <= _y2) ||
        (_y >= y && _y <= y2) || (_y2 >= y && _y2 <= y2));
}
```

### 示例 5.79. 显示与矩形

```csharp
public void Display(Graphics g) {
    g.FillRectangle(brush, rect);
}
```

```csharp
public Rectangle getRectangle() {
    return(rect);
}
```

## Direct3D 简介

Managed Direct3D 是一种低级图形应用程序/编程接口，用于为静态和动画项目渲染二维和三维图像，这些项目既涉及基础程序，也涉及图形密集型程序。Managed Direct3D 利用硬件加速来生成高质量实时图形，同时与之前版本的 DirectX 相比，学习曲线仅需极少的时间成本。Managed Direct3D 的命名空间包含近 300 个类、结构、枚举和委托，其中每个都包含大量成员、属性和字段。幸运的是，大多数应用程序只需要少量常见引用，通常从设备类开始（详见 Direct3D 的设备类）。

### Direct3D 的设备类

设备类包含三个构造函数，其中在 Managed DirectX 中只使用一个：`public Device(int adapter, DeviceType deviceType, Control renderWindow, CreateFlags behaviorFlags, PresentParameters [] presentationParameters);` 第一个参数 *adapter* 指计算机引用的物理设备，它具有唯一的适配器标识符（注意，零表示默认值）。*deviceType* 包括 *Hardware*、*Reference* 和 *Software*。*Hardware* 指直接访问，而 *Reference* 指仿真。（当硬件不支持所请求的功能时，需要仿真。）*Reference* 光栅化器要慢得多，并且要求所有用户都安装 SDK；因此，它只应用于调试。还有一种自定义的 *Software* 光栅化器，其可用性有限。*behaviorFlags*（behaviorFlags.SoftwareVertexProcessing）控制设备的行为，指定我们的处理单元，例如 CPU 和 GPU。（GPU 提供最佳性能；同样，这取决于硬件可用性）。构造函数 *presentationParameters* 用于控制呈现，它包括两个关键成员：*Windowed* 和 *SwapEffect*。Windowed 成员（布尔类型）用于确定窗口状态（true 表示窗口模式，false 表示全屏模式），而 SwapEffect 用于控制缓冲区行为。SwapEffect.Copy、SwapEffect.Discard 和 SwapEffect.Flip 分别用于复制、丢弃和翻转。Flip 会创建一个额外的后台缓冲区，而 Copy 要求我们将后台缓冲区设置为一个；Discard 只是丢弃缓冲区的内容。

Device 还包括 Clear 和 Present 方法。Present 是两者中较简单的一个，没有参数，用于将图形呈现到屏幕。Clear 至少包含四个参数：ClearFlags、Color、float zdepth 和 int stencil。目前，我们将把这些设置限制在最基本的级别：(ClearFlags.Target, Color.Empty, 0.0f, 0)。我们还需要构建一个 Windows 应用程序，添加对 DirectX、DirectX.Direct3D 和 Direct3DX 的引用。（注意，我们不包含 using Microsoft.DirectX.Direct3D; 这一语句；参见 CD-ROM 上的示例 5.80。）

## 使用 Direct3D 显示 2D 图像

与 DirectDraw 一样，Direct3D 使用简单的 Draw 命令来显示图像，不过 Direct3D 的 Draw 命令版本需要七个参数，即 spriteTexture、sprite、textureSize、scaling、rotation、transition 和 color。前三个参数与位图主体有关：spriteTexture 引用实际加载的图像或位图文件（*.bmp），sprite 用于将我们的位图链接到 Device 类，textureSize 用于设置该纹理的大小。随后，scaling 决定渲染图像的大小；rotationCenter、rotation 和 translation 与角色位置有关（translation 使用笛卡尔坐标放置图像）；color 显然决定图像的颜色。

这里我们还想介绍用于包含绘制函数的方法，它们被恰当地命名为 BeginScene ( ); EndScene ( ); 这些方法可以构建到用户定义的图形调用中，或作为 OnPaint 引用的一部分（参见 CD-ROM 上的示例 5.81）。

## Direct3D 的 2D 动画——基础

图像位置由平移坐标 x、y 以及可能的 z 控制。对这些值进行加减，本质上就产生了移动。然而，这种移动不应被视为真正的动画，而只是一种简单的位移形式。要

