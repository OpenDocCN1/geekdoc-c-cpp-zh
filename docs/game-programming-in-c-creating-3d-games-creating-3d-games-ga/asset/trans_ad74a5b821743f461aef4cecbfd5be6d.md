

## C++ 游戏编程
### 创建 3D 游戏
Sanjay Madhav
### Addison-Wesley

波士顿 • 哥伦布 • 印第安纳波利斯 • 纽约 • 旧金山
阿姆斯特丹 • 开普敦 • 迪拜 • 伦敦 • 马德里 • 米兰
慕尼黑 • 巴黎 • 蒙特利尔 • 多伦多 • 德里 • 墨西哥城 • 圣保罗 • 悉尼 • 香港 • 首尔 • 新加坡 • 台北 • 东京

制造商和销售商用于区分其产品的许多名称均声称为商标。当这些名称出现在本书中，且出版商知晓商标主张时，这些名称已按首字母大写或全大写形式印刷。

作者和出版商在编写本书时已尽力，但不做任何明示或暗示的担保，也不对任何错误或遗漏承担责任。对于与使用本书所含信息或程序相关或由此产生的偶然或后果性损害，概不承担责任。

关于批量购买本书或特殊销售机会（可能包括电子版本；定制封面设计；以及特定于您的业务、培训目标、营销重点或品牌兴趣的内容）的信息，请联系我们的企业销售部，电子邮件 corpsales@pearsoned.com 或电话 (800) 382-3419。

政府销售咨询，请联系 governmentsales@pearsoned.com。

关于美国境外销售的问题，请联系 intlcs@pearson.com。

访问我们的网站：informit.com/aw

国会图书馆控制号：2017964125

版权所有 © 2018 Pearson Education, Inc.

版权所有。在美国印刷。本出版物受版权保护，任何禁止的复制、存储在检索系统中或以任何形式或任何方式（电子、机械、复印、录制或其他）传播，均必须事先获得出版商的许可。有关权限、请求表格以及 Pearson Education 全球权利与许可部门内相应联系人的信息，请访问 www.pearsoned.com/permissions/。

Overwatch™ 是 Blizzard Entertainment, Inc. 在美国和/或其他国家的商标。

Call of Duty® 是 Activision Publishing, Inc. 的注册商标。

Uncharted™ 和 Horizon: Zero Dawn™ 是 Sony Interactive Entertainment LLC 的商标，God of War® 是其注册商标。

Visual Studio®、Xbox® 和 Windows® 是 Microsoft Corporation 的注册商标。

Apple®、iOS®、Mac®、macOS® 和 Xcode® 是 Apple Inc. 的注册商标。

GitHub® 是 GitHub, Inc. 的注册商标。

OpenGL® 和椭圆徽标是 Silicon Graphics, Inc. 在美国和/或全球其他国家的商标或注册商标。

Linux® 是 Linus Torvalds 的注册商标。

FMOD® 是 Firelight Technologies Pty, Ltd. 的注册商标。

Pac-Man® 是 Bandai Namco Entertainment Inc. 的注册商标。

Asteroids® 和 Pong® 是 Atari Interactive Inc. 的注册商标。

PlayStation® 是 Sony Interactive Entertainment Inc. 的注册商标。

Android® 是 Google Inc. 的注册商标。

Unreal® 是 Epic Games, Inc. 在美国及其他地区的商标或注册商标。

Unity® 是 Unity Technologies 的注册商标。

Maya® 和 FBX® 是 Autodesk, Inc. 在美国及其他国家的注册商标。

Skyrim® 是 ZeniMax Media Inc. 的注册商标。

Planet Coaster® 是 Frontier Developments Plc. 的注册商标。

ISBN-13: 978-0-13-459720-1

ISBN-10: 0-13-459720-6

1 18

### 总编辑
Mark Taub

### 执行编辑
Laura Lewin

### 开发编辑
Michael Thurston

### 管理编辑
Sandra Schroeder

### 技术编辑
Josh Glazer
Brian Overland
Matt Whiting

### 高级项目编辑
Lori Lyons

