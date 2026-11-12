

**步骤 9：** 创建鼠标悬停脚本，以便在鼠标移到每个按钮上时高亮该按钮。新建一个 JavaScript 脚本，将其命名为 InventoryButtonScript。在脚本编辑器中打开此脚本，并输入以下内容：

```javascript
var buttonReg : Texture2D;
var buttonOver : Texture2D;

function OnMouseOver () {
    guiTexture.texture = buttonOver;
}

function OnMouseExit(){
    guiTexture.texture = buttonReg;
}
```

### 为什么？

首先，我们声明两个变量，二者均为 Texture2D 类型，这只表示它们是用作纹理的图像。然后，在一段看起来应该有点熟悉的代码中，我们表示：“当鼠标位于此对象上时，转到 guiTexture 组件，并让其纹理变为 buttonOver。当我们移出此对象时，将 guiTexture 的纹理改为 buttonReg。”

此脚本将分配给每个按钮，并且对于每个按钮，我们将拖放该按钮的两种纹理版本。

- **步骤 10：** 保存并返回 Unity。修复语法问题。
- **步骤 11：** 在 Hierarchy 中将此脚本分配给 EMP、手电筒和手枪按钮。
- **步骤 12：** 通过从 Project 面板的 2D Assets 文件夹中拖动相应纹理，为每个按钮填充 Button Reg 和 Button Over 变量。例如，对于 InventoryButton_EMP，Button Reg 变量应填充 ButtonInventory-EMP 纹理（来自 Project 面板），Button Over 变量应填充 ButtonInventory-EMPText 纹理，依此类推（图 16.3）。

![](img/0285f88bc840f313779e011725b623a5_466_0.png)

**图 16.3** 按钮切换脚本的实际效果。

**步骤 13：** 播放并测试。这会有点奇怪，因为角色会四处查看，并且只有为了移到按钮上方时才会移动。

**步骤 14：** 进一步优化：让纹理不仅进行切换，还提高其 Alpha 值，使其变得更不透明；然后让它在鼠标移出时再调低 Alpha 值：

```javascript
var buttonReg : Texture2D;
var buttonOver : Texture2D;

function OnMouseOver(){
    guiTexture.texture = buttonOver;
    guiTexture.color = Color (.5,.5,.5,.5);
}

function OnMouseExit(){
    guiTexture.texture = buttonReg;
    guiTexture.color = Color (.5,.5,.5,.25);
}
```

**步骤 15：** 保存。返回 Unity 并修复任何语法问题。

**步骤 16：** 确保引擎状态已就绪。打开 AC_ToolFunctionalityScript。在脚本靠前的位置（所有变量声明中）应当有几个布尔变量。将所有布尔变量改为私有变量（我们不想在 Unity 编辑器中控制它们，而是希望由按钮来控制），并为 flashlightActive 创建一个新变量。你的变量应如下所示：

```javascript
private var flashlightActive : boolean;
private var pistolActive : boolean;
private var empActive : boolean;
private var empGhostActive : boolean;
```

### 为什么？

对于物品栏系统来说，真正重要的只有 flashlightActive、pistolActive 和 empActive。请记住，empGhostActive 是 EMP 机制的一部分。

**步骤 17：** 保存 AC_ToolFunctionalityScript。

## 脚本间通信回顾

请记住，在 AC_ToolFunctionality 脚本中，我们是在调用该脚本内的函数，而调用方式就是直接写出函数名（例如，AddHighlight(hitObj) 表示“触发带有参数 hitObj 的函数 AddHighlight，而这个函数就包含在此脚本中”）。不过，我们也可以触发其他脚本中存在的函数。我们只需要告诉 Unity 该脚本在哪里；具体来说，就是它附加在哪个对象上。

我们使用以下格式来实现：

```text
GameObject.GetComponent("name of script").NameOfFunction;
```

我们也可以用非常相似的方式发送消息来定义其中一个变量（例如布尔变量）：

```text
GameObject.GetComponent("name of script").BooleanVariable
    = true;
```

