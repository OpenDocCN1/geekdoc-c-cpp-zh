

```
{
    return false;
}

// Get the value type, and check it's an integer
auto& property = itr->value;
if (!property.IsInt())
{
    return false;
}

// We have the property
outInt = property.GetInt();
return true;
}
```

然后可以在 `LoadLevel` 中使用 `GetInt` 函数来验证加载的文件版本是否与预期版本匹配：

单击此处查看代码图像

```
int version = 0;
```

```
if (!JsonHelper::GetInt(doc, "version", version) ||
    version != LevelVersion)
{
    SDL_Log("Incorrect level file version for %s", file);
    return false;
}
```

这里所指的 JSON 对象是整个文档（根 JSON 对象）。首先确保 GetInt 返回一个值，如果返回了，则检查其值是否与预期值（名为 LevelVersion 的常量）匹配。

你还可以向 JsonHelper 添加类似函数，以提取其他基本类型：GetFloat、GetBool 和 GetString。然而，此范式真正强大之处在于处理非基本类型。具体来说，此游戏中许多属性的类型为 Vector3（例如 ambientLight），因此拥有 GetVector3 函数非常有用。函数的整体构造仍然相同，只是你需要验证该属性是一个包含三个浮点数成员的数组。你可以同样声明一个 GetQuaternion 函数。

## 环境光和方向光

有了辅助函数后，你可以创建一个函数来加载全局属性。由于全局属性各不相同，未必都需要相同的类类型，因此你必须手动查询所需的特定属性。清单 14.4 中的 LoadGlobalProperties 函数演示了如何加载环境光和方向光属性。请注意，在大多数情况下，你会为这些属性调用已创建的辅助函数。

请注意，你可以通过 operator[] 直接将属性访问为 rapidjson::Value&。dirObj["directionalLight"] 调用会获取名为 directionalLight 的键的值，然后 IsObject() 调用会验证该值的类型是否为 JSON 对象。

方向光的另一个有趣模式是直接访问你想要设置的变量。在这种情况下，你不需要对 GetVector3 调用添加任何条件检查。这是因为如果请求的属性不存在，Get 函数保证不会更改变量。如果你可以直接访问变量，并且不在乎属性是否未设置，那么这可以减少代码量。

## 清单 14.4

LevelLoader::LoadGlobalProperties 实现

单击此处查看代码图像

```
void LevelLoader::LoadGlobalProperties(Game* game,
const rapidjson::Value& inObject)
{
    // Get ambient light
    Vector3 ambient;
    if (JsonHelper::GetVector3(inObject, "ambientLight", ambient))
    {
        game->GetRenderer()->SetAmbientLight(ambient);
    }

    // Get directional light
    const rapidjson::Value& dirObj = inObject["directionalLight"];
    if (dirObj.IsObject())
    {
        DirectionalLight& light = game->GetRenderer()->GetDirectionalLight();
        // Set direction/color, if they exist
        JsonHelper::GetVector3(dirObj, "direction", light.direction);
        JsonHelper::GetVector3(dirObj, "color", light.color);
    }
}
```

然后在 `LoadLevel` 中添加对 `LoadGlobalProperties` 的调用，紧跟在级别文件版本验证代码之后：

**单击此处查看代码图像**

```
// Handle any global properties
const rapidjson::Value& globals = doc["globalProperties"];
if (globals.IsObject())
{
    LoadGlobalProperties(game, globals);
}
```

然后可以在 `Game::LoadData` 中添加对 `LoadLevel` 的调用，以加载 `Level0.gplevel` 文件：

**单击此处查看代码图像**

```
LevelLoader::LoadLevel(this, "Assets/Level0.gplevel")
```

由于你现在正在从级别文件加载光照属性，因此还可以删除 `LoadData` 中硬编码环境光和方向光的代码。

## 加载角色

加载角色意味着 JSON 文件需要一个角色数组，每个角色都有该角色的属性信息。但是，你需要一种方式来指定需要哪种类型的 `Actor`（因为存在子类）。此外，你希望避免在级别加载代码中有一长串条件检查来确定要分配哪个 `Actor` 子类。

