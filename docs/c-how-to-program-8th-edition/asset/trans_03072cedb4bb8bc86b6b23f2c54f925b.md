
- 渲染 CLX
- 渲染子系统 CLXXI
- RenderWindow 类 CLXXI
- 分辨率 CLXXI
- ResourceGroupManager 类 CXCII
- 根节点 CLXXI
- 场景 CLXXI
- 场景图 CLXXI
- SceneManager 类 CLXXI
- SceneNode 类 CLXXIX
- 脚本 CLXXVIII
- Sound 类 CXCIII
- SoundManager 类 CXCII
- 镜面光 CLXI
- 聚光灯 CLXIII
- TextAreaOverlayElement 类 CLXXXIII
- 纹理 CLX
- 计时器 CLXII
- Viewport 类 CLXXIII
- 世界空间 CLXXVI
- z 顺序 CLXXXIII

## 自测练习

- **27.1** 填写下列各句中的空白：
  - a) ______ 头文件包含最常用的 Ogre 头文件。
  - b) 在调用任何其他 Ogre 函数（日志记录除外）之前，必须先创建 ______ 对象。
  - c) OgreAL 用于指向声音文件数据的主要类型是 ________。
  - d) 在 Ogre 中，使用 ______ 对象表示颜色。
  - e) ______ 头文件包含最常用的 OgreAL 头文件。
  - f) ______ 用于定义 Ogre 程序的材质和覆盖层。
  - g) ______ 对象用于为 Ogre 程序加载资源。
  - h) Ogre 使用 ______ 对象管理场景。
  - i) 3D 模型在 Ogre ______ 文件中定义。

- **27.2** 判断下列各句是否正确；如果错误，请说明原因。
  - a) 坐标 (0, 0) 指的是 OverlayContainer 的左下角。
  - b) 如果 Ogre 试图加载一个不存在的外部文件，将发生运行时错误。
  - c) Ogre 中的颜色值范围为 0 到 255。
  - d) 向 createSound 函数传递 false 值会使声音文件连续播放。
  - e) 在屏幕上绘制文本的 Overlay 必须指定绘制该文本所用的字体。
  - f) 每个 Entity 都必须具有唯一的名称。

- **27.3** 编写语句完成下列各项：
  - a) 将名为 `entityPtr` 的 Entity 指针附加到名为 `nodePtr` 的 SceneNode 指针。
  - b) 将上一题中的 Entity 缩放为原始大小的一半。
  - c) 创建循环播放 sound.wav 文件的 Sound 示例。
  - d) 如果正在按下空格键，则将 int 变量 number 的值设为 0。
  - e) 设置一个 Overlay Element，使其相对于父 Container 的大小定位。
  - f) 将 media 文件夹中名为 sounds 的文件夹添加为“General”资源位置。
  - g) 将一个 SceneNode 向左移动 15 个单位、向上移动 4 个单位，并向你的方向移动 8 个单位。

- **27.4** 找出下列各项中的错误：
  - a) `SceneNode node;`
  - b) `ColourValue(0, 0, 255);`
  - c) `Root *rootPtr = new Root();`  
    `rootPtr->initialize( true, "window" );`
  - d) `viewportPtr = sceneManagerPtr->addViewport( cameraPtr );`

## 自测练习答案

- **27.1** a) Ogre.h。b) Root。c) Sound。d) ColourValue。e) OgreAL.h。f) scripts。g) ResourceGroupManager 或 ResourceManager。h) SceneManager。i) .mesh。
- **27.2**
  - a) 错误。坐标 (0, 0) 指的是 OverlayContainer 的左上角。
  - b) 正确。
  - c) 错误。Ogre 中的颜色值范围为 0.0 到 1.0。
  - d) 错误。声音将播放一次，然后停止。
  - e) 正确。
  - f) 正确。
- **27.3**
  ```cpp
  a) nodePtr->attachObject(entityPtr);
  b) nodePtr->setScale(.5, .5, .5);
  c) soundManagerPtr->createSound("sample", "sound.wav", true);
  d) if (keyEvent.key==OIS::KC_SPACE)
         number = 0;
  e) metrics_mode_relative;
  f) ResourceGroupManager::getSingleton().addResourceLocation("media/sounds",
         "FileSystem", "General");
  g) sceneNodePtr->translate(-15, 4, 0);
  ```
- **27.4**
  - a) 变量 node 应改为声明为指向 SceneNode 的指针。Ogre 的所有 SceneNode 函数要么将指针作为参数，要么返回指针。
  - b) ColourValue 对象只能接受 0 到 1 之间的参数值。
  - c) Ogre 使用英式拼写，该函数拼写为 initialise。此外，必须在调用 initialise 之前设置渲染设置。
  - d) addViewport 是 RenderWindow 类的函数，不是 SceneManager 的函数。

## 练习

