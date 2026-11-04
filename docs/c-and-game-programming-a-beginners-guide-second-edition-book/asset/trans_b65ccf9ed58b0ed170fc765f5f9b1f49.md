
在C#中使用goto语句的一个实际原因是为了在处理switch语句时允许人为的贯穿（fall-through）。请记住，C#不再允许我们在包含可执行语句的switch分支之间贯穿，因此goto是一个很好的解决方案。C#的goto也有其局限性，包括不能跳入局部作用域块、不能跨越类，并且不能（也不应该）用于改变try-catch块，如第5章所述（参见示例4.41）。

### 示例4.41：goto语句。

```csharp
using System;

namespace Chapter4 {
    class Class1 {
        static void Main() {
            char Character = '1';

            switch (Character) {
                case '1':
                    Console.WriteLine ("1 and a");
                    goto case2;

                case '2':
                    case2:
                        Console.WriteLine ("2");
                        goto case3;

                case '3':
                    case3:
                        Console.WriteLine ("and a 3");
                        break;
            }

            Console.WriteLine ("Program Terminated");
        }
    }
}
```

## 游戏4——战斗波

我们现在进一步深入游戏的演变过程。结合数组和指针的知识，我们终于可以自由地同时使用多个对象实例以及决定这些实例的信息数组。我们还能够简化这些流程

- 8. 如果所有外星人都被摧毁，一批新的飞船将出现在顶部。
- 9. 摧毁外星飞船将获得分数，并且分数将保存到记录高分的文件中。
- 10. 外星人的分值将从较低（前排飞船）到较高（后排飞船）排列。
- 11. 随着外星人数量的减少，它们将移动得更快。
- 12. 外星人还会偶尔随机开火。

## 绘制角色与定义动作

我们将再次使用编译器的图形功能来创建角色。外星飞船将集体移动，沿着x轴行进，当最外侧的外星人到达任一侧时，还会沿y轴附加移动。相比之下，我们玩家控制的角色只能使用数字键盘上的左、右箭头沿x轴移动，并使用空格键启用武器（参见示例4.42b）。

### 示例4.42b：设计角色。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_295_0.png)

> > **注意：** 外星人遵循简单的预设运动模式，而玩家则可以使用键盘。控制键将设置为4（b）和6（a），空格键用于发射角色武器。

### 示例4.43：战斗波的算法。

BattleWave.cpp:

- 1. 设置Windows环境。这包括我们的操作系统和编译器所需的一切。
- 2. 编写一组用于动画化我们角色的函数（包括外星/人类飞船和武器射击）。
- 3. 编写一个定义屏幕边界的函数。
- 4. 设置一个键盘函数，包含左右移动以及武器键。
- 5. 编写一组函数来控制玩家的武器以及人工智能外星人的武器控制系统。
- 6. 编写一个函数，在关卡完成后重置外星人。
- 7. 调用用于保存和读取玩家最高分的两个函数。

**游戏循环内部：**

- 8. 重置外星人以开始新的关卡。
- 9. 恢复/测试并显示最高分。
- 10. 显示角色。
- 11. 读取键盘输入。
- 12. 跟踪武器。
- 13. 检测碰撞。
- 14. 游戏运行时播放三种声音：武器射击、飞船移动和爆炸……
- 15. 测试边界（墙壁）。
- 16. 移动角色。
- 17. 清除屏幕。

外部循环：

- 18. 重复循环，直到外星人到达我们玩家的y轴位置。
- 19. 询问玩家是否想再玩一次。结束或重复游戏。

在继续之前，请确保一切设置正确（创建新项目、新源文件、添加声音文件、测试编译，并使用之前所有的游戏文件进行链接——所有这些都在project4中完成）。

## 绘制角色

请务必记住，DirectX要求我们的图形文件以位图（bitmap）格式存储，而且虽然Forms也可以使用位图，但大多数Windows Forms程序员更喜欢使用JPEG等低分辨率图形文件格式以节省资源。同样重要的是，这些区别仅仅是存储类型的不同，并不影响我们绘制图像所采用的步骤。例如，本书附带的CD-ROM中同时包含.JPG和.BMP格式的图像，它们最初是以位图创建的，然后以JPEG格式重新保存。

