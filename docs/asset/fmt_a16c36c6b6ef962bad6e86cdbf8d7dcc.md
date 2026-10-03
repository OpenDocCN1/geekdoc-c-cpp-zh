
此示例从 `Dictionaries` 项目开始。打开场景，我们将看到一个挂载了 `Dictionaries` 组件的 `Main Camera`。

```csharp
using UnityEngine;
using System.Collections;
// 字典的新命名空间
using System.Collections.Generic;
public class Dictionaries : MonoBehaviour
{
    // 声明一个名为 MyDictionary 的字典
    Dictionary<string,int> MyDictionary;
    // 使用此进行初始化
    void Start ()
    {
        MyDictionary = new Dictionary<string,int>();
        MyDictionary.Add("Zombies",10);
        Debug.Log(MyDictionary["Zombies"]);
    }
}
```

我们需要添加一个新的命名空间 `System.Collections.Generic`，它其中包含了 `Dictionary` 数据类型。我们可以使用多种方法，但最常用的方法之一是 `Dictionary<string,int>` 组合。这允许我们使用字符串来查找字典中的值。字典声明的结构为 `<第一个类型, 第二类型>`，其中你调用的第一个类型是键（key），第二个类型是与该键关联的值（value）。键（即第一个值）在整个字典中必须是唯一的。

```csharp
MyDictionary = new Dictionary<string,int>();
MyDictionary.Add("Zombies",10);
MyDictionary.Add("Zombies",7);
```

如果我们尝试使用上述代码，将得到以下错误：`ArgumentException: An element with the same key already exists in the dictionary.`

当使用字典时，键是用于查找与第二个类型关联关系的值。因此，在上面的代码中，如果你请求 `"Zombies"`，字典将无法告诉你是 10 还是 7。

要向字典添加条目，我们使用 `MyDictionary.Add("Zombies",10);` 将带有值的字符串推入变量中。要检索它们，我们使用类似于访问数组的方式。

```csharp
MyDictionary = new Dictionary<string,int>();
MyDictionary.Add("Zombies",10);
Debug.Log(MyDictionary["Zombies"]);
```

`Dictionary["Zombies"]` 在使用 `.Add()` 状态赋值值时充当了索引的作用。我们也可以在字典中使用不同的类型。

```csharp
Dictionary<int, Object> obj = new Dictionary<int, Object>();
Object[] allObjects = GameObject.FindObjectsOfType(typeof(Object)) as Object[];
for(int i = 0; i < allObjects.Length; i++) {
```

```csharp
obs.Add(i, allObjects[i]);
Debug.Log(obs[i]);
}
```

上述代码将打印出场景中找到的 `Object`。`obs[i]` 这一行代码就足够使用 `int` 提取场景中找到的对象。为了让这更清晰，我们可以使用以下三条语句：

```csharp
Debug.Log(obs[1]);
Debug.Log(obs[2]);
Debug.Log(obs[3]);
```

此代码会在 `Console` 面板中产生以下消息：

```
Main Camera (UnityEngine.AudioListener)
UnityEngine.Debug:Log(Object)
MyDictionary:Start() (at Assets/Dictionary.cs:19)
Main Camera (UnityEngine.FlareLayer)
UnityEngine.Debug:Log(Object)
MyDictionary:Start() (at Assets/Dictionary.cs:20)
Main Camera (UnityEngine.GUILayer)
UnityEngine.Debug:Log(Object)
MyDictionary:Start() (at Assets/Dictionary.cs:21)
```

`obs[1]` 是 `Main CameraAudioListener`，它本身并不重要，重要的是我们目前引用它的方式。字典 `obs` 是一个数组，我们使用 `int` 来访问它。在字典的每个条目中，我们都有一个关联的对象。

# 高级

# 569

栈（Stack）基本上是一个数组，你可以在脑海中将其想象成一堆书。栈顶是所有函数执行操作的地方。将对象推入栈中（Push）是在栈的顶部加载另一个对象。查看栈顶（Peek）意味着查看栈顶书籍的内容。从栈中弹出（Pop）意味着从栈中取出顶部的元素；不弹出书在逻辑上毫无意义。

## 7.19.3.1 基础示例

我们将继续使用第 7.19.2 节中的项目，该项目包含了一些我们希望在场景中继续使用的功能。此类挂载在主摄像（`Main Camera`）上。

