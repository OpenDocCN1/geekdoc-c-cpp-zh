

enter、exit 和 update 方法以及每个链接推进条件方法。此状态特定的数据区域是放置计时器或计数器的便利位置。状态机通过向状态机工厂请求一个命名状态机的实例来创建。状态机工厂加载从可视状态机数据文件生成的文件，安装状态机引擎元表，并将对象返回给调用者。一旦调用者拥有此表，就可以开始更新状态机。状态机工厂的用户可以是另一个 Lua 脚本、游戏引擎 C/C++ 代码，或任何存在 Lua 接口的其他代码。一旦状态机启动，状态机的用户应以适当的周期运行 Update()。如果状态机完成，Update() 返回 Lua 值 nil，在条件语句中求值为 false。

## 把所有内容整合在一起

作为此技术的具体示例，让我们设计一个状态机来操作一把简单的枪。这把枪应该能够发射子弹、耗尽弹药、从库存中存储的弹药重新装填，并在没有更多弹药时进行空枪击发。要查看可视化设计，可以使用 UMLPad 打开随附光盘中的文件 Gun1.uss；状态机设计的快照如图 1.15.1 所示。

![](img/672fe9a2d008ba627b1991e15d70f43e_213_0.png)

图 1.15.1 描述手枪可能执行动作的简单状态机。

此状态机有一个起点（大黑点）且没有终点。启动后，状态机将立即进入 Idle 状态。由于我们重新利用了通用状态机编辑器，在填充每个状态的数据时必须小心遵循一些约定。在“活动和描述”字段中，代码生成脚本将查找特殊字符串 OnEnter、OnExit 和 OnUpdate。每个字符串之后的所有文本都将成为状态机引擎在适当时间运行的方法。这些方法将接收一个参数：state，这是一个可用于存储数据的状态特定表。如果将此精华融入你的生产流程，你可能希望修改 UMLPad 以包含每个方法的单独字段。在 Idle 状态中，只定义了一个方法：OnEnter。每次状态机引擎将状态机推进到 Idle 状态时，都会运行 OnEnter 方法。在此示例中，OnEnter 方法将 Idle 打印到屏幕上。

通过检查，我们可以看到状态机离开 Idle 状态有三种方式。推进所需的条件在每个链接上详细说明。在每个状态机更新周期中，这些条件会依次求值，一旦满足其中一个，状态机引擎就会将链接的状态设为当前状态，首先运行旧当前状态的 OnExit 方法（如果存在），然后运行新当前状态的 OnEnter 方法（如果存在）。

在这种情况下，假设 triggerDown 已变为 true，因为游戏引擎响应玩家按下射击按钮设置了该变量。Firing 状态成为当前状态。在实际实现中，Firing 的 OnEnter 方法可能会调用方法来播放枪声并在游戏世界中创建子弹实例。在下一个更新周期中，状态机发现 Firing 状态只有一个出口链接，由于没有条件，该链接会立即被跟随。

在 Recoil and Recovering 状态中，也只有一个出口链接（返回 Idle 状态），但直到计时器达到一定阈值之前都不能跟随。每个更新周期，状态机引擎运行 Recoil and Recovering 的 OnUpdate 方法，该方法按 game engine 设置的变量 frameTime 中的量增加计时器。状态的其余部分以类似方式运行。

## 数据驱动设计展示

在 Gun1.lua 上运行转换脚本 uusToState.lua 会生成一个文件 Gun1.lua，StateMachineFactory.lua 中的状态机工厂可以使用它为请求代码提供枪支状态机。脚本 testGun.lua 正是这样做的，它从 StateMachineFactory 请求一个 Gun 状态机，然后通过提供 frameTime、triggerDown 和 reloadDown 等变量来模拟游戏引擎的角色。脚本 testGun.lua 让枪经过 Idle、Fire、Recover 和 reload 状态，直到所有弹药耗尽，然后枪会陷入空转和空枪击发的无限循环。