我们最初的设计只包含七幅独特的图画：四张目标图像（每张用多种颜色复制五次）、目标武器/炸弹（同样用多种颜色复制），以及一张人类图像和他的两枚火箭/导弹。四张外星人图像分别是灯泡怪（Bulb）、青蛙怪（Frog）、机器人怪（Robot）和眼睛怪（Eye），而人类角色则被戏称为Gus（参见游戏4设计）。

## 游戏4设计

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_298_0.png)

草图设计4.1：灯泡怪。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_298_1.png)

草图设计4.2：青蛙怪。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_299_0.png)

**草图设计4.3：机器人怪。**

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_299_1.png)

**草图设计4.4：眼睛怪。**

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_300_0.png)

**草图设计4.5：炸弹。**

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_300_1.png)

**草图设计4.6：Gus（英雄）。**

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_302_0.png)

- p1 (x-10, y-10)
- p2 (x-5, y-10)
- p3 (x-5, y-5)
- p4 (x+5, y-5)
- p5 (x+5, y-10)
- p6 (x+10, y-10)
- p7 (x+10, y-5)
- p8 (x+5, y-5)
- p9 (x+5, y+5)
- p10 (x+10, y+5)
- p11 (x+10, y+10)
- p12 (x+5, y+10)
- p13 (x+5, y+5)
- p14 (x-5, y+5)
- p15 (x-5, y+10)
- p16 (x-10, y+10)
- p17 (x-10, y+5)
- p18 (x-5, y+5)
- p19 (x-5, y-5)
- p20 (x-10, y-5)
- p21 (x-10, y-10)

渲染设计4.2：外星人2。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_302_1.png)

- p1 (x-5, y-10)
- p2 (x+5, y-10)
- p3 (x+5, y-5)
- p4 (x+10, y-5)
- p5 (x+10, y+10)
- p6 (x+5, y+10)
- p7 (x+5, y)
- p8 (x-5, y)
- p9 (x-5, y+10)
- p10 (x-5, y-5)
- p11 (x-10, y-5)
- p12 (x-5, y-5)
- p13 (x-5, y-10)

渲染设计4.3：外星人3。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_302_2.png)

- p1 (x-10, y-10)
- p2 (x+10, y-10)
- p3 (x+10, y-5)
- p4 (x+5, y-5)
- p5 (x+5, y+5)
- p6 (x+10, y+5)
- p7 (x+10, y+10)
- p8 (x+5, y+10)
- p9 (x+5, y+5)
- p10 (x-5, y+5)
- p11 (x-5, y+10)
- p12 (x-10, y+10)
- p13 (x-10, y+5)
- p14 (x-5, y+5)
- p15 (x-5, y-5)
- p16 (x-10, y-5)
- p17 (x-10, y-10)

渲染设计4.4：外星人4。

我们的英雄用一个简单的饼形表示，例如 `g.FillPie ( Brushes.Blue, player.imagePosX, player.imagePosY, player.imageWidth, player.imageHeight, 65, 50);`。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_303_0.png)

渲染设计4.5：英雄。

## 动画角色：显示角色

我们将使用一个简单的OnPaint函数来绘制我们的角色，包括飞船、武器以及所有外星飞行器。请注意我如何改变了绘图中的颜色，使它们具有独特的外观；你还应该注意到那些色彩缤纷的图案（参见示例4.44）。

### 示例4.44：绘制战斗波角色。

```csharp
// Draw the scores
buffer.ColorFill(Color.Black);
buffer.ForeColor = Color.Blue;
if(player.score < HighScore) {
    buffer.DrawText(4 * SCALE, 2*SCALE, HighScore.ToString(), false);
} else {
    buffer.DrawText(4 * SCALE, 2*SCALE, player.score.ToString(), false);
}

buffer.DrawText(16 * SCALE, 2*SCALE, player.score.ToString(), false);

if (player.isActive) {
    try {
        destination = new Rectangle(player.imagePosX, player.imagePosY,
            player.imageWidth, player.imageHeight);
        buffer.Draw(destination, PlayerDraw, DrawFlags.Wait);
        ...
for (int i = 0; i < NUM_MISSILES; i ++) {
```