```csharp
public GameObject[] Stack;
// 使用此进行初始化
void Start()
{
    GameObject[] go = GameObject.FindObjectsOfType(typeof(GameObject)) as GameObject[];
    // 创建新栈
    Stack<GameObject> objectStack = new Stack<GameObject>();
    // 使用 push 将对象推入栈
    foreach (GameObject go in go)
    {
        objectStack.Push(go);
    }
    // 初始化类作用域 ObjectStack
    // 以在检查面板中查看
    ObjectStack = new GameObject[objectStack.Count];
    // 将栈拷贝到 Unity 数组中
    objectStack.CopyTo(ObjectStack, 0);
}
```

在这里使用栈是有意义的；然而，`Push()` 函数使得代码变得非常易读。使用栈来清晰性和易用性的主要优点是，栈能够清楚地显示正在发生什么以及数据流向哪里。

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_590_0.png)

# 使用 Unity 3D 学习 C# 编程

栈的结果可能意义不大。`FindObjectsOfType` 函数的顺序并不保证任何特定的顺序。然而，知道栈底元素是第一个找到的对象，而栈顶元素是最后一个找到的，这是有趣的。为了更好地利用栈，可以使用触发器（Trigger）。为了测试这一点，我们将在场景中添加一个胶囊碰撞体（`Capsule Collider`）并挂载一个刚体（`Rigidbody`）组件。

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_591_0.png)

胶囊碰撞体的设置应开启 `"Trigger On"`，然后我们需要一个刚体，其中关闭重力（Gravity）并开启其位置和旋转的约束（constraint）。这将我们的对象在场景中更易处理。

在 `Start()` 中，我们将初始化一个新的栈，以便在胶囊碰到场景中的另一个对象时使用。我们将使用数组在编辑器的检查面板（`Inspector panel`）中显示。这将使栈的操作更加可见。

```csharp
using UnityEngine;
using System.Collections.Generic;
public class CollisionStack : MonoBehaviour {
    // 存储栈和数组
    public GameObject[] HitList;
    public Stack<GameObject> HitStack;
    void Start ()
    {
        HitStack = new Stack<GameObject>();
    }
    void OnTriggerEnter(Collider other)
    {
        if (!HitStack.Contains(other.gameObject))
        {
            HitStack.Push(other.gameObject);
            HitList = new GameObject[HitStack.Count];
            HitStack.CopyTo(HitList, 0);
        }
    }
}
```

我们需要查看的代码包含在 `OnTriggerEnter()` 函数中。如果该语句完成了两件事，我们可以使用传入参数 `other` 以及它挂载的 `gameObject` 碰撞器。栈有一个名为 `Contains()` 的成员函数，可以在其中使用 `other.gameObject` 检查整个栈中它是否已经添加。如果没有，我们将使用 `Push()` 将其放入栈的 `gameObject` 组件。

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_592_0.png)

启动游戏并移动胶囊，碰到场景中的物体。栈会将碰到的对象添加到 `HitList` 的顶部。每当调用 `OnTriggerEnter` 时，`Hitlist` 重新初始化其内容到 `Hitlist`，以便在检查面板中查看。

当然，这并不是唯一的方法。在诸如塔防游戏中，你可以根据对象在栈中的顺序对它们进行优先级排序。当新对象到达并添加到栈中时，你可以对栈顶对象进行人工关注。

```csharp
void Update() {
    if(HitStack.Count > 0) {
        GameObject lastObject = HitStack.Peek() as GameObject;
        Debug.DrawLine(transform.position, lastObject.transform.position);
    }
}
```

如果在 `Update()` 函数中添加一个简单的检查，我们可以用它来从胶囊到最后添加到栈的物体之间画一条线。要从栈中取出对象，我们需要使用类型转换（cast）。

栈是一个泛型容器。它中的所有内容都存储为 `object`。这并不意味着任何数据丢失；它只是以泛型方式存储。

`Peek()` 函数用于在栈上观察添加到栈中的对象。语句 `lastObject = HitStack.Peek() as GameObject;` 将数据从 `HitStack.Peek()` 的结果赋值给 `lastObject`。在赋值之后，我们就可以使用 `lastObject.transform.position`。

要从栈中移除对象，我们需要使用 `Pop()` 函数。

`img/05ac639a69dd6f0bc68ebaed1d4ca9f7_593`

# 594

## 7.19.4 队列 (Queues)

队列的工作方式与栈类似，但有一些修改。队列与栈的区别在于对象的添加顺序。当你将对象添加到队列时，它位于队列末尾。当你移除对象时，它是最早进入的。这种行为被称为先进先出（First-In-First-Out）。

队列也是一个泛型容器。其中的所有内容都存储为 `object`。这并不意味着任何数据丢失；它只是以泛型方式存储。

`Enqueue()` 函数用于将对象添加到末尾。`Dequeue()` 函数用于移除并返回队列头部的对象。`Peek()` 函数用于观察队列头部的对象而不移除它。在本示例中，我们将使用队列来管理胶囊接触的对象。