现在是此精华的精妙之处：重新配置现有状态机以满足新的设计要求。也许设计部门希望对一种武器进行一些游戏性实验，该武器在弹药耗尽且扳机释放时会自动重新装填。为便于此操作，创建了一条从 Idle 状态到 Reload 状态的第二条链接，其条件为 not triggerDown 和 numRounds == 0，状态机现在具有所需的行为。图 1.15.2 显示了 Gun2.uss，其中包含从 Idle 到 Reload 的新链接。

![](img/672fe9a2d008ba627b1991e15d70f43e_215_0.png)

图 1.15.2 已从“Idle”创建到“Reload”状态的第二条链接，当枪支没有弹药时会跟随该链接。

比较通过 testGun.lua 运行从 Gun1.uss 和 Gun2.uss 生成的 Gun.lua（将 reloadDown 硬编码为 false）以查看新行为的效果。当枪支没有弹药时，它会重新装填，即使 reloadDown 永远不会为 true。现在假设设计部门有新需求。枪支需要有 4% 的卡壳概率，清除需要三秒钟。修改 Idle 状态，在每个 OnUpdate 周期中计算卡壳概率。当扳机按下且有可发射的子弹时，如果卡壳概率小于 0.04，状态机将卡壳状态设为新状态。在 Idle 再次成为当前状态之前，卡壳状态的计时器必须增加到三秒钟。我们只需点击几下鼠标并输入少量内容，就创建了两个新的游戏对象行为！

## 结论

希望，使用文本编辑器以外的工具来创建游戏内动作和行为的潜力能引起你的兴趣。本精华中介绍的工具和语言，虽然是开始尝试状态机代码生成的良好基础，但不如受到以下概念的启发重要：像状态机这样的系统的核心结构可以被抽象、编写和调试一次，然后由工具提供的数据和代码来启用，这些工具具有许多好处，包括系统的自文档化、快速行为修改、系统约束的强制执行，以及对系统设计师没有特定语言知识要求。

## 参考文献

- [Bignami04] Bignami, Luigi. UMLPad。可在线查阅：http://web.tiscali.it/ggb-home/umlpad/umlpad.htm。
- [Burns04] Burns, Jon 和 David Eichorn。“GDC 2004—游戏行业 Lua 圆桌会议报告”。可在线查阅：http://lua-users.org/lists/lua-l/2004-04/msg00164.html。
- [Herrington03] Herrington, Jack. 《代码生成实战》。Manning Publications，2003。
- [Jerusalimschy03a] Jerusalimschy, Roberto, L. H. de Figueiredo, 和 W. Celes，《Lua 5.0 参考手册》。技术报告 MCC-14/03，PUC-Rio，2003。可在线查阅：http://www.lua.org/manual/5.0/。
- [Jerusalimschy03b] Jerusalimschy, Roberto. 《Lua 编程》。Lua.org，2003。另可在线查阅：http://www.inf.puc-rio.br/~roberto/book/。
- [Lua04] Lua。可在线查阅：http://www.lua.org/。
- [Manzur04] Manzur, Ariel. tolua++。可在线查阅：http://www.codenix.com/~tolua/。

## 1.16

## 通用组件库

Warrick Buchanan

warrick@argonaut.com

随着计算机游戏规模和复杂性的不断增加，采用允许更结构化设计方法的技术变得越来越关键。将软件系统视为一系列可重用组件的概念并不新鲜，但在我们行业中，这仍然是一项并非总是在应该应用的地方得到应用的实践。

本精华介绍了一个可配置的 C++ 模板库，旨在简化开发可重用软件组件的过程，支持工厂、接口、接口版本控制、类型识别策略和引用计数等功能。

首先，我们将介绍库所依赖的若干基本概念，这些概念本身也很有用且可以独立使用。从这些概念出发，我们将构建组件系统的基础并演示其用法。

### 类型识别系统

库依赖于在运行时识别类类型的手段。由于实现类型识别系统有多种偏好，因此它作为库的可配置参数呈现。它是一个简单的用户定义类，至少必须以如下形式实现：

```
struct TypeID
{
    template<class Type> TypeID(const Type* type);
    int ID();

    int operator==(const TypeID& typeID) const;
    bool operator<(const TypeID& typeID) const;

    static TypeID FromName(const char* const name);
};
```