与之前一样，首先可视化数据可能的样子会有所帮助。清单 14.5 显示了在 JSON 文件中指定角色的一种方法。此示例仅显示类型为 `TargetActor` 的角色，但类型可以轻松指定任何其他 `Actor` 子类。请注意，除了类型之外，还有针对该角色的任何其他属性。此处设置的唯一属性是位置和旋转，但这些可能是角色的任何属性。

## 清单 14.5 带角色的关卡 (Level1.gplevel)

单击此处查看代码图像

```
{
    // Version and global properties
    // ...
    "actors": [
    {
        "type": "TargetActor",
        "properties": {
          "position": [1450.0, 0.0, 100.0]
        }
    },
    {
        "type": "TargetActor",
        "properties": {
          "position": [0.0, -1450.0, 200.0],
          "rotation": [0.0, 0.0, 0.7071, 0.7071]
        }
    },
    {
        "type": "TargetActor",
        "properties": {
          "position": [0.0, 1450.0, 200.0],
          "rotation": [0.0, 0.0, -0.7071, 0.7071]
        }
    }
    ]
}
```

假设你暂时拥有一种构建特定类型角色的方法，你还需要能够为角色加载属性。最简单的方法是在基类 Actor 中创建一个虚拟 LoadProperties 函数，如清单 14.6 所示。

## 清单 14.6 Actor::LoadProperties 函数

单击此处查看代码图像

```
void Actor::LoadProperties(const rapidjson::Value& inObj)
{
    // Use strings for different states
    std::string state;
    if (JsonHelper::GetString(inObj, "state", state))
    {
        if (state == "active")
        {
            SetState(EAActive);
        }
        else if (state == "paused")
        {
            SetState(EPaused);
        }
        else if (state == "dead")
        {
            SetState(EDead);
        }
    }

    // Load position, rotation, and scale, and compute
    JsonHelper::GetVector3(inObj, "position", mPosition);
    JsonHelper::GetQuaternion(inObj, "rotation", mRotation);
    JsonHelper::GetFloat(inObj, "scale", mScale);
    ComputeWorldTransform();
}
```

然后，对于 Actor 的某个子类，你可以根据需要重写 LoadProperties 函数以加载任何其他属性：

单击此处查看代码图像

```
void SomeActor::LoadProperties(const rapidjson::Value& inObj)
{
    // Load base actor properties
    Actor::LoadProperties(inObj);

    // Load any of my custom properties

    // ...

}
```

既然你有了加载属性的方法，下一步就是解决构建正确类型角色的问题。一种方法是创建一个映射，其中键是角色类型的字符串名称，值是可以动态分配该类型角色的函数。键很简单，因为它只是一个字符串。对于值，你可以创建一个静态函数来动态分配特定类型的角色。为了避免在 `Actor` 的每个子类中声明单独的函数，你可以在基类 `Actor` 中创建如下模板函数：

单击此处查看代码图像

```
template <typename T>

static Actor* Create(class Game* game, const rapidjson::Value& inObj)
{

    // Dynamically allocate actor of type T

    T* t = new T(game);

    // Call LoadProperties on new actor

    t->LoadProperties(inObj);

    return t;
}
```

由于它基于类型进行模板化，因此可以动态分配指定类型的对象，然后根据需要调用 LoadProperties 来设置该角色类型的任何参数。

然后，回到 LevelLoader，你需要创建该映射。键类型是 std::string，但对于值，你需要一个与 Actor::Create 函数签名匹配的函数。为此，你可以再次使用 std::function 辅助类来定义签名。

首先，你使用别名声明（类似于 typedef）来创建 ActorFunc 类型说明符：

单击此处查看代码图像

```
using ActorFunc = std::function<
    class Actor*(class Game*, const rapidjson::Value&)
>;
```

std::function 的模板参数指定该函数返回 Actor* 并接受两个参数：Game* 和 rapidjson::Value&。

接下来，你将映射声明为静态变量，位于