- **27.5** 查看我们的游戏编程资源中心 www.deitel.com/computergames/gameprogramming/ 以及 C++ 游戏编程资源中心 www.deitel.com/CplusplusGameProgramming/ 中可用的资源。
- **27.6** *（Pong 胜利条件）* 修改 Pong 游戏，使玩家达到 21 分时游戏结束，并显示左方或右方玩家获胜的消息。
- **27.7** *（球速增加）* 在大多数 Pong 游戏中，当两名玩家之间的回合持续很长时间时，球会开始加速，以避免僵局。修改 Pong 游戏，使球在回合中每被击中十次就加速一次。当任一玩家得分时，球应恢复原始速度。
- **27.8** *（球拍速度降低）* 有些 Pong 游戏还会调整一名或两名玩家球拍的速度，以保持游戏平衡。修改 Pong 游戏，使一名玩家领先至少 5 分时，其球拍开始减速。该玩家领先越多，其球拍移动应越慢。如果该玩家的领先优势降到 5 分以下，其球拍应恢复正常速度。
- **27.9** *（Pong 菜单）* 修改 Pong 游戏，使游戏开始前屏幕上出现一个菜单，允许玩家从几种不同的球速和球拍速度中选择。
- **27.10** *（旋转球体）* 编写一个程序，在屏幕中央绘制网格 sphere.mesh。当用户按下一个方向键时，该网格应向该方向移动十个单位。
- **27.11** *（旋转球体修改）* 修改练习 27.10 中的程序，使用户按住方向键时，球体每秒只移动一次。
- **27.12** *（贪吃蛇游戏）* 贪吃蛇游戏的目标是操控蛇在游戏区域内移动，尝试吃掉食物碎块。蛇由游戏区域内一串相邻的球体表示，游戏区域是一个二维网格。蛇可以向上、向下、向左或向右移动。如果蛇吃到一块食物（用“F”表示），它就会通过在末端增加另一个球体而变长（图 27.21）。如果蛇撞到游戏区域的墙壁（即将要超出数组范围），玩家就输了（图 27.22）。如果蛇撞到自己，玩家就输了（图 27.23）。
- **27.13** *（带障碍物的贪吃蛇）* 修改练习 27.12 中的程序，在游戏区域中添加障碍物（图 27.24）。如果蛇撞到障碍物，玩家就输了。

![](img/bfd978e7e9b192bab46ec2a89e481263_1300_0.png)

**图 27.21** | 蛇吃到食物时会变长。

![](img/bfd978e7e9b192bab46ec2a89e481263_1301_0.png)

**图 27.22** | 蛇撞到墙壁就会死亡。

![](img/bfd978e7e9b192bab46ec2a89e481263_1301_1.png)

**图 27.23** | 蛇撞到自己就会死亡。

![](img/bfd978e7e9b192bab46ec2a89e481263_1301_2.png)

**图 27.24** | 蛇撞到障碍物就会死亡。

> “我真的很喜欢《有所作为》编程练习。游戏编程[在函数章节中]让学生兴奋。”——Virginia Bailey，杰克逊州立大学

> “文本很早就介绍面向对象编程，这很好。汽车类比经过深思熟虑。对控制结构的处理极其细致。多态性章节中的虚函数图和相应解释很透彻，确实值得称赞。”——Gregory Dai，eBay 公司

> “对 C++ 的‘对象优先’讲解非常出色，同时仍便于初学者理解。以示例驱动的讲解因可选的面向对象设计案例研究而更加丰富，该案例研究将材料置于软件工程项目背景中。”——Gavin O'Brien，萨斯喀彻温应用科学与技术学院

> “很好的是，[作者们]很早就使用了 STL 和标准库。”——John Dibbling，SpryWare

> “为 C++ 所有核心方面的基础教学提供了完整基础。示例为 C++ 程序的构建提供了坚实基础。对 C++ 流式 I/O 的概述很扎实。”——Peter DePasquale，新泽西学院

> “关于因使用 = 代替 == 以及反之而导致的错误的讨论很棒！”——Wing-Ning Li，阿肯色大学

> “从面向对象角度对异常进行了全面而详细的讲解。”——Dean Mathias，犹他州立大学

> “第 20 章（数据结构）非常好。这些示例对计算机科学、信息技术、软件工程和商科学生来说都易于理解。”——Thomas J. Borrelli，罗切斯特理工学院

> “Simpletron 练习非常精彩。多态性章节以清晰的方式解释了面向对象编程中最难理解的主题之一。干得好！写作极佳，示例开发得很好，练习也很有趣。”——José Antonio González Seco，西班牙安达卢西亚议会

> “很早就引入 UML 是个好主意。”——Raymond Stephenson，微软

> “很好地使用了图表，尤其是激活调用栈和递归函数的图表。”——Amar Raheja，加州州立理工大学波莫纳分校

> “对指针的精彩讨论——我所见过的最好的。”——Anne B. Horton，洛克希德·马丁

> “对多态性以及编译器如何在‘底层’实现多态性的讲解很棒。我希望我在学生时代就能看到如此清晰的数据结构讲解。”——Ed James-Beckham，Borland

> “对查找、排序以及 Big-O 的介绍很好。”——Robert Myers，佛罗里达州立大学

> “将让你快速上手内存管理和正则表达式库。”——Ed Brey，Kohler 公司

> “对标准模板库（STL）的出色介绍。对认真学习的学生来说，这是最好的 C++ 编程书！”——Richard Albright，Goldey-Beacom 学院

> “每个代码示例都经过完整审查。这是学生学习良好编程实践的关键一步。”——Jack R. Hagemeister，华盛顿州立大学

> “我所见过的最全面的 C++ 讲解。充满涵盖整个软件开发生命周期的真实案例研究。代码示例非常出色！”——Terrell Hull，Logical Integration Solutions

