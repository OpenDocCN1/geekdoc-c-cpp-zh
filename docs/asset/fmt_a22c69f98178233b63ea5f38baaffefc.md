
```cs
float myFloat = 1f;
switch (myFloat)
{
    case 1.0:
        //做事情
        break;
    case 20.0f:
        //做其他事情
        break;
}
```

上面的代码将产生错误：

`Assets/Switch.cs(20,1): error CS0151: 类型为 'float' 的 switch 表达式无法转换为整数类型、bool、char、string、enum 或 nullable`

在不推迟到类型章节的情况下，整数类型通常指的是像整数一样的值。字母和单词也包含在这些类型集合中。`switch` 排除了 `floats` 和 `doubles`，因为它们属于某些非整数类型。`float 1` 也可以被视为 `1.0` 或 `1.00000f`，`switch` 很难决定如何解释上述示例中的 `MyFloat` 为一个整数或一个浮点数。

## 6.7.7 我们学到了什么

`switch` 语句是强大且灵活的。通过使用贯穿（fall-through）或 `goto case` 语句的特殊条件，我们能够在 `switch` 语句内部添加额外的实用性。

仅仅因为我们可以，并不意味着我们应该使用贯穿或 `goto case`。通常，这会导致困惑且难以阅读的代码。怪异且不可理解的贯穿或 `goto case` 应该留给最怪异且不兼容的条件。为了避免养成坏习惯，最好忘记你曾见过 `goto` 语句。

既然已经发出了警告，实验和玩代码仍然很有趣。发现并解决具有唯一参数的问题是编程技能的一部分。使用奇怪且看起来异常的结构在很多方面都有帮助。如果我们能够理解一串代码，我们更有能力处理更常规的语法。

`switch` 语句可以用于任意数量的不同参数。字符串、整数和其他类型可以很容易地用于 `switch` 语句。

```cs
string s = "some condition";
switch (s)
{
    case "some condition":
        //为某些条件做事情
        break;
    case "other condition":
        //做其他事情
        break;
}
```

## 6.8 结构体 (Structs)

我们现在能够构建和操作数据了。枚举、数组和变量是有意义的。基本的逻辑流控制系统并不困惑。接下来是创建我们数据形式的能力。内置类型可能无法描述我们正在尝试的东西。

数据结构允许我们变得具体且简洁。`float`、`int` 和 `Vector3` 本身是有用的。然而，单独地复制和移动每个变量看起来可能很丑。这种缺乏组织的状态留下了更多错误的机会。

### 6.8.1 结构体

玩家角色的结构体应该包含位置、生命值、弹药、手持武器以及背包中的武器和护甲，其他相关内容应该包含在 `player.cs` 中而不应被排除。要构建一个结构体，使用类型前的 `struct` 关键字。这与声明枚举的方式非常相似。不同之处在于，我们在结构体中声明每个变量为不同的类型。

构建结构体后，你可以访问结构体的任何公共组件，使用点符号法访问生命值。例如。

```cs
public struct PlayerData {
    public Vector3 Pos;
    public int hitpoints;
    public int ammunition;
    public float RunSpeed;
}
```

## 6.8.2 结构体 vs 类 (Class)

结构体和类之间主要区别是结构体是值类型，而类是引用类型。当你将一个结构体赋值给另一个变量时，你是在创建数据的副本。当你将一个类赋值给另一个变量时，你是在复制对象的引用。

```cs
public struct PlayerData {
    public Vector3 Pos;
    public int hitpoints;
    public int ammunition;
    public float RunSpeed;
}

public class PlayerData {
    public Vector3 Pos;
    public int hitpoints;
    public int ammunition;
    public float RunSpeed;
}
```

```cs
MyClass mc2 = new MyClass();
mc2.a = mClass.a;
mc2.a = 7;
debug.Log(mc.a + " " + and + " " + mClass.a + " " + and + " " + mc2.a);
```

通过创建一个名为 `mc2` 的 `MyClass` 实例，我们可以将 `mClass.a` 的值赋值给 `mc2`，这会避免在 `mc2` 和 `mClass` 之间创建引用。上述代码输出为：

`3 and 3 and 7`

尽管我们将 `mc2` 的 `.a` 赋值给 `mClass.a`，但我们仍然丢失了 `mc2` 和 `mClass` 之间的引用。当我们将 `mc2.a` 改为 `7` 时，它对 `mc.a` 和 `mClass.a` 没有产生影响。结构体（`struct`）和类（`class`）之间的区别微妙但明显。

结构体的值在赋值给 `mStruct` 时会被复制，为了实现与类相同的行为，我们需要通过 `mc2.a = mClass.a` 分别赋值每个字段。只有通过这种方式，我们才能真正将值从 `mClass.a` 复制到 `mc2.a`，而不是引用。

