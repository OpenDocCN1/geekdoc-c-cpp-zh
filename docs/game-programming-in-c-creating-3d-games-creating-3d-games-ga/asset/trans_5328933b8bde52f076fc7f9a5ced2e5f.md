

云层和地面层。如果云层滚动速度比地面层慢，就会给人一种云层比地面更远的印象。传统动画已使用这种技术近一个世纪，并且它很有效。通常，只需要三层就能创建可信的视差效果，如图 2.5 所示。当然，更多层会为效果增加更多深度。

![](img/e9afcec1487716b0ef80d7e7c09869c8_162_0.png)

图 2.5 将太空场景分解为三层，以便实现视差滚动

要实现视差效果，请将多个 BGSpriteComponents 附加到单个 actor 上并指定不同的绘制顺序值。然后，您可以为每个背景使用不同的滚动速度来完成效果。

## 游戏项目

遗憾的是，您尚未学习足够多的新主题来制作具有比第 1 章“游戏编程概述”中创建的 Pong 克隆游戏明显更复杂机制的游戏。仅将精灵添加到上一章的游戏中也不会特别有趣。因此，与其做一个完整的游戏，本章的游戏项目演示了本章涵盖的新技术。代码可在本书的 GitHub 仓库中找到，位于 Chapter02 目录。在 Windows 上打开 Chapter02-windows.sln，在 Mac 上打开 Chapter02-mac.xcodeproj。图 2.6 展示了游戏项目的实际运行效果。Jacob Zinman-Jeanes 创建了精灵图像，这些图像根据 CC BY 许可证授权。

![](img/e9afcec1487716b0ef80d7e7c09869c8_164_0.png)

图 2.6 横向卷轴项目的实际运行效果

代码包括混合 `Actor/Component` 模型、`SpriteComponent`、`AnimSpriteComponent` 和视差滚动的实现。它还包括一个名为 `Ship` 的 `Actor` 子类。`Ship` 类包含两个速度变量，分别用于控制左右速度和上下速度。清单 2.9 显示了 `Ship` 的声明。

## 清单 2.9 Ship 声明

单击此处查看代码图像

```cpp
class Ship : public Actor
{
public:
    Ship(class Game* game);

    void UpdateActor(float deltaTime) override;

    void ProcessKeyboard(const uint8_t* state);

    float GetRightSpeed() const { return mRightSpeed; }

    float GetDownSpeed() const { return mDownSpeed; }

private:

    float mRightSpeed;

    float mDownSpeed;
};
```

Ship 构造函数将 mRightSpeed 和 mDownSpeed 初始化为 0，并创建一个附加到船上的 AnimSpriteComponent，关联相关纹理：

单击此处查看代码图像

```cpp
AnimSpriteComponent* asc = new AnimSpriteComponent(this);

std::vector<SDL_Texture*> anims = {

    game->GetTexture("Assets/Ship01.png"),

    game->GetTexture("Assets/Ship02.png"),

    game->GetTexture("Assets/Ship03.png"),

    game->GetTexture("Assets/Ship04.png"),

};

asc->SetAnimTextures(anims);
```

键盘输入直接影响船的速度。游戏使用 W 和 S 键使船上下移动，使用 A 和 D 键使船左右移动。ProcessKeyboard 函数接收这些输入并适当更新 mRightSpeed 和 mDownSpeed。

Ship::UpdateActor 函数实现了船的移动，使用与第 1 章所示类似的技术：

单击此处查看代码图像

```cpp
void Ship::UpdateActor(float deltaTime)
{
    Actor::UpdateActor(deltaTime);

    // Update position based on speeds and delta time
    Vector2 pos = GetPosition();

    pos.x += mRightSpeed * deltaTime;
    pos.y += mDownSpeed * deltaTime;

    // Restrict position to left half of screen
    // ...

    SetPosition(pos);
}
```

移动是游戏中如此常见的功能，以至于将其实现为组件（而不是在 `UpdateActor` 函数中）非常合理。第 3 章“向量和基础物理”讨论了如何创建 `MoveComponent` 类。

背景是一个通用的 `Actor`（不是子类），它拥有两个 `BGSpriteComponent`。这两个背景不同的滚动速度创建了视差效果。所有这些 actor（包括船）都在 `Game::LoadData` 函数中创建。

