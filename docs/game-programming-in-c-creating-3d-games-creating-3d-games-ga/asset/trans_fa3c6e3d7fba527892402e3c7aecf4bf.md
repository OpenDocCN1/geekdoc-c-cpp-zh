

## sComponentFactoryMap:

单击此处查看代码图像

```cpp
std::unordered_map<std::string, std::pair<int, Compon
LevelLoader::sComponentFactoryMap
{
    { "AudioComponent",
        { Component::TAudioComponent, &Component::Create
    },
    { "BallMove",
        { Component::TBallMove, &Component::Create<BallW
    },
    // Other components omitted
    // ...
};
```

然后，您在 LevelLoader 中实现一个名为 LoadComponents 的帮助函数，如清单 14.10 所示。与 LoadActors 类似，它接收一个要加载的组件数组并遍历该数组。然后，您使用 sComponentFactoryMap 查找组件类型。如果找到了，则检查该角色是否已拥有该类型的组件。iter->second.first 访问值对的第一个元素，该元素对应类型 ID。如果角色没有请求类型的组件，则使用值对第二个元素中存储的函数（iter->second.second）创建一个组件。如果组件已存在，则可以直接在其上调用 LoadProperties。

### 清单 14.10 LevelLoader::LoadComponents 实现

单击此处查看代码图像

```cpp
void LevelLoader::LoadComponents(Actor* actor,
    const rapidjson::Value& inArray)
{
    // Loop through array of components
    for (rapidjson::SizeType i = 0; i < inArray.Size())
    {
        const rapidjson::Value& compObj = inArray[i];
        if (compObj.IsObject())
        {
            // Get the type
            std::string type;
            if (JsonHelper::GetString(compObj, "type", t
            {
                auto iter = sComponentFactoryMap.find(typeId);
                if (iter != sComponentFactoryMap.end())
                {
                    // Get the typeid of component
                    Component::TypeID tid = static_cast<Co
                    (iter->second.first);
                    // Does the actor already have a compo
                    Component* comp = actor->GetComponent(
                    if (comp == nullptr)
                    {
                        // It's a new component, call funct
                        comp = iter->second.second(actor, c
                    }
                    else
                    {
                        // It already exists, just load pro
                        comp->LoadProperties(compObj["prope
                    }
                }
                else
                {
                    SDL_Log("Unknown component type %s", t
                }
            }
        }
    }
}
```

最后，您在 `LoadActors` 中添加代码，如果存在 `components` 属性，则访问该属性并在其上调用 `LoadComponents`：

单击此处查看代码图像

```cpp
// Construct with function stored in map
Actor* actor = iter->second(game, actorObj["propertie
// Get the actor's components
if (actorObj.HasMember("components"))
{
    const rapidjson::Value& components = actorObj["cor
    if (components.IsArray())
    {
        LoadComponents(actor, components);
    }
}
}
}
```

所有这些代码就位后，您现在可以从文件加载整个关卡，包括全局属性、角色以及每个角色关联的任何组件。

## 保存关卡文件

从概念上讲，保存到关卡文件比从文件加载更简单。首先，您编写关卡的全局属性。然后，您遍历游戏中的每个角色以及每个角色附加的每个组件。对于每个这样的项，您需要写出相关属性。

实现细节有些复杂，因为 RapidJSON 接口用于创建 JSON 文件比读取文件稍微复杂一些。但是，总体上，您可以使用类似于加载关卡文件时所用的技术。

首先，您在 JsonHelper 中创建辅助 Add 函数，以便可以快速将其他属性添加到现有 JSON 对象。例如，AddInt 函数的语法如下：

单击此处查看代码图像

```cpp
void JsonHelper::AddInt(rapidjson::Document::Allocato
rapidjson::Value& inObject, const char* name, int
{
    rapidjson::Value v(value);
    inObject.AddMember(rapidjson::StringRef(name), v,
}
```

最后三个参数与 GetInt 函数的参数相同，只是 Value 现在不是 const。第一个参数是 RapidJSON 在需要分配内存时使用的分配器。每次调用 AddMember 都需要一个分配器，因此您必须传入一个。您可以直接从 Document 对象获取默认分配器，但如果需要，也可以使用其他分配器。然后，您创建一个 Value 对象来封装整数，并使用 AddMember 函数将带有指定名称的值添加到 inObject。

