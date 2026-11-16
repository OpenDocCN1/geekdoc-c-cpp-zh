

向渲染组件请求 Entity 组件提供对象的世界位置。游戏中任何能够访问对象管理器的代码都可以查询特定对象所属的接口。只需要知道对象 ID 即可。

组件之间的第二种通信方式采用消息形式。当某个组件有话要说，但不太清楚该对谁说时，这种方式非常有用。消息可以发送给某个对象，也可以发送给所有对象。例如，当可收集组件告知其所属对象它已被拾取并希望隐藏时，它会向对象中的所有组件发布一条消息，表示希望被隐藏。每种组件类型会在初始化时告诉对象管理器它感兴趣接收哪些消息。

## 扩展我们的对象

那么，如果我们想让勺子能够弯曲，该怎么办呢？目前，我们的勺子对象是刚性的，不容易弯曲。解决方案很简单：我们给对象添加一个动画组件。

现在，我们还没有真正讨论过对象是如何定义的。在传统系统中，这部分看起来很简单：对象由它在继承树中的位置以及它向外部暴露的方法来定义。我们仍然可以为每种对象类型创建一个类，并使用聚合，使每个对象类由一堆 has-a 关系构建而成，而不是旧式的 is-a 关系。这让我们离目标更近了一步，但这仍然意味着对象是在代码中设置的，这意味着每次更改对象结构时都需要重新编译。

我们真正希望的是，对象创建的整个过程完全由数据驱动。这样一来，设计师可以在无需程序员介入的情况下，随意修改现有对象甚至创建新的对象类型。系统已经具备实现这一目标所需的一切。我们只需要推导出用于指定组件和对象的文件格式，并为设计师提供所需的工具即可。

## 创建系统

既然我们对想要的东西有了合理的构想，就可以着手创建该系统了。随书 CD-ROM 包含了基于组件的对象管理系统的所有代码，其中包括几个不同的组件和消息，可供你开始使用。它并不是一个完整的系统，考虑到所有游戏都各不相同，它也不可能是完整的，但将系统扩展到适用于各种游戏应该足够容易。

![](img/672fe9a2d008ba627b1991e15d70f43e_71_0.png)

## 组件接口

我们要查看的第一个类是组件接口。这是所有其他组件接口和组件派生的基类。它的样子如下：

```cpp
class IComponent
{
public:
    IComponent();
    virtual ~IComponent() = 0;
    virtual bool Init(CParameterNode &) = 0;
    virtual void Deinit(void) = 0;
    virtual EMessageResult HandleMessage(const CMessage &);
    virtual EComponentTypeId GetComponentTypeId(void) = 0;

    CObjectId GetObjectId(void) const;
    ICmpEntity *GetEntity() const;

private:
    void SetObjectId(CObjectId oid);
    friend CObjectManager;
    CObjectId mObjectId;
};
```

现在我们知道它长什么样了，但它有什么作用呢？让我们逐一查看每个声明。首先是构造函数和析构函数。除了虚析构函数表明该类旨在被派生而非实例化之外，它们实际上没什么作用。之后，事情变得稍微有趣一些。接下来的两个声明：

```cpp
virtual bool Init(CParameterNode &) = 0;
```

和

```cpp
virtual void Deinit(void) = 0;
```

它们分别在每个组件的初始化和反初始化时被调用。Init() 方法的唯一参数是对 CParameterNode 对象的引用。CParameterNode 是组件数据树中的一个节点。可以把它看作 XML 数据文件中的一个节点，它允许我们从该节点及其子节点读取数据，而无需进行读取 XML 通常所需的所有解析工作。然后，每个组件的 Init() 方法会从这个参数节点请求所需的数据，并相应地初始化组件。Deinit() 方法负责清理组件，确保释放组件拥有的任何内存并释放其持有的任何句柄。

下一个声明：

```cpp
virtual EMessageResult HandleMessage(const CMessage &);
```

