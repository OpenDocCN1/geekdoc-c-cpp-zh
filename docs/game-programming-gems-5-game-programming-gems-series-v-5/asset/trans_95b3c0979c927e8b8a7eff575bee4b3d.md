

仅此而已。只需少量代码，就能快速轻松地将游戏引擎的功能暴露给 Lua。还有许多更复杂的方法可以将 Lua 与 C 链接，但它们超出了本入门概述的范围。Lua 也不局限于与 C 的集成。像 LuaBind 这样的工具也可用于帮助在 Lua 与 C++ 类之间建立关系。

## 将 Lua 嵌入游戏

既然我们了解了如何在游戏引擎和 Lua 之间创建链接，现在来探讨如何将 Lua 嵌入游戏。

## 创建和销毁状态

要在游戏中使用 Lua，必须先创建一个 Lua 状态，然后加载并执行 Lua 代码块。Lua 状态的创建方式如下：

```
lua_State *luaState = lua_open();
```

当我们准备关闭游戏时，关闭状态：

```
lua_close(luaState)
```

这将释放解释器使用的所有内存，并触发对已加载到状态中的代码的任何剩余垃圾回收。

## 加载和执行代码

一旦 Lua 初始化完成，并且我们已像之前所示注册了新函数，就可以开始加载和执行 Lua 代码了。Lua 支持从任意来源向解释器提供数据。在本示例中，我们将使用一些从文件和字符串获取输入的 Lua 辅助例程。从磁盘执行脚本可以使用：

```
lua_dofile(luaState, "LuaScriptFile.lua");
```

这将编译并执行脚本（如果存在任何执行点）。如果文件仅包含函数定义，则所有函数都将被定义并添加到 Lua 状态中，但不会执行任何实际代码。

同样，文本字符串中的 Lua 代码可以使用以下方式执行：

```
lua_dostring(luaState, "a=14; b=7;");
```

如你所料，使用 Lua 创建交互式命令控制台只需几行简单代码。

Lua 脚本加载的一个非常有趣的特性是，这些例程可以接受文本脚本或预翻译的二进制 Lua 代码。Lua 发行版附带一个名为 luac 的预翻译器，可将脚本编译为二进制形式。完成此操作后，应用程序可以选择省略 Lua 的词法分析器和解析器组件，从而使代码开销更小。这还为开发人员提供了选择：将一些脚本保留为原始文本形式以供修改，而将其他脚本编译，从而隐藏起来不被窥探。

```
lua_loadfile(luaState, "LuaScriptFile.lua");
```

## 从 C 调用 Lua 函数

如前所示，将脚本加载到 Lua 中但不立即执行任何代码，而是在稍后再执行，这通常很有用。一个很好的例子是游戏实体逻辑的脚本化。每个实体类在启动时可能会加载一个定义其游戏内行为的 Lua 脚本。可能有用于设置、移动和渲染的单独 Lua 例程。一个简单的 Lua 实体的 Lua 代码可能如下所示：

```
-- functions for fictional "walker" entity
function WalkerSetup(walker)
    -- our poor walker only lives for 1 minute
    timer = 60.0;
end;

function WalkerMove(walker, elapsedSec)
    timer = timer - elapsedSec;
    if (timer > 0.0) then
        Walker.DoAI(walker);
        Walker.UpdateControls(walker);
        Walker.DoPhysics(walker, elapsedSec);
        Walker.UpdateAccelAndPos(walker, elapsedSec);
    end;

    else
        Walker.Destroy(walker);
    end;
end;

function WalkerRender(walker)
    visible = Walker.GetVisibility(walker)
    if (visible == 1) then
        matrix = Walker.GetMatrix(walker);
        Game.SetModelMatrix(matrix);
        Game.RenderModel(Walker.GetModel(walker));
    end;
end;
```

当实体类初始化时，它可以使用 lua_loadfile() 来读取和编译脚本。然后，实体的 C 代码可以在游戏循环中根据需要调用 Lua 脚本例程。从 C 调用特定的 Lua 函数涉及将函数以及所有参数推入通信堆栈，然后调用 lua_call()。

调用 walker 的 Move() 例程的示例如下：

