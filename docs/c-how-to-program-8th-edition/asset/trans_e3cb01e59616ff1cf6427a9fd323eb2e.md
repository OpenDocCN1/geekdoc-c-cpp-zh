
## 代码示例

www.blender.org/download/get-blender/  
Blender 下载页面。

www.ogre3d.org/wiki/index.php/CodeSnippets#HOWTO  
《Ogre Cookbook》包含代码示例，解释如何完成与几何体、渲染、材质、纹理、动画、输入 GUI 和声音相关的各种任务。

www.ogre3d.org/phpBB2/viewtopic.php?t=27326  
《Asteroid Wars》是一款使用 Ogre 实现图形效果的游戏。源代码可获取。

www.ogre3d.org/phpBB2/viewtopic.php?t=27806  
五款使用 Ogre 编写的游戏。所有游戏的源代码均可获取。

## 书籍

www.amazon.com/Pro-OGRE-3D-Programming/dp/1590597109/ref=pd_bbs_sr_1/102-2583408-2260151?ie=UTF8&s=books&qid=1173888297&sr=1-1  
《Pro OGRE 3D Programming》，作者 Gregory Junker。

## 论坛

www.ogre3d.org/phpBB2/viewtopic.php?t=5706  
一篇论坛帖子，介绍如何在 Debian GNU/Linux 上安装 Ogre。

www.ogre3d.org/phpBB2/viewforum.php?f=2  
Ogre 帮助论坛。在使用 Ogre 时遇到任何问题，都可以向 Ogre 用户寻求帮助。

www.ogre3d.org/phpBB2/  
Ogre 网站上的多个论坛，包括帮助、Ogre 实践应用、内容创作、编程基础等。

www.ogre3d.org/phpBB2addons/  
Ogre 附加组件论坛。多个论坛专门讨论较受欢迎的 Ogre 附加组件，包括 OgreAL、OgreODE、NxOgre、PyOgre 等。

www.ogre3d.org/phpBB2addons/viewforum.php?f=10  
Ogre 网站上的 OgreAL 论坛。提供有关安装和使用 OgreAL 的信息。寻求帮助的好地方。

www.wreckedgames.com/forum/viewforum.php?f=6&sid=dc5f903554a80ac5194213329f5e46e4  
OIS 论坛。获取有关使用 OIS 的帮助。

## 小结

## 第 27.3 节 游戏编程基础

- 3D 图形引擎隐藏了使用图形 API 所需的繁琐而复杂的编程。
- Ogre 支持 Direct3D 和 OpenGL 图形 API，并可在 Windows、Linux 和 Mac 平台上运行。
- Ogre 严格来说是一个图形渲染引擎。Ogre 社区已经制作了许多附加组件，使用户可以将其他库与 Ogre 集成，以支持那些功能。
- 3D 模型是可在屏幕上绘制的对象的计算机表示。
- 材质通过设置光照属性、颜色和纹理来确定对象的外观。
- 纹理是包裹在模型上的图像。

实体的最终大小。这些函数还会按相同比例缩放 SceneNode 的所有子节点。要改变这一点，请调用 `setInheritScale` 函数并向其传入 `false`。

- `setPosition` 函数将节点放置在场景中的给定坐标处。
- Ogre 使用材质脚本创建材质。将文件保存为 `.material` 扩展名的文件。一个材质文件可以定义多个材质；每个材质都必须具有唯一名称。
- Overlay 由保存在 `.overlay` 文件中的脚本定义。单个 `.overlay` 文件可以包含多个 Overlay 定义。Overlay 中的每个对象都有三个主要属性——度量模式、位置和大小。
- Overlay 由 OverlayElement 组成。Overlay 中的第一个元素必须是 OverlayContainer。OverlayContainer 可以容纳任何 OverlayElement。TextAreaOverlayElement 用于保存文本。调用 show 函数将 Overlay 显示在屏幕上。
- 使用 TextAreaOverlayElement 显示文本。调用 `setCaption` 更改屏幕上的文本。
- z 顺序较高的 Overlay 将渲染在 z 顺序较低的 Overlay 之上。
- 字体由 fontdef 文件中的脚本定义。
- 使用 OverlayManager 类的静态成员函数 `getSingleton` 获取 OverlayManager 对象。

### 第 27.4.4 节 动画与计时器

