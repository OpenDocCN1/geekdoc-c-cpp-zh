
`memory-model := persistence.`

`pers |= memory-model.`

`ui |== memory-model.`

`backend |= memory-model.`

## URIs 与进程内 REST

REST 模型和持久化存储的底层架构模型是进程内 REST（In-Process REST），它是 REST 架构风格在应用程序内部的适配。所有实体都通过承担 URI 角色的标识符进行引用；在 Wunderlist 中，这些是 `WObject` 类的实例，它们编码了实体类型、容器 ID 和对象 ID。容器是闭包对象的 ID，例如，任务所属列表的 ID。并非所有对象都有显式的容器；例如，列表或登录用户直接就是根对象。示例 17.2 显示了几个以字符串 URI 形式表示的 `WObjectReference`。

## 示例 17.2 内部 URI

```
task://container/2/id/3

list://id/2/

task://container/2/

task://id/3
```

URI 是结构化的。例如，示例 17.2 中的第一个 URI 指向 ID 为 2 的列表内 ID 为 3 的任务。第 2 个 URI 是 ID 为 2 的列表对象。该 URI 仅指向 ID 为 3 的任务，而没有提供列表 ID。在我们目前的实现中，这需要在所有列表中搜索该任务。

存储被组织为一系列对象，这些对象就像微型 Web 服务器，不同之处它们不使用 HTTP 协议进行通信，而是使用示例 17.3 所示的普通 Objective-C 消息协议。如你所见，消息大致对应 GET、PUT 和 DELETE 动词，唯一的不同在于我们通常讨论的是对象数组，而不是一次处理单个对象。

## 示例 17.3 存储协议

```
@protocol WLStorage <NSObject>

(NSArray*)objectsForReference: (WLObjectReference*) ref;

-(void)removeObjectsForReference: (WLObjectReference*) ref;

-(void)setObjects:(NSArray*)new forReference: (WLObjectReference*) ref;

end
```
