
无论我们是否在文档模型中工作，现在都可以通过类似下面的单次调用访问持久化存储特定的参数：

```
NSString *value = [[self preferences] valueForKey:@"exampleKey1"];
```

我们也可以通过类似下面的调用设置它们：

```
[[self preferences] setValue:@"someValue" forKey:@"someKey"];
```

在这两个示例中，我们直接在 DocumentPreferences 对象上调用 -valueForKey: 和 -setValue:forKey:，而无需担心该值是否存在。如果它不存在，我们将收到 nil。如果它已设置为默认值，我们将取回该默认值；如果我们已覆盖默认值或先前设置了该属性，则将返回该属性值。

最后，与 NSUserDefaults 类似，默认值不会持久化到磁盘。因此，我们每次初始化 DocumentPreferences 时都需要设置它们：

下载 CDPreferences/MyDocument.m

```
NSMutableDictionary *defaults = [NSMutableDictionary dictionary];
[defaults setValue:[NSNumber numberWithBool:YES] forKey:@"default1"];
[defaults setValue:@"DefaultValue2" forKey:@"default2"];
[defaults setValue:@"DefaultValue3" forKey:@"default3"];
[_preferences setDefaults:defaults];
```

但是，我们不必担心以后更改默认值。如果我们在后续版本中更改默认值，只要用户尚未覆盖它们，它们就会自动更新。

## 索引

### A

- 访问模式，112–113
- add: 方法（NSArrayController），26, 29
- addImage: 方法，31
- addObserver:forKeyPath: 方法，39
- addPersistentStoreWithType: 方法，90, 152
- 地址簿应用程序，16
- allObjects 实现（DistributedCDServer），214
- allParameterNames 实现（CDPreferences），236
- allParameters 实现（CDPreferences），235
- AppDelegate 对象
  - 添加到 xib 文件，22
  - 图像路径，在头文件中，30
- applicationDidFinishLaunching: 方法，212, 220
- applicationDidFinishLaunching: 方法，122
- applicationShouldTerminate: 方法，122
- associateObject:parent: 方法，181
- 原子存储，98
- 属性特性（数据模型），18
- 属性检查器，44
- 数据类实体的属性，144
- NSManagedObject 对象的属性，52–54
  - 原始访问，53
- 自动数据迁移，88–90
  - 开启，78
- awakeFromFetch: 方法，重写，59
- awakeFromInsert: 方法，重写，59

### B

- 二进制数据，存储位置，99
- 二进制存储，97, 98, 189
- Bonjour，207, 210
- 广播服务（分布式 Core Data），210–212
- 按钮，26

### C

- 缓存数据，110
- 计算值，存储，103
- 级联选项（删除规则），19
- CDPreferences 应用程序
  - 构建，230–237
  - DocumentPreferences 对象，230–236
    - allParameterNames，236
    - allParameters，235
    - createParameter:，235
    - findParameter:，233
    - setValue:forUndefinedKey:，234, 236
    - valueForUndefinedKey:，232, 236
- 客户端，分布式 Core Data，218–221
  - allObjects，214
  - applicationDidFinishLaunching:，220
  - createChildForObject:，217
  - createObject:，216
  - deleteObject:，216
  - netServiceBrowser:didFindService:，220
  - netServiceDidResolveAddress:，221
  - objectsOfName:withPredicate:，218
  - ping，214
  - ping 实现
    - 测试，223
  - 接收来自客户端的请求，213
- 客户端描述文件（Sync Services），149
- ClientDescriptionList 文件，149
- 客户端，同步，141
  - 注册为客户端，153–156
- “客户端”面板（Synchronizers），158
- Cocoa Application 模板，16
- Cocoa 绑定，34–49
  - 键值编码（KVC），34–38
  - 键值观察（KVO），39–40
    - 与 NSArrayController 对象配合使用，42
    - 与 NSFormatter 对象配合使用，43
    - 与 NSObjectController 对象配合使用，46
    - 与 NSOutlineView 对象配合使用，46
    - 与 NSSearchField 对象配合使用，48
    - 与 NSTableView 对象配合使用，41
    - 与 NSViewController 对象配合使用，48
      - NSManagedObject 属性的原始访问，53
      - NSManagedObject 关系的原始访问，56
    - 用于食谱应用程序，40–49
- 创建 Cocoa Touch 项目，184
- 组合框（用户界面），28
  - 绑定到 Type 实体，66
- 常用数据，存储，104
- Compile Sources 部分，77
- contextDidSave: 方法，178
- 控制器层，构建，22–25
  - 将对象添加到 xib 文件，22
- controllerDidChangeContent: 方法，203
- controllerWillChangeContent: 方法，201
- copyPropertiesFromObject:toObject:parent: 方法，179–180
- copyRecipe: 方法，178
- Core Data，定义，9–10
- Core Data API（栈），51
  - 添加到 Cocoa Touch 项目，186–189
  - NSManagedObjectContext，概述，64–67
  - NSManagedObjectModel，概述，68–69
  - NSPersistentStoreCoordinator，概述，69–71
  - 需要，75
- Core Data Application 模板，16
- createChildForObject: 实现（DistributedCDServer），217
- createDestinationInstanceForSourceInstance: 方法，86–88
- createObject: 实现（DistributedCDServer），216
- createParameter: 实现（CDPreferences），235
- createRelationshipForDestinationInstance: 方法，88
- 跨线程通信，164, 177
- 自定义数据存储，98