- `translate` 函数移动 SceneNode。
- 默认情况下，SceneNode 的平移在父空间中完成。父空间中的平移是相对于父节点的原点进行的。世界空间中的平移是相对于场景原点 (0, 0, 0) 进行的。局部空间中的平移是相对于节点原点进行的。
- FrameListener 处理 `Ogre::FrameEvents`。FrameEvent 在帧开始或结束时发生。

### 第 27.4.5 节 用户输入

- Ogre 不直接支持来自键盘、鼠标或操纵杆等设备的用户输入。
- 使用面向对象输入系统（OIS）处理用户输入。
- InputManager 用于创建各种输入设备。要创建 InputManager，我们必须为其提供一个用于收集输入的窗口。
- Keyboard 对象收集 KeyEvent 事件并将其发送给 KeyListener。
- OIS 定义了键盘上所有按键的枚举，我们用它来确定按下了哪个键。

### 第 27.4.6 节 碰撞检测

- `getPosition` 返回一个 Vector3，表示节点相对于其父节点的位置；`_getDerivedPosition` 返回相对于原点的位置。
- SceneManager 可以根据节点创建时赋予的名称，检索场景图中的任意节点。
- Ball 的方向由 Vector3 确定。x 值为正表示 Ball 将沿 x 轴向右移动，x 值为负表示 Ball 将向左移动。如果 Ball 正在向右移动，将其 x 值乘以 −1 会改变符号并反转方向。
- 有完整的库专门用于处理碰撞和物理。

### 第 27.4.7 节 声音

- OgreAL 是 OpenAL 音频库的封装。该封装允许我们通过将声音附加到场景图中的节点，将声音功能集成到 Ogre 代码中。
- 我们必须使用预处理器指令来包含 `OgreAL.h` 头文件。
- Sound 是包含声音数据的 OgreAL 对象。使用 `SoundManager` 类的 `createSound` 函数创建声音。只能有一个 `SoundManager`。
- `createSound` 函数接受三个参数。第一个是 `Ogre::String`，将作为 Sound 在 OgreAL 系统中的名称。第二个是与该声音关联的声音文件名。第三个是 bool，用于确定是否应循环播放该 Sound 以继续播放。传入 false 会将 Sound 完整播放一次，然后停止。传入 true 会连续循环播放声音，直到你停止它。
- 使用 `attachObject` 函数将 Sound 附加到节点。
- 每个 Sound 都必须具有唯一名称。
- Sound 必须播放完毕后才能再次播放。

### 第 27.4.8 节 资源

- 所有资源都必须在使用前加载。
- 使用 `ResourceGroupManager` 管理游戏的资源。
- `addResourceLocation` 函数接受三个 `Ogre::String` 参数。第一个是资源的位置。第二个是资源所在文件的类型。第三个是这些文件所属的资源组。

### 第 27.4.9 节 Pong 驱动程序

- Ogre 支持多种平台，因此应尽量避免编写平台特定的代码。

## 术语

| 术语 | 参考页码 | 术语 | 参考页码 |
|---|---|---|---|
| 3D 图形引擎 | CLIX | KeyListener 类 | CLXXXVII |
| 3D 模型 | CLX | 细节层次（LoD） | CLXI |
| 3D 建模工具 | CLX | Light 类 | CLXXIII |
| 3D 声音 | CLXII | 局部空间 | CLXXXVI |
| alpha 通道 | CLX | 材质 | CLIX |
| 环境光 | CLXI | 网格 | CLXXIV |
| Camera 类 | CLXXIII | 度量模式 | CLXXXIII |
| 碰撞检测 | CLXI | 法线 | CLXXIX |
| 颜色 | CLX | 面向对象输入系统（OIS） | CLXXXVI |
| 色深 | CLXXI | Ogre（面向对象的图形渲染引擎） | CLIX |
| 剔除 | CLXXII | OgreAL | CLXIII |
| 漫射光 | CLXI | OpenAL 音频库 | CXCIII |
| Direct3D | CLX | OpenGL | CLX |
| 定向光 | CLXXIII | Overlay 类 | CLXXXIII |
| 自发光 | CLXI | OverlayContainer 类 | CLXXXIII |
| Entity 类 | CLXXIV | PanelOverlayElement 类 | CLXXXIII |
| 导出 3D 模型 | CLX | 父空间 | CLXXXVI |
| 帧 | CLXII | 像素模式 | CLXXXIII |
| FrameEvent 类 | CLXXXVI | 点光源 | CLXIII |
| FrameListener 类 | CLXXXVI | 相对模式 | CLXXXIII |
| Keyboard 类 | CLXXXVII |  |  |
| KeyEvent 类 | CLXXXVII |  |  |