## 6.8.3 不使用结构体

另一种方法是使用其他形式的数据容器，如数组。数组中的每个对象可以持有不同的类型，但必须通过其在数组中的索引号来访问。行走速度在数组中是 `4` 还是 `3` 由你来记忆。组织上的问题使得这非常容易出错并忘记哪个索引持有什么内容。

一旦你开始使用这种记录方法来处理这种类型的数据，你很可能会忘记某些内容并导致代码崩溃。世界上有些语言并没有结构体，而这是管理数据类型集合的唯一方法。感谢结构体的存在。

```csharp
public object[] PlayerDataArray;
// 使用此代码进行初始化
void Start () {
    PlayerDataArray[0] = new Vector3(0);//位置
    PlayerDataArray[1] = 10;//生命值
    PlayerDataArray[2] = 13;//弹药量
    PlayerDataArray[3] = 6.5f;//跑步速度
    PlayerDataArray[4] = 1.2f;//行走速度
}
```

当另一个生物与玩家接触时，应该给它一个存储在 `playerData` 中的整个 `PlayerData` 的副本。这将所有数据限制在一个对象中，并减少了为了传输不同数据而进行单独操作的需求。为了与类相同的操作，由于上述类和结构体赋值之间的行为，我们必须使用相同的索引同时复制每个参数。

## 6.8.4 处理结构体

我们将从 Unity 3D 中的 `Struct` 项目开始。在这个项目中，我们有一个包含立方体和一个附带的 `Struct.cs` 组件的场景。结构体最适合包含特定对象的数据集合。如果我们想为立方体设置一组简单的参数，可能会使用以下结构体：

```csharp
struct BoxParameters{
    public float width;
    public float height;
    public float depth;
    public Color color;
}
// 使用这个新结构体并将其命名为 myParameters
BoxParameters myParameters;
```

将此结构体添加到 Unity 3D 场景上的新类中，我们拥有了一个使用单个对象存储和移动数据集合的系统。在这个对象内部，我们为宽度、高度、深度和颜色分配了公共变量。

要使用它，我们可以使用点操作符在结构体内单独调整每个参数。

```csharp
// 使用此代码进行初始化
void Start()
{
    myParameters.width = 2;
    myParameters.height = 3;
    myParameters.depth = 4;
    myParameters.color = new Color(1,0,0,1);
}
```

在 `Start()` 函数中，我们可以访问 `myParameters` 变量并为其赋值。一旦为 `BoxParameters myParameters` 赋值了值，我们就可以作为变量传递给函数。

```csharp
void UpdateCube(BoxParameters box)
{
    Vector3 size = new Vector3(box.width, box.height, box.depth);
    gameObject.transform.localScale = size;
    gameObject.renderer.material.color = box.color;
}
```

新函数允许通过点访问器传递给它的 `BoxParameters` 并暴露赋值给它的值；它是一个运算符，但不限于访问器，还包括属性、函数以及所有的结构体和类成员。第一语句创建了一个新的 `Vector3 size`。然后将大小赋值给它，其中我们提取了宽度、高度和深度并将值赋值给 `Vector3` 的 `x`、`y`、`z` 参数。一旦 `Vector3` 创建完成，我们将值赋值给 `gameObject.transform.localScale`。之后，我们还可以通过将 `renderer.material.color` 赋值为来自 `BoxParameters` 的值来改变 `gameObject` 的颜色。

将这两者结合，我们可以在 `gameObject` 的 `Update()` 函数中进行一些有趣的操作。

```csharp
void Update()
{
    float h = (100 * Math.Sin(Time.fixedTime))/10;
    myParameters.height = h;
    UpdateCube(myParameters);
}
```

在这里我们使用了一些简单的数学计算 `((100 * Math.Sin(Time.fixedTime))/10)`，并将该值赋值给 `float h`。然后我们只需要更新结构体中的一个变量就可以更新整个游戏对象。

## 6.8.5 访问结构体

现在我们有了结构体。通过将变量组合在一起，我们减少了需要传递给函数的参数数量。如果结构体局限于创建它的类，它就是 `BoxParameters`。通过将结构体移动到类外部，它变得全局可用以完成相同的任务。

```csharp
using UnityEngine;
using System.Collections;
// 在开放区域定义
struct BoxParameters
{
    public float width;
    public float height;
    public float depth;
    public Color color;
}

public class Struct : MonoBehaviour
{
    public BoxParameters myParameters;
    // 使用此代码进行初始化
    void Start ()
    {
        myParameters.width = 2;
        myParameters.height = 3;
        myParameters.depth = 4;
        myParameters.color = new Color(1,0,0,1);
    }
    void UpdateCube(BoxParameters box)
    {
        Vector3 size = new Vector3(box.width, box.height, box.depth);
        gameObject.transform.localScale = size;
        gameObject.renderer.material.color = box.color;
    }
    void Update()
    {
        float h = (100 * Math.Sin(Time.fixedTime))/10;
        myParameters.height = h;
        UpdateCube(myParameters);
    }
}
```

