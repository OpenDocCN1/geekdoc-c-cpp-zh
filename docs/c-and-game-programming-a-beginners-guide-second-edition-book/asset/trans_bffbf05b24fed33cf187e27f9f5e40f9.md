
## 构建游戏类

与之前的游戏一样，我们接下来的两个游戏也依赖于一组类、它们的实例以及大量操作数据以产生我们所看到的网络创作的方法。这些实例及其组件是利用本章收集的知识库构建的，因此在此讨论这些技术是明智的。我们将讨论的第一个类是所有游戏中的关键组件；它用于创建角色、他们的武器以及屏幕上几乎所有出现的对象。

### 游戏类—AnimatedImage.cs

名为 AnimatedImage 的类将用于控制我们的角色，包括它们的外观、移动和限制。在此类的前面我们将包含一组 System 引用；这些引用由接下来的几节中包含的多个方法所必需。始终有必要将我们的类包装在明确标记的命名空间内，在本例中为命名空间 Games。然后，我们将声明一些字段并创建我们的构造函数（注意构造函数重载对于多种设置而言是多么重要——请参阅 CD-ROM 上 Game Classes 文件夹中的 AnimatedImage.cs）。

### 示例 5.61. AnimatedImage.cs

```
/*AnimatedImage.cs: Contains the AnimatedImage class, which is a
* generic class capable of holding and doing animation logic for
* an image. You can sub-class this object to customize its behavior.
*/

using System;
using System.Drawing;

namespace GameClasses {
    public class AnimatedImage {
        // Constants
        public const int DEFAULTSTEP = 3;
        public const int SOUTHWEST = 1;
        public const int SOUTH = 2;
        public const int SOUTHEAST = 3;
        public const int EAST = 4;
        public const int NORTHEAST = 5;
        public const int NORTH = 6;
```

```csharp
public const int NORTHWEST = 7;
public const int WEST = 8;

// Member data
public int imageWidth; // Width of the image
public int imageHeight; // Height of the image
public int imagePosX; // X Position in containing object
public int imagePosY; // Y Position in containing object
public Image imageData; // The image itself

public int imageOffsetX; // facilitates "relative" positioning
public int imageOffsetY; // by placing image at a specified
// offset to PosX, PosY.

public int animationStep; // How much the image should move/step

public Rectangle constraintBox; // Our sandbox to play in
public int direction; // current direction the image is heading
public bool isActive; // whether the image should be animated
public AnimatedImage owner; // if it's controlled by another image

#region Constructors
public AnimatedImage() : this(0,0) {} // default constructor

public AnimatedImage(int posX, int posY) {
imagePosX = posX;
imagePosY = posY;
isActive = false;
animationStep = DEFAULTSTEP;
}
#endregion
...
```

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_426_0.png)

> 记住，C# 类引用不是主程序的一部分，因此不需要 main 方法。此外，值得注意的是，该类被留为开放式，以便包含我们的方法，这些方法将在接下来的几节中讨论。

## 动画

动画是基于若干要素的运动幻觉，其中包括背景变化、角色外观变化以及物体的实际物理位移。因此，本节旨在从笛卡尔坐标的角度以及通用方法的角度回顾动画。方法 `Animate()` 将作为 AnimatedImage 类的一部分包含在内。作为通用类/方法，AnimatedImage 及其组件 Animate 将可被我们所有的游戏检索/已检索。表达式 using GameClasses 使这些组件可用。

`Animate` 是一个不返回类型的虚公共方法。该方法包含一个 switch 语句，使用 North、South、East 和 West 来表示 Up、Down、Left 和 Right。Southeast、Southwest、Northeast 和 Northwest 允许对角线移动。

### 示例 5.62. 动画对象

在这里，我们将想要创建我们的第一个方法——注意名称 `Animate()` 如何传达其含义。当然，它实际上只是一个由 switch 语句控制的简单值操作集合，但将其放在类内部，我们极大地提高了其潜力。

```java
// Animate() performs all position movements on the object.
virtual public void Animate() {
    switch(direction) {
        case SOUTHWEST:
            this.imagePosX -= animationStep;
            this.imagePosY += animationStep;
            break;
        case SOUTH:
            this.imagePosY += animationStep;
            break;
        case SOUTHEAST:
            this.imagePosX += animationStep;
            this.imagePosY += animationStep;
            break;
```