### 制作经理
Dhayanidhi Karunanidhi

### 文稿编辑
Kitty Wilson

### 索引编制人
Lisa Stumpf

### 校对员
Larry Sulky

### 编辑助理
Courtney Martin

### 封面设计师
Chuti Prasertsith

### 排版人员
codemantra

致我的家人和朋友：感谢支持。

## 章节概览
- 前言
- 致谢
- 作者简介
- 1 游戏编程概述
- 2 游戏对象与 2D 图形
- 3 向量与基础物理
- 4 人工智能
- 5 OpenGL
- 6 3D 图形
- 7 音频
- 8 输入系统
- 9 摄像机
- 10 碰撞检测
- 11 用户界面
- 12 骨骼动画
- 13 中级图形
- 14 关卡文件与二进制数据
- A 中级 C++ 复习
- 索引

在 InformIT 网站上注册您的 C++ 游戏编程副本，以便在更新和更正发布时方便地获取。要开始注册流程，请访问 informit.com/register 并登录或创建帐户。输入产品 ISBN 9780134597201 并点击 Submit。在“已注册产品”选项卡中查找该产品旁边的“访问奖励内容”链接，并按照该链接访问任何可用的奖励材料。如果您希望收到新版本和更新的独家优惠通知，请勾选接收我们电子邮件的方框。

## 目录
- 前言
- 致谢
- 作者简介
- 1 游戏编程概述
  - 设置开发环境
    - Microsoft Windows
    - Apple macOS
  - 获取本书源代码
  - 超越 C++ 标准库
  - 游戏循环与 Game 类
  - 帧结构
  - 实现骨架 Game 类
  - Main 函数
  - 基础输入处理
  - 基础 2D 图形
    - 颜色缓冲区
    - 双缓冲
    - 实现基础 2D 图形
  - 绘制墙壁、球和挡板
  - 更新游戏
    - 实时与游戏时间
    - 作为增量时间函数的逻辑
    - 更新挡板位置
    - 更新球的位置
  - 游戏项目
  - 总结
  - 建议阅读
  - 练习
    - 练习 1.1
    - 练习 1.2
- 2 游戏对象与 2D 图形
  - 游戏对象
    - 游戏对象类型
    - 游戏对象模型
    - 将游戏对象集成到游戏循环中
  - 精灵
    - 加载图像文件
    - 绘制精灵
    - 精灵动画
  - 滚动背景
  - 游戏项目
  - 总结
  - 建议阅读
  - 练习
    - 练习 2.1
    - 练习 2.2
    - 练习 2.3
- 3 向量与基础物理
  - 向量
    - 获取两点之间的向量：减法
    - 缩放向量：标量乘法
    - 组合两个向量：加法
    - 确定距离：长度
    - 确定方向：单位向量与归一化
    - 从角度转换为前向量
    - 将前向量转换为角度：反正切
    - 确定两个向量之间的角度：点积
    - 计算法线：叉积
  - 基础移动
    - 创建基础 `MoveComponent` 类
    - 创建 `InputComponent` 类
  - 牛顿物理
    - 线性力学概述
    - 使用欧拉积分计算位置
    - 可变时间步长的问题
  - 基础碰撞检测
    - 圆与圆相交
    - 创建 `CircleComponent` 子类
  - 游戏项目
  - 总结
  - 建议阅读
  - 练习
    - 练习 3.1
    - 练习 3.2
    - 练习 3.3
- 4 人工智能
  - 状态机行为
    - 设计状态机
    - 基础状态机实现
    - 作为类的状态
  - 路径查找
    - 图
    - 广度优先搜索
    - 启发式
    - 贪婪最佳优先搜索
    - A* 搜索
    - Dijkstra 算法
    - 跟随路径
    - 其他图表示
  - 游戏树
    - 极小极大算法
    - 处理不完整的游戏树
    - Alpha-Beta 剪枝
  - 游戏项目
  - 总结
  - 建议阅读
  - 练习
    - 练习 4.1
    - 练习 4.2
- 5 OpenGL