```
-- call this entity's Move script
lua_getglobal(luaState, "WalkerMove");
lua_pushlightuserdata(luaState, this);
lua_pushnumber(luaState, elapsedSec);
lua_call(luaState, 2, 0);
```

第一个调用将名为 "WalkerMove" 的全局值推入堆栈。该值恰好是我们在初始化 walker 类时加载的脚本中的一个函数。

下一个调用将我们 C++ 实体的 this 指针推入通信堆栈以供 Lua 使用。实际上，Lua 不会使用这个值，因为它完全不理解我们的 C++ 对象。相反，它会将此值直接传回给 C 胶水函数，以便它们知道使用哪个对象指针。要推入我们的 this 指针，我们调用了 lua_pushlightuserdata()。“轻量用户数据”是一种特殊的 Lua 数据类型，当 C 代码需要向 Lua 提供其本身不理解的数据时可以使用它。大多数时候，如本示例所示，轻量用户数据用于保存指向 C/C++ 对象和结构的指针。

接下来，我们只需调用 lua_pushnumber() 来推入自上一帧以来经过的秒数。现在函数和所有参数都已正确放在堆栈上，我们可以通过调用以下方式执行 Lua 代码：

```
lua_call(luaState, 2, 0);
```

第二个参数（2）告诉 Lua 堆栈上推入了多少个参数，第三个参数（0）告诉我们期望返回多少个返回值。Lua 将执行整个函数，在返回时，通信堆栈将包含我们期望的任何返回值。

现在我们可以从 Lua 调用 C 函数，也可以从 C 调用 Lua 函数。我们离让游戏支持 Lua 又近了一步……或者真的如此吗？

### 实时注意事项

请注意，当我们使用 lua_dofile() 加载并执行一个代码块，或使用 lua_call() 调用 Lua 脚本中的函数时，调用不会在请求的 Lua 脚本处理完毕之前返回。这对于某些应用程序和架构可能没问题，但在许多游戏中这不够。我们需要能够随时间安排事件。

### 基于时间的示例

比如说，我们想使用 Lua 来脚本化火山喷发时摄像机的移动。我们可以在每一帧调用 Lua 脚本中的 moveCamera() 函数，该 Lua 函数会在内部更新计时器，并在计时器触发新的摄像机状态时调用不同的子函数。然而，这很混乱，我们更喜欢一个简单的线性脚本，看起来类似这样：

```
-- script to trigger volcano eruption
-- every 20 minutes throughout the entire game

function EruptSequence()
    -- start shaking the camera gently for 10 seconds
    Camera.SetShakeMag(0.002);
    Script.WaitSeconds(10);

    -- suspend player control
    Game.SuspendPlayer();
    -- set the camera to slowly orbit the volcano
    entTarget = Entity.FindByName("Volcano");
    Camera.SetMode(CMX_ORBIT);
    Camera.SetTargetEnt(entTarget);
    Camera.SetOrbitRate(0.500);
    Camera.SetOrbitTiltRate(0.003);
    -- and jack up the shaking!
    Camera.SetShakeMag(0.01);
    Script.WaitSeconds(5);

    -- ok, after 5 seconds ease up on the shake
    Camera.SetBankShakeMag(0.002);
    -- and put the camera back in the player's eyes
    entPlayer = Entity.FindByName("Player");
    Camera.SetTargetEnt(entPlayer);
    Camera.SetMode(CMX_FIRSTPERSON);
    Game.ResumePlayer();
    Script.WaitSeconds(10);

    -- after 10 seconds, turn shake off all together
    Camera.SetShakeMag(0.0);
end

-- This is the first executable code in the script;
-- an implied main(), if you will
-- Run the erupt sequence every 20 minutes
while (1) do
    Script.WaitSeconds(20 * 60);
    EruptSequence();
end
```

这段代码首先定义了一个处理摄像机序列的函数。然后，脚本每隔 20 分钟重复调用该函数。我们使用一个名为 Script.WaitSeconds() 的新注册例程来安排各种事件，它只是简单地延迟给定的时间。

这在理论上很有效，但如果执行 Lua 代码不会在代码完成之前返回，我们怎么能期望运行实际的游戏循环呢？答案在于我们对 Script.WaitSeconds() 函数的实现，以及一种名为协程（coroutines）的 Lua 特性。