```csharp
public class CollisionQueue : MonoBehaviour {
    // 存储队列和数组
    public GameObject[] HitList;
    public Queue<GameObject> HitQueue;
    void Start ()
    {
        HitQueue = new Queue<GameObject>();
    }
    void OnTriggerEnter(Collider other)
    {
        if (!HitQueue.Contains(other.gameObject))
        {
            HitQueue.Enqueue(other.gameObject);
            HitList = new GameObject[HitQueue.Count];
            HitQueue.CopyTo(HitList, 0);
        }
    }
}
```

我们需要查看的代码包含在 `OnTriggerEnter()` 函数中。如果该语句完成了两件事，我们可以使用传入参数 `other` 以及它挂载的 `gameObject` 碰撞器。队列有一个名为 `Contains()` 的成员函数，可以在其中使用 `other.gameObject` 检查整个栈中它是否已经添加。如果没有，我们将使用 `Enqueue()` 将其放入栈的组件中。

启动游戏并移动胶囊，碰到场景中的物体。队列会将碰到的对象添加到 `HitList` 的末尾。每当调用 `OnTriggerEnter` 时，`Hitlist` 重新初始化其内容到 `Hitlist`，以便在检查面板中查看。

```csharp
void Update() {
    if(HitQueue.Count > 0) {
        GameObject firstObject = HitQueue.Peek() as GameObject;
        Debug.DrawLine(transform.position, firstObject.transform.position);
    }
}
```

如果在 `Update()` 函数中添加一个简单的检查，我们可以用它从胶囊到最后添加到栈的物体之间画一条线。要从栈中取出对象，我们需要使用类型转换。

```csharp
IEnumerator dequeueQueue() {
    yield return WaitForSeconds(2);
    if (HitQueue.Count > 0)
    {
        HitQueue.Dequeue();
        HitList = new GameObject[HitQueue.Count];
        HitQueue.CopyTo(HitList, 0);
        StopCoroutine("dequeueQueue");
    }
}
```

# 使用 Unity3D 学习 C# 编程

![](img/05ac639a69dd6f0bc68ebaed1d4ca9f7_595_0.png)

如果这是一个类似武器塔的东西，我们可能会向移动缓慢的僵尸发射导弹或机枪。用于添加到队列（queue）或栈（stack）的系统可以是任何内容，`pop()` 和 `Dequeue()` 函数也是如此。它们可以根据需要被调用，例如当栈顶对象或队列底对象被销毁时作为事件被调用。

## 7.19.5 我们学到了什么

组织和引用数据是编程的一个重要部分。因此，编程的很大工作是收集、组织和重新组织数据；在你自己的代码中已经有许多可以使用的此类机制。

学习 C# 的每一个系统并不是我们的目标。重要的是记住，某些系统在很多情况下可能很有用。当你开始记住它们时，可以查阅它们是如何使用的。

学习任何语言最重要的部分在于，存在诸如 queue（队列）、stack（栈）和 dictionary（字典）这样的词汇，它们管理数据的方式不同。当你遇到类似需要处理的事项列表时，你应该查阅什么系统最能满足你当时的需求。

一次性学习一切是不可能的。记住任何编程语言拥有的半部分功能就很了。不重要的是去互联网上查找它们，并通过阅读一些示例来记住它们是如何使用的。

最好的办法是观察这些结构在这里是如何被使用的。当你自己工作并遇到看起来熟悉的东西时，好主意是回想一下你学过的内容以作为复习。将这些发现应用到你当前的任务中。

## 7.20 回调 (Callbacks)

简单来说，回调（callback）是在另一个函数完成其工作后执行的函数。当我们开始某项工作并想知道它何时完成时，通常会使用回调。当我们在关卡中开始生成怪物并想知道所有怪物何时生成完毕时，可以使用。

除非两个对象同时存在场景中，否则无法在它们之间建立引用。当我们在一个场景中的对象依赖于另一个即将加载的场景中的对象时，就会变成一个问题。使用这种加载顺序，如果有一个事件（比如我们刚刚决定的事件）在场景完成时触发，将会很有用。

管理函数何时以及如何被调用，简单来说就是设置委托（delegate），在任务完成后调用它。当任务完成时，委托被调用，然后执行任何分配的函数。这个概念是启动一个特定任务的函数，并让该函数意识到在任务完成后有其他函数需要被调用。

### 7.20.1 基础示例

在 `Callback` 项目中，我们在一个球体上挂载了 `SimpleCallback.cs`。以下代码只有几个函数，可以让你入门。