## 摘要

表示游戏对象有多种方式。最简单的方法是使用单体层次结构，所有游戏对象都继承自一个基类，但这可能会迅速变得难以管理。使用基于组件的模型，您可以根据游戏对象包含的组件来定义其功能。本书采用混合方法，具有浅层的游戏对象层次结构，但组件实现了一些行为，例如绘制和移动。

最早的游戏使用 2D 图形。虽然当今许多游戏是 3D 的，但 2D 游戏仍然非常流行。精灵是任何 2D 游戏的主要视觉构建块，无论是否有动画。SDL 通过简单的接口支持加载和绘制纹理。

许多 2D 游戏实现了翻页动画，通过快速连续绘制不同图像来使精灵看起来在动画。您可以使用其他技术实现滚动背景层，并可以使用视差效果来创造深度的错觉。

## 补充阅读

Jason Gregory 用几页篇幅介绍了不同类型的游戏对象模型，包括 Naughty Dog 使用的模型。Michael Dickheiser 的书包含一篇关于实现纯组件模型的文章。

Dickheiser, Michael, Ed. Game Programming Gems 6. Boston: Charles River Media, 2006.

Gregory, Jason. Game Engine Architecture, 2nd edition. Boca Raton: CRC Press, 2014.

## 练习

本章的第一个练习是关于不同类型游戏对象模型的思想实验。在第二个练习中，您将向 **AnimSpriteComponent** 类添加功能。最后一个练习涉及添加对 **tile maps** 的支持，这是一种从瓦片生成 2D 场景的技术。

## 练习 2.1

考虑一个动物野生动物园游戏，玩家可以开着不同的车辆在野外观察动物。思考这样一个游戏中可能存在的不同类型的生物、植物和车辆。您如何在单体类层次结构对象模型中实现这些对象？

现在考虑同一个游戏，但使用基于组件的游戏对象模型实现。您如何实现这一点？这两种方法中，哪一种对这个游戏似乎更有益？

## 练习 2.2

`AnimSpriteComponent` 类目前仅支持单个动画，由向量中的所有精灵组成。修改该类以支持多个不同的动画。将每个动画定义为向量中纹理的一个范围。使用 `Chapter02/Assets` 目录中的 `CharacterXX.png` 文件进行测试。

现在添加对非循环动画的支持。在将动画定义为纹理范围时，还允许指定循环或非循环。当非循环动画结束时，它不应回绕到初始纹理。

## 练习 2.3

生成 2D 场景的一种方法是通过瓦片地图。在这种方法中，一个图像文件（称为 **tile set**）包含一系列大小统一的瓦片。许多这样的瓦片组合形成一个 2D 场景。Tiled (http://www.mapeditor.org) 是一个用于生成瓦片集和瓦片地图的优秀程序，它为本练习生成了瓦片地图。**图 2.7** 说明了瓦片集的一部分是什么样子。

![](img/e9afcec1487716b0ef80d7e7c09869c8_170_0.png)

**图 2.7** 练习 2-3 使用的瓦片集的一部分

在此示例中，瓦片地图存储在 CSV 文件中。使用 `Chapter02/Assets` 目录中的 `MapLayerX.csv` 文件，其中有三个不同的图层（图层 1 最近，图层 3 最远）。`Tiles.png` 包含瓦片集。CSV 文件中的每一行包含一系列数字，如下所示：

```
-1,0,5,5,5,5
```

-1 表示该瓦片没有图像（因此您不应为该瓦片渲染任何内容）。其他每个数字都引用瓦片集中的特定瓦片。编号从左到右，然后从上到下。因此，在此瓦片集中，瓦片 8 是第二行最左侧的瓦片。

创建一个名为 TileMapComponent 的新组件，它继承自 SpriteComponent。此类需要一个函数来加载和读取瓦片地图 CSV 文件。然后重写 Draw 以从瓦片集纹理绘制每个瓦片。为了仅绘制纹理的一部分而不是整个纹理，请使用 SDL_RenderCopyEx 的 srcrect 参数。这样可以仅从瓦片集纹理绘制单个瓦片正方形，而不是整个瓦片集。