```csharp
case WEST:
    this.imagePosX -= animationStep;
    break;
case EAST:
    this.imagePosX += animationStep;
    break;
case NORTHWEST:
    this.imagePosX -= animationStep;
    this.imagePosY -= animationStep;
    break;
case NORTH:
    this.imagePosY -= animationStep;
    break;
case NORTHEAST:
    this.imagePosX += animationStep;
    this.imagePosY -= animationStep;
    break;
}
```

## 显示

标准图像显示很简单，只有三个步骤：1) Graphics 声明，我们将使用字母 g；2) 方法 DrawImage，它包含在通过 g 访问的 drawing 类中，如 g.DrawImage；以及 3) DrawImage 引用的签名，例如，角色的实际图像、x 坐标、y 坐标、其宽度和高度。请注意，列出的变量实际上是在类顶部部分声明的字段（请参阅 CD-ROM 上的 AnimatedImage.cs 和第 3 章中的示例 3.46）。

## 图像缩放

如上一节所示，我们图像的高度和宽度在显示中起着重要作用。然后，高度和宽度可以根据需要使用方法 Rescale 进行重置、增加或减小，该方法也位于文件 AnimatedImage.cs 中（请参阅 CD-ROM 上的 AnimatedImage.cs 和第 3 章中的示例 3.47）。

## 为角色添加实质

在大多数情况下，角色只是幻觉——它们的图像没有任何真正的实质。因此，自然限制、偏转甚至碰撞都不会被计算机注意到，除非，当然，我们编写大量定义这些响应的方法。所有这些都相对简单，通常只涉及记录几个关键点，并在角色绊倒这些点时反转或禁用角色（请参阅示例 5.65–5.69）。

### 示例 5.63. ContainsPoint.

// Determines if the point is within the confines of this image
virtual public bool ContainsPoint(int x, int y) {
    return (x >= imagePosX && x <= imagePosX + imageWidth &&
            y >= imagePosY && y <= imagePosY + imageHeight);
}

在这里我们需要确定矩形（或墙）是否与我们的角色相交。这是通过仔细比较每个坐标包括图像的高度和宽度来完成的。应注意，该方法被重载，其中一个比较使用实际点，另一个使用图像。

### 示例 5.64. Intersects.

碰撞检测是游戏中另一个非常常见的关键点，因此将其放在我们的类中是合乎逻辑的。

// Determines if the given rectangle intersects this image
virtual public bool Intersects(int x, int y,
    int width, int height) {
    // simple variable renaming
    int x2 = x + width, y2 = y + height, _x = imagePosX;
    int _y = imagePosY, _x2 = imagePosX + imageWidth;
    int _y2 = imagePosY + imageHeight;

    return ((x >= _x && x <= _x2) || (x2 >= _x && x2 <= _x2) ||
(_x >= x && _x <= x2) || (_x2 >= x && _x2 <= x2)) &&
(y >= _y && y <= _y2) || (y2 >= _y && y2 <= _y2) ||
(_y >= y && _y <= y2) || (_y2 >= y && _y2 <= y2));
}
virtual public bool Intersects(AnimatedImage img) {
return Intersects(img.imagePosX, img.imagePosY,
img.imageWidth, img.imageHeight);
}

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_430_0.png)

> 现在我们对宇宙有了把握，我们将想要关注导弹和/或球体使用的运动。在这里我们需要根据潜在的游戏将方法分开。记住，我们不一定知道我们的方法将如何被使用和/或在本书出版后可能会创建什么新游戏。物体的运动可分为两种可能类型：标准武器发射和球体的反弹效果。

ConstrainToBox 命令将图像保持在屏幕内——Box 为窗口，图像为我们的动画角色。如果角色试图超出限制，X 和 Y 坐标将被调整以将其移回。

### 示例 5.65. ConstrainToBox.

// Moves the image to be within the specified boundary.
// Returns whether any position changes were made.
virtual public bool ConstrainToBox() {
bool retVal = false;

if (!isActive)
return false;

if (imagePosX < constraintBox.X) {
imagePosX = constraintBox.X;
retVal = true;
} else if ((imagePosX + imageWidth) >
(constraintBox.X + constraintBox.Width)) {