最终，我们会在物品栏脚本中同时做这两件事；我们希望 Unity 明白，当我们点击某个按钮时，它需要激活 AC_ToolFunctionality 中的某个特定布尔变量。

我们会频繁地与同一个脚本通信，因此可以通过声明一些额外变量，然后在脚本中始终引用这些变量来稍微简化操作。

**步骤 18：** 打开 InventoryButtonScript。创建一个新变量，用于存放承载我们将要引用的脚本的对象。然后让该脚本在 Awake 时找到 Main Camera：

```javascript
var buttonReg : Texture2D;
var buttonOver : Texture2D;
private var mainCamera : GameObject;

function Awake(){
    mainCamera = GameObject.Find("Main Camera");
}
```

### 为什么？

请记住，AC_ToolFunctionalityScript 附加在 Main Camera 上，而 Main Camera 是我们预制体 FPC_AegisChung 的子对象。因此，为了引用那个脚本，我们需要确保此脚本知道该对象在哪里。

现在，我们在这里冒一个经过权衡的风险。在这种情况下，我们将 var mainCamera 设为私有变量，并让 Awake 函数去找到它。这与我们一直使用的在 Unity 中手动定义公共变量的方法相反。在这种情况下，我们做出了一个相当安全的假设：场景中只会有一个名为“Main Camera”的对象。而且由于此脚本附加到三个对象上，让 Unity 在启动时去找到它对我们来说更轻松一些，因为我们无需手动填充这些变量。

**步骤 19：** 创建另一个私有变量，用于保存对实际脚本的引用；然后让该脚本也在 Awake 时被找到：

```javascript
var buttonReg : Texture2D;
var buttonOver : Texture2D;
private var mainCamera : GameObject;
private var toolFunctionality;

function Awake(){
    mainCamera = GameObject.Find("Main Camera");
    toolFunctionality = mainCamera.GetComponent("AC_ToolFunctionalityScript");
}
```

### 为什么？

请注意，这个新的私有变量没有类型。这是 JavaScript 的一个奇特现实——类型不必定义。通常它有助于提升性能，但在这种我们要访问特定脚本的情况下，可以将类型留空，这也是处理脚本时的常见做法。

**步骤 20：** 创建一个新的 OnMouseDown 函数，开始通过此脚本设置布尔变量。既然此脚本已经去查找那个脚本，就开始向它传递命令：

```javascript
...

function OnMouseDown (){
    if (name == "InventoryButton_EMP"){
        toolFunctionality.flashlightActive = false;
        toolFunctionality.pistolActive = false;
        toolFunctionality.empActive = true;
    }
    if (name == "InventoryButton_Pistol"){
        toolFunctionality.empActive = false;
        toolFunctionality.flashlightActive = false;
        toolFunctionality.pistolActive = true;
    }
    if (name == "InventoryButton_Flashlight"){
        toolFunctionality.empActive = false;
        toolFunctionality.pistolActive = false;
        toolFunctionality.flashlightActive = true;
    }
}
```

### 为什么？

这看起来像是一大段脚本，但概念相当直接。它表示：“当用户点击此对象时（函数 OnMouseDown），检查此对象的名字是否为 InventoryButton_EMP。如果是，就转到 toolFunctionality（我们刚刚将其定义为附加到 mainCamera 的组件（脚本）），并在那里将布尔变量 flashlightActive 设为 false，将布尔变量 pistolActive 设为 false，将布尔变量 empActive 设为 true。如果被点击的对象不是 InventoryButton_EMP，那么检查它是否为 InventoryButton_Pistol，如果是……”以此类推。也有更优雅的解决方案（可以看看 switch 语句或单例）；但这个方案特别容易使用。

## 在脚本中触发动画

到目前为止，我们已经让 InventoryButtonScript 能够去与 AC_ToolFunctionalityScript 中包含的迷你状态引擎通信，并开启和关闭其中包含的布尔变量。但在这真正顺畅运行之前，我们还需要对 AC_ToolFunctionalityScript 中包含的函数做一些额外的强化。