其余 Add 函数类似，但 AddVector3 和 AddQuaternion 除外，对于这两个函数，您必须先创建一个数组，然后向该数组添加浮点值。（您在查看全局属性时会看到这种数组语法。）

然后，您为 LevelLoader::SaveLevel 函数创建一个骨架，如清单 14.11 所示。首先，您创建 RapidJSON 文档并通过 SetObject 为其根创建一个对象。接下来，您添加版本整数。然后，您使用 StringBuffer 和 PrettyWriter 创建 JSON 文件的格式化输出字符串。最后，您使用标准 std::ofstream 将字符串写入文件。

### 清单 14.11 LevelLoader::SaveLevel 实现

单击此处查看代码图像

```cpp
void LevelLoader::SaveLevel(Game* game,
    const std::string& fileName)
{
    // Create the document and root object
    rapidjson::Document doc;
    doc.SetObject();

    // Write the version
    JsonHelper::AddInt(doc.GetAllocator(), doc, "versi

    // Create the rest of the file (TODO)
    // ...

    // Save JSON to string buffer
    rapidjson::StringBuffer buffer;

    // Use PrettyWriter for pretty output (otherwise t
    rapidjson::PrettyWriter<rapidjson::StringBuffer> w
    doc.Accept(writer);

    const char* output = buffer.GetString();

    // Write output to file
    std::ofstream outFile(fileName);

    if (outFile.is_open())
    {
        outFile << output;
    }
}
```

目前，此函数仅将版本写入输出文件。但有了这个骨架代码，您可以开始添加其余输出。

### 保存全局属性

接下来，您需要向 `LevelLoader` 添加一个 `SaveGlobalProperties` 函数。此处我们省略其实现，因为它与迄今编写的其他函数非常相似。您只需添加环境光和方向光对象的属性即可。

完成此函数后，您按如下方式将其集成到 SaveLevel 函数中：

单击此处查看代码图像

```cpp
rapidjson::Value globals(rapidjson::kObjectType);
SaveGlobalProperties(doc.GetAllocator(), game, global
doc.AddMember("globalProperties", globals, doc.GetAll
```

### 保存角色和组件

为了能够保存角色和组件，您需要一种方法，给定 Actor 或 Component 指针，获取类型的字符串名称。您已经为组件拥有了 TypeID，因此要获取相应的字符串，您只需在 Component 中声明一个不同名称的常量数组。您在 Component.h 中按如下方式声明此数组：

单击此处查看代码图像

```cpp
static const char* TypeNames[NUM_COMPONENT_TYPES];
```

然后在 Component.cpp 中，您填充该数组。重要的是，您要保持与 TypeID 枚举相同的顺序：

单击此处查看代码图像

```cpp
const char* Component::TypeNames[NUM_COMPONENT_TYPES] = {
    "Component",
    "AudioComponent",
    "BallMove",
    // Rest omitted
    // ...
};
```

通过保持顺序，您可以轻松地根据类型获取组件的名称，使用类似下面的代码片段：

单击此处查看代码图像

```cpp
Component* comp = /* points to something */;
const char* name = Component::TypeNames[comp->GetTypeID()];
```

要为 Actor 及其子类执行相同的操作，您还需要向 Actor 添加一个 TypeID 枚举。这基本上与本章前面组件中的 TypeID 代码相同，因此此处省略。

然后，您需要在 Actor 和 Component 中创建一个虚拟 SaveProperties 函数，并在每个需要这样做的子类中重写它。这最终与加载关卡文件时编写的 LoadProperties 函数非常相似。例如，清单 14.12 显示了 Actor::SaveProperties 的实现。请注意，您大量使用了 LevelLoader 中的 Add 函数，并且需要传入分配器，因为所有 Add 函数都需要它。

### 清单 14.12 Actor::SaveProperties 实现

单击此处查看代码图像

```cpp
void Actor::SaveProperties(rapidjson::Document::AllocatorType& allocator,
    rapidjson::Value& inObj) const
{
    std::string state = "active";
    if (mState == EPaused)
    {
        state = "paused";
    }
    else if (mState == EDead)
    {
        state = "dead";
    }
}
```