### D

- 数据变更通知，iPhone，192–194
  - 委托设计模式，193
  - NSFetchedResultsController 对象，194
  - NSNotificationCenter 对象，193
- 数据类（同步模式），142, 143
- 数据反规范化，102
- 数据迁移，73
  - 自动迁移，88–90
    - 开启，78
  - 复杂迁移，示例，85–88
  - 手动迁移，90
  - 过程，82
  - 渐进式迁移，90–95
    - 创建迁移方法，91
    - 查找托管对象模型，92
    - 查找映射模型，93
    - 简单迁移，示例，76–82
      - 创建第一个映射模型，79–81
      - 创建带版本的数据模型，77
      - 开启自动迁移，78
- 数据模型
  - 添加到 Cocoa Touch 项目，185
  - 构建，16–21
    - 将实体添加到模型，17–21
  - 用于 DistributedCDServer 应用程序（示例），209
  - 为同步而更新，143–146
- 数据模型优化，99–104
  - 反规范化数据，102
  - 实体继承，101
  - 智能关系，103
  - 存储二进制数据，99
- 数据对象，21
- DataClasses 键（Schema.plist），147
- DataModel.xcdatamodel 文件，17
- dealloc: 方法，不重写，58
- 委托设计（iPhone），193
- 删除规则，19
- deleteObject: 实现（DistributedCDServer），216
- 删除对象，110
- 反规范化数据，102
- description: 方法，不重写，57
- 目标实体，19
- didFinishFetch: 方法，重写，58
- disconnect 方法，223
- 磁盘访问，**109**
  - 故障与磁盘访问，**111**
  - 获取请求与磁盘访问，**108**
  - SQLite 存储，**109**
  - 写入磁盘，**110**
- DisplayName 键（ClientDescription.plist），**149**
- 分布式对象，与 Core Data 配合使用，**207–227**
  - 构建客户端，**218–221**
    - applicationDidFinishLaunching:，**220**
    - netServiceBrowser:didFindService:，**220**
    - netServiceDidResolveAddress:，**221**
  - 构建服务器，**209–218**
    - allObjects，**214**
    - 广播服务，**210–212**
    - createChildForObject:，**217**
    - createObject:，**216**
    - deleteObject:，**216**
    - 分布式对象协议，**209**
    - objectsOfName:withPredicate:，**218**
    - ping，**214, 223**
    - 接收来自客户端的请求，**213**
    - 启动服务器，**212–213**
  - 使用分布式对象的缺点，**208**
  - 测试网络代码，**222–226**
    - disconnect 方法，**223**
    - startTestTimers 方法，**222**
    - testChildDeletion 方法，**226**
    - testChildInsertion 方法，**225**
    - testObjectDeletion 方法，**225**
    - testObjectFetch 方法，**224**
    - testObjectInsertion 方法，**225**
    - testPing 方法，**223**
- 分布式对象协议，**209**
- DistributedCDClient 项目，**218–221**
  - applicationDidFinishLaunching:，**220**
  - netServiceBrowser:didFindService:，**220**
  - netServiceDidResolveAddress:，**221**
- DistributedCDServer 应用程序，**209–218**
  - DistributedCDServer 应用程序对象，**214**
    - 广播服务，**210–213**
    - createChildForObject:，**217**
    - createObject:，**216**
    - deleteObject:，**216**
    - 分布式对象协议，**209**
    - objectsOfName:withPredicate:，**218**
    - ping，**214**
  - ping 实现
    - 测试，**223**
    - 接收客户端请求，**213**
- 基于文档的应用程序，**219, 228**
- @dynamic 关键字，**38, 53**
- 动态参数，**228–237**
  - 为其构建项目，**230**
  - DocumentPreferences 对象，**230–236**
    - allParameterNames，**236**
    - allParameters，**235**
    - createParameter:，**235**
    - findParameter:，**233**
    - setValue:forUndefinedKey:，**234, 236**
    - valueForUndefinedKey:，**232, 236**

### E

- Enterprise Objects，**10**
- 实体，添加到数据模型，**17–21**
- 数据类中的实体，**142**
- Entities 键（ClientDescription.plist），**149**
- 实体哈希，**83**
- 实体继承，**101**
- entityForName:inManagedObjectContext:
  - 方法，**60**
- 错误，呈现，**76**
- executeFetchRequest:error: 方法，**60**
- 导出食谱（多线程示例），**165–173**

### F

- 故障的 NSManagedObject 对象，**105**
- 故障，**108–112**
  - 磁盘访问与故障，**111**
  - 获取性能，**104–108**
    - 磁盘访问与获取性能，**108**
  - 故障的 NSManagedObject 对象的故障，**105**
  - 加载 NSManagedObjectID 对象，**105**
  - 属性值，预取，**106**
  - 关系，预取，**107, 109**
- 获取请求，**59–63**
  - 磁盘访问与获取请求，**108**
  - 执行，**60**
  - 用于导出食谱（示例），**167**
  - 用于导入食谱（示例），**176**
  - 缩小搜索范围或筛选结果，**61**
  - 设置要获取的实体，**60**
  - 存储，**62**
- 获取的属性，**71**