它未被声明为纯虚函数。如果组件类不想重写它，则不必重写。其返回值是枚举类型 EMessageResult，样子如下：

```cpp
enum EMessageResult
{
    MR_FALSE,
    MR_TRUE,
    MR_IGNORED,
    MR_ERROR
};
```

其中 MR_FALSE、MR_TRUE 和 MR_ERROR 均表示消息已被处理。MR_IGNORED 表示未尝试处理该消息。IComponent 中 HandleMessage() 的实现直接返回 MR_IGNORED，不采取任何进一步操作。

下一个声明：

```cpp
virtual EComponentTypeId GetComponentTypeId(void) = 0;
```

它返回枚举类型 EComponentTypeId 的值。枚举中的条目与可实例化的组件类之间存在一对一关系。

然后是：

```cpp
CObjectId GetObjectId(void) const;
```

GetObjectId() 是一个非虚成员函数，我们添加了成员变量 mObjectId。在理想世界中，我们不会有这个成员变量，GetObjectId() 将是纯虚函数，以使 IComponent 类成为一个合适的接口。然而，在现实世界中，将 mObjectId 作为 IComponent 类的成员变量，并通过私有部分中剩下的两个声明让对象管理器能够修改它，是非常合理的：

```cpp
void SetObjectId(CObjectId oId);
friend CObjectManager;
```

如果不允许这样做，每个组件类都必须包含相同的代码来设置对象 ID，这将引入大量出错的可能性。

最后是公共方法：

```cpp
ICmpEntity *GetEntity() const;
```

这是另一个实用性比外观更重要的情况。在我们的系统中，我们决定所有对象都必须包含一个实现 ICmpEntity 接口的组件，因此我们在此添加 GetEntity() 以方便从同一对象中的任何其他组件查找该组件。ICmpEntity 类可以在随书 CD-ROM 上查看。

## 对象管理器

系统的核心是对象管理器。`CObjectManager` 类在这里过于庞大，无法逐个方法地讲解，因此我们将重点介绍核心功能。有关 `CObjectManager` 的声明和实现，请参阅随书 CD-ROM 上的代码。

对象管理器最重要的功能是数据库。它被实现为一个单独的结构体，以向用户隐藏实现细节。不过，我们这里还是来偷看一下。它如下：

```cpp
struct SObjectManagerDB
{
    // Static component type data
    SComponentTypeInfo mComponentTypeInfo[NUM_COMPONENT_TYPE_IDS];

    std::set<EComponentTypeId> mInterfaceTypeToComponentTypes[NUM_INTERFACE_TYPE_IDS];

    // Dynamic component data
    std::map<CObjectId, IComponent*> mComponentTypeToComponentMap[NUM_COMPONENT_TYPE_IDS];

    // Message data
    std::set<EComponentTypeId> mMessageTypeToComponentTypes[NUM_MESSAGE_TYPE_IDS];
};
```

`SObjectManagerDB` 的所有成员都是由更复杂的数据类型组成的普通旧式数组。它们都可以被视为二维数组，其中一个维度在编译时已知，因为我们知道组件、接口和消息类型的数量。

该结构体的前两个数据成员在系统初始化时设置，并在游戏运行期间保持不变。每种组件类型都会调用 `CObjectManager::RegisterComponentType()`，用于设置这两个数组中的数据。`SComponentTypeInfo` 包含我们创建组件所需的数据。它的样子如下：

```cpp
struct ComponentTypeInfo
{
    ComponentCreationMethod mCreationMethod;
    ComponentDestructionMethod mDestructionMethod;
    CHash mTypeHash;
};
```

创建和销毁方法成员是函数指针 typedef：

```cpp
typedef IComponent* (*ComponentCreationMethod)(void);
typedef bool (*ComponentDestructionMethod)(IComponent *);
```

我们将把具有这些签名的函数作为每个组件类的静态成员函数来创建。它们负责创建和销毁组件，