创建一个新类 `UseStruct` 并将其添加到场景中的主摄像机（Main Camera）。

```csharp
using UnityEngine;
using System.Collections;
public class UseStruct : MonoBehaviour
{
    BoxParameters ThatBox;
    // 使用全局可用的 BoxParameters 结构体！
    void Start ()
    {
        // 每帧调用一次
    }
    void Update ()
    {
        ThatBox = GameObject.Find("Cube").GetComponent<Struct>().myParameters;
        gameObject.transform.position = new Vector3(0, ThatBox.height+0.5f, -10);
    }
}
```

新的类是 `BoxParameters` 结构体，因为它没有局限于 `Struct` 类内部。`myParameters` 应该设为公共以便在 `Struct` 类之外访问。我们可以将 `UseStruct` 的 `ThatBox` 赋值给立方体的 `Struct.myparameters`。通过对 `ThatBox.height` 的巧妙使用，我们可以让摄像机跟随场景中立方体的缩放，如下：

```csharp
gameObject.transform.position = new Vector3(0, ThatBox.height*0.5f, -10);
```

## 6.8.6 全局访问

在实践中，为你的全局访问结构体和枚举设置一个中心位置是一个好主意。项目中的第三个类 `Globals.cs` 可以包含以下代码：

```csharp
using UnityEngine;
using System.Collections;
public struct BoxParameters
{
    public float width;
    public float height;
    public float depth;
    public Color color;
}
```

通过这种简单的结构，我们能够为所有全局可访问的信息创建一个中心位置。从简单的 `public struct BoxParameters` 开始，我们可以继续向全局可访问数据中添加越来越多的有用的信息。每个 C# 脚本都需要声明一个类（`class`）。虽然这很常见，但并不是严格强制的。像 `Globals.cs` 这样的工具文件非常有用，它们可以提供一个整洁的系统，团队中的每个程序员都能找到可以在场景中不同对象之间共享的方便结构。

## 6.8.7 我们学到了什么

在第 6.8.6 节中，我们讨论了全局访问。这个概念并不新。当你编写一个类时（在本例中是 `Struct` 结构），它可以被任何其他类访问。因此，当我们将 `UseStruct` 赋值给场景中的主摄像（Main Camera）时，它能够使用 `Struct`。

## 6.9 类数据

由于计算机管理内存的方式，使用结构体（`struct`）优于类（`class`）。在不详细的情况下，内存的一部分被称为堆（heap），另一部分被称为栈（stack）。通常，栈是分配给游戏的一部分较小、组织更有条且速度更快的内存。堆通常更大，且访问时间比栈更长。

值可以分配到栈上，而结构体是一种值类型；因此，访问栈比访问类更快。虽然结构体和其他值类型的使用方式可能禁用了它们在栈上的分配，但它们会进入堆中。类和其他引用数据类型无论如何都存储在堆中。

在一个简单的函数中，出现的变量都会被推入栈中。一旦函数执行完成，函数内部创建的所有临时变量在函数执行完毕后会立即被销毁。

```csharp
void DoThings()
{
    int[] arrayOfInts = new int[100];
    for (int i = 0; i < 100 ; i++)
    {
        arrayOfInts[i] = 0;
    }
}
```

`DoThings()` 函数几乎什么都没做，但创建了一个被添加到栈中的 `int` 数组。一旦这个函数完成，该 `int` 数组就会被清除。通常，栈收缩得非常快。被添加到栈的第二个对象是 `int i`，它在循环内部使用。

类相对于结构体的主要优势是增加了构造函数（`constructor`）和类继承（`class inheritance`）。除此之外，你可以在创建时为类中的每个变量添加赋值。

```csharp
struct MyStruct
{
    public int a = 0;
    public MyStruct()
    {
    }
}
class MyClass
{
    public int a = 0;
    public MyClass()
    {
    }
}
```

上述代码产生了以下错误：

`Assets/ClassVStruct.cs(7,28): error CS0573: 'ClassVStruct.MyStruct.a': Struct体不能有实例字段初始化器`

`Assets/ClassVStruct.cs(8,24): error CS0568: Struct体不能包含显式的无参数构造函数`

在结构体中，不允许给字段赋值。因此，`public a = 0;` 只在类中允许。默认值只在类中允许。同样，构造函数 `public MyStruct()` 是不允许的，但在类中是允许的。
