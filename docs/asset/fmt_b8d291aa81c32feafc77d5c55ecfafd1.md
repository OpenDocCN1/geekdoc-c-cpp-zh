
如果你自己运行它，`Producing` 和 `Consuming` 的行可能会交错出现，但 `All items have been consumed` 这一行始终会在最后。

`BlockingCollection` 类还拥有静态的 `AddToAny`、`TryAddToAny`、`TakeFromAny` 和 `TryTakeFromAny` 方法。所有这些方法除了接收一个项、一个超时时间和 `CancellationToken` 外，还接收一个 `BlockingCollection<T>[]`。`(Try)AddToAny` 方法会遍历数组中的所有集合，直到找到一个可以接受该项的集合（因为其未达到容量）。`(Try)TakeFromAny` 方法会遍历数组中的所有集合，直到找到一个可以移除项的集合。

## 符号
- .NET Framework
- 检查, 8
- 旧代码, 459
- 反射 API, 583
- 与...稳定性, 34
- 投影, 655
- 版本, 268
- 与 WinRT 的互操作性, 654, 655
- .winmd 文件扩展名, 644

### A
- `AbandonedMutex` 异常, 785
- `Abort` 方法, 579, 581
- `Thread` 类, 679
- 终止线程, 578
- 可访问性, 166
- 可访问修饰符, 156
- 访问器资源, 505
- 访问器方法, 228, 231
- 的可访问性, 248
- 泛型, 248
- 索引器, 244
- 内联, 247
- 命名, 245
- 性能, 247
- `ReaderLock` 方法, 355
- `WriterLock` 方法, 355

### 用于 .NET Framework 的 API
- .NET Framework 的 API, 583
- WinRT 的 API, 调用, 650
- `AppDomain` 类型, 实例方法, 595
- `AppManager` 类, 576
- `AppMonitor` 类, 573
- `AppDomains`, 17
- 终止线程, 跨边界访问对象, 559
- 应用输出, 562
- ASP.NET 应用和, 575
- 集合中的, 557
- 发现, 602
- 多个集合中的, 573
- 回调方法, 573
- 跨边界转换, 565
- `CreateDomain` 方法重载, 563
- 创建, 563
- 默认值, 556
- 定义, 556
- 演示, 563
- 可执行应用和, 574
- 特性, 556
- 第一机会异常通知, 573
- 前台/后台线程和, 688
- 友好名称, 563
- 垃圾回收, 571
- 垃圾回收表, 545
- 优雅偏移量, 577
- 实例字段和, 566, 567
- 隔离性提供的, 557, 566
- 托管代码和, 576
- 卸载, 477, 494, 566, 570
- 作为垃圾回收触发,579
- XML Web应用和, 575
- 针对特定的加载程序集, 585
- 加载到中, 564
- 多次加载到中, 586
- 托管代码和, 576
- 按值序列化对象, 568
- 按引用序列化对象, 564
- 内存使用监控, 524
- 跨边界方法调用, 566
- Microsoft Silverlight 应用和, 574
- 监控, 571
- 跨边界传递对象, 569
- 权限集继承, 563
- 代理类型, 定义, 564
- 目的, 553
- 只读属性中的, 572
- 健壮宿主应用, 577
- 单例类型和, 634
- SQL Server 和, 575
- 静态成员和, 567
- 线程池。见线程
- 线程和, 562
- 卸载

`ArrayEnumerator` 对象，278 个数组，373。另请参见向量的访问，386 访问元素，383 使用不安全代码访问，386 分配，373, 374 在线程栈上分配，388 378 类型之间的强制类型转换，379 集合实现，381 编译器的推断的，376 转换，378 复制，382 元素 元素，380 协变，379 创建，596 Decimal 值的数值，383 派生自，370, 383 动态创建，383 嵌入结构体中，390 隐式类型，239, 376, 377 索引到，375 初始化元素，376 内联，390 内部实现，384 锯齿数组，375 在托管堆中，386 非零下界，383 开销信息，374 传递和返回，382 多边形，375 引用类型，373 引用，376 单维的，375 静态方法，380 任务的，710 类型名称，385 类型的，384 不安全访问，388 WinRT，648, 660 零基的，374 基于长度的，382 as 运算符，96 AsBuffer 方法，658 ASCII 编码

程序集 ASCIIEncoding 对象，353 AsOrdered 方法，718 ASP.NET 异步对象，751 线程模型，748 ASP.NET 应用程序 AppDomain 和，575 运行的进程，687 程序集 32 位和 64 位，8 管理控制，62 程序集链接器（Assembly Linker），以及 52 优点，7 特性，45 特性，45 将模块合并为，45 压缩，74 配置文件，84 配置下载，45 从更改的模块创建，7 区域，59 中的数据文件，46 默认路径到，38 定义的，6, 45 延迟签名，76 部署和打包，60 不同类型中的，46 目录，63 在其中发现类型，590 双倍副本，75 从网络下载，586 执行代码，111 所需的文件，50 友元，154 全局程序集缓存（GAC），72 全局部署的，67 加载到 AppDomain，564 定位，63, 83 句柄表，47 多文件，46, 48 命名空间和，101 平台，指定，8 防止执行的，587 私有部署，67 私有部署，61 发行者策略控制，86 引用，37, 51, 70, 94 98 

# 程序集链接器 (Assembly Linker)

程序集（续）
注册，74
添加资源文件，53
卫星程序（satellite），59
自描述性质，7
序列化和，616
对文件签名，70
查看统计数据，44
强命名的，66, 67, 68, 72
从 GAC 卸载，73
卸载，587
被多个 AppDomain 使用，558
验证，76
跳过验证，77
版本号，58
版本资源属性，56
版本资源中的，54
版本控制问题，597
版本策略，587
Visual Studio IDE，以及 51
弱命名的，66, 68
Win32 解决的，嵌入，54
Windows 安装程序和，73
程序集链接器，52, 53
程序集加载，584
回调方法，587, 588
嵌入依赖的 DLL，588
Load 方法，585
用于元数据分析，586
多次加载到 AppDomain，586
针对特定 AppDomain，585
针对特定架构，583
带有特定路径名称，586
`AssemblyDef` 表，47
`AssemblyRef` 表，39
`AssemblyResolve` 事件，588
程序集类型，25, 592
`AsSequential` 方法，718
`Assert` 方法，502, 503
关联数据，550
`AsStream` 方法，658
缓冲，656
`Assume` 方法，502, 503
`AsTask` 方法，653, 654
`async`，651
`AsyncCoordinator` 类，770, 171

异步计算密集型操作，693。另请参见计算密集型异步
调用，693
启动，700
Windows 调度器和，694
异步异常，495
异步标志，729
异步函数，732
`await` 运算符和，746
`awaiters` 和，738
编译器警告，关闭，746
调试，745
事件处理程序和，741
示例，735
异常处理和，744
可扩展性，738
在框架类库中，742
识别，733
从非调用者线程启动，745
限制，734
作为状态机，734
步入和退出，745
`Task` 对象和，733
线程同步和，757
未处理的异常和，745
`WebClient` 和，744
异步 I/O 操作，729
异步函数和，732
取消，751
并发函数，746
调试器和，731
事件处理程序和，742
`FileStream` 对象和，753
垃圾回收和，731
GUI 响应能力，732
忽略 `SynchronizationContext` 对象，750
不完整的，显示，738
性能优势，731
用于的 `Task` 类型，738
线程优先级，754
异步 lambda 异常，746
异步，操作，650, 691
异步服务器，71
异步线程同步，714
异步 WinRT API，649 826

# C# 编译器 (C# compiler)

`Attribute` 类，424
特性/属性（attributes）。另请参见自定义属性
设置，368
`AttributeUsage` 属性，428
自动实现属性，231
自动重置事件，7782, 784
`AutoReset` 方法，786
`await`，651
`await` 运算符，652
`awaiters`，738, 740

阻塞线程
避免，705, 805
计数器，806
`BlockingCollection` 类，820
块，455, 457, 480
`finally`，455, 456, 478
`try`，454, 497
`bool` 类型，112
装箱，可空类型，447
装箱值方法，135
装箱值类型，124
更改字段，136
效率，130
示例代码，128

后台线程
基础字段，230
`Barrier` 类，805
基础编码和解码，356
基类，296, 312
基类型，与接口，312
`Connection` 方法，755
`Connection` 方法，743
`BinaryFormatter` 对象，614
二进制命名空间，614
二进制运算符，192
可空类型，444
`BinaryReader` 类型，350
`BinaryWriter` 方法，350
`Break` 方法（Parallel），716
缓冲，332
缓冲 LINQ 查询，720
缓冲，548
字节数组方法，516
字节数组，653
字符在字符串中检查，333
扩展，327
小写/大写，更改，318
数值等值，返回，318
检查运算符，699

# C# 

绑定早期/晚期，389
处理的，608
`BindNameTo` 方法，641
`BindTo` 方法，641
位标志，367
位图，垃圾收集，383
字节类型，112
转换为数值值，319
实例方法，318
静态方法，318
字符数组，337
方法，338
字符，317。另请参见文本元素
转换为字节，353

# C++ 编译器，托管

缓存线程，673
引用，550
回调函数，391。另请参见委托
未托管，391
用于，391

# 强制

`char` 类型转换为数值值，319
类型转换为数值类型，319
隐式/显式，114
with/as 运算符，95
`using` 指令，98
C# 支持，404
实现，256
语言翻译，763
处理的原始类型，316
引用类型，35
响应文件，316
不安全代码，174

## CollectionCount 方法

库开发者，异常处理
指南, 478, 485
类
定义, 168, 276
泛型集合, 125
实例, 296
部分, 159
作为引用类型, 119
密封, 168
安全性, 168
静态, 158
WinRT, 646
清理代码, 478。另请参阅 catch 块；finally 块；try 块；垃圾回收
构造, 479
`Dispose` 方法, 535, 537
抛出的异常, 457
保证, 497
对于原生资源, 533
`Clear` 方法, 337
CLI (通用语言基础设施), 24
`Clone` 方法, 335
可克隆变量, 301
克隆字符串, 335
通过序列化克隆, 615
`Close` 方法, 658
已关闭类型, 272
`CloseHandle` 方法, 780
CLR (通用语言运行时)
代码语言与行为, 25
其代码位置, 554
通用语言方面的, 152
其编译器, 4
已定义, 3
演示, 104
字段布局, 123
执行的函数, 471
头文件, 5
托管, 554
与托管代码的互操作性, 30
加载, 8, 556
命名空间和, 98
可空类型支持, 447
向 WinRT 传递数据块, 656
设置主机管理器, 555
关机，垃圾回收
触发器, 519
类型引用，解析, 80
类型安全, 95
版本，检查, 8
中的版本控制, 161
WinRT，映射类型到, 659
`CLR` 投影, 645
WinRT 组件类型系统规则和, 645
`CLRcreateInstance` 函数, 554
`CLRVer.exe`, 8
CLS (通用语言规范), 26
使用它的示例代码, 279
异常, 458
其规则, 28
`Code Craft Checker (CCCheck.exe)`, 503
`Code Craft Document Generator Tool (CCDocGen.exe)`, 504
`Code Craft Reference Assembly Generator (CCRefGen.exe)`, 504
代码技巧, 475, 498
检查, 503, 504
`Contract` 类, 498
定义, 501
异常, 500
运行时代码, 506
用于最大化的工具, 499
针对特征调优, 500
违反, 500
代码爆炸, 183, 277
代码优化, 14, 763
`volatile` 类和, 765
代码页，指定, 352
代码，程序执行顺序, 765
代码重用。另请参阅泛型
`codeBase` 元素, 45, 84
`Collect` 方法, 519, 522, 523
集合类
泛型, 125, 270
线程安全的, 818
集合初始化器, 235
集合对象，序列化/反序列化, 622
集合类型，WinRT, 648
`CollectionCount` 方法, 524

## 集合

集合, 260
向其中添加项, 236
数组实现, 381
中的最大数量, 821
非阻塞转变为阻塞, 820
生产者/消费者场景, 820
WinRT, 648

`ColorMatrix` 类, 244
COM 通用封装器 (CCWs), 644
COM 组件，作为 WinRT 组件, 644
`Combine` 方法, 400
命令行开关，响应文件, 36
通用语言规范。另请参阅 CLS (通用语言规范)
通用类型系统。另请参阅 CTS (通用类型系统)
计算密集型异步线程, 678
计算密集型操作, 691, 693
取消, 696
设置时间后取消, 700
协作取消, 696
发起, 700
周期性, 720
防止取消, 698
`ComputeResult` 方法, 770
`Concat` 方法, 129, 222
拼接字符串, 322
`ConcurrentBag` 类, 818
并发类, 818
`ConcurrentDictionary` 类, 818
`ConcurrentSchedulerPair` 类, 818
`ConcurrentQueue` 类, 818
`ConcurrentStack` 类, 818
条件变量, 811
条件属性类, 440
`WeakTable` 类, 551
配置文件, 62, 84
其组件, 84
定位, 64
发布者控制和, 86
作为单独程序集, 87
`ConfigureAwait` 方法, 750
`Console` 类, 345, 759
其常量, 175
已定义, 151, 175
元数据和, 175
对于非原始类型, 175
不支持, 224
`ConstrainedCopy` 方法, 380
受约束执行区域 (CERs), 475, 494
垃圾回收中的压缩, 509, 521
`Compare` 方法，比较字符串, 325
`CompareExchange` 方法, 769, 776, 810
`CompareInfo` 类，方法, 329
`object`, 326, 327
`CompareOptions` 类型, 324
`CompareTo` 方法, 135, 311, 318
比较字符串, 323
`comparisonType`, 324
`Compilation`属性, 330
`CompilerGenerated` 属性, 410
代码优化, 763
其提供的函数, 470
托管，异常处理, 492
编译源码, 303
`CompleteListener` 方法, 821
组件对象模型 (COM)。另请参阅 objects
组件软件处理 (CSP), 160
其视图, 160
服务, 161
面向对象编程的可组合性, 470
压缩，程序集, 34
构造函数, 289
泛型和, 285
主构造函数, 287
作为引用类型, 287
次要, 288
其类型参数, 287
结构化实例, 594
构造函数约束, 289

## CreateEvent 方法

构造函数方法, 43, 184, 184, 396
调用默认, 186
创建类型, 182
默认, 181
定义多个, 182
定义值类型, 185
对于委托, 398
实例, 181
无参数, 186
其虚方法和, 182
`ConstructorInfo` 对象, 595
构造函数
定义, 595
对于自定义属性类, 428
命名参数, 424
无参数, 235
位置参数, 424
对于序列化/反序列化, 628
线程, 679
上下文结构, 683
上下文切换, 672, 683
作为异步同步, 814
避免, 673
I/O 操作和, 731
性能问题, 672, 683
上下文线程, 671
`ContinueAll` 方法, 710
`ContinueWith` 方法, 705, 707, 729, 733
`Contract` 类, 475
合约程序集, 504
`ContractFailed` 事件, 500
`ContractInvariantMethod` 属性, 502
`ContractReferenceAssembly` 属性, 504
变体引用类型, 395
变体类型参数, 279
`in` 和 `out` 关键字, 280
方便语法, 183
转换构造函数, 195
转换运算符方法, 195
构造, 197
隐式和显式, 196, 197
其元数据, 197
参数, 197
支持, 198
版本运算符，已定义, 372

`Convert` 类, 628
`Convert` 方法, 355
`Convert` 类型, 319, 356
`ConvertList` 方法, 289
协作取消, 696
未处理异常和, 698
`Copy` 方法, 335
`Array` 类, 378, 382
对比 `BlockCopy` 方法, 380
复制操作和装箱类型, 127
复制数组, 378, 382
字符串, 335
`CopyTo` 方法, 335, 382
`Clr.dll`, 574
多个，另请参阅 multiple
`Flags.exe`, 8
损坏
内存, 506
状态，避免, 228
状态 (CERs), 489
损坏。另请参阅 state
`CountDown` 事件类, 504
事件方法, 393, 394
委托链, 275
变体标识符, 326
`in` 和 `out` 关键字, 280
引用类型, 395
类型参数, 279
CPUs。另请参阅 multiple
其用法, 670
多个, 672
用法, 677
用法, 681
用法, 682
用法, 688
用法, 691
方法, 700

## CreateFile 方法

`CreateFile` 方法，同步执行, 752
`CreateFile` 方法，同步执行的, 564
`CreateInstanceUnwrap` 方法, 595
`CreateInstance` 方法, 383
`Activator` 类, 594
`AppDomain` 类, 595
`Array` 类, 396
`CreateResource` 通知, 519
`CreateMutex` 方法, 780
`CreateProcess` 函数, 557
`CreateSemaphore` 方法, 780
关键区域, 577
`CriticalFinal` 对象, 528
`CriticalHandle` 类, 531
`CSC.exe`, 36
`CSC.rsp`, 36
CTS (通用类型系统), 24
CUI (控制台界面)应用程序, 36
其中的区域设置, 59
`CultureInfo` 类, 318
`CultureInfo` 类型, 326
`Current` 属性, 318
`CurrentImage` 属性, 326
自定义属性, 421
多次应用, 427
属性对象，构造, 331
`AttributeUsage` 属性, 428
类继承, 425
构造函数, 428
用于 C# 的 switch, 422
数据类型对于, 428
定义属性类, 425
用于类的定义, 428
其定义, 424
在代码中检测, 430
在代码中检测（不执行）, 457
特定检测, 432
发现, 602
枚举类型, 427
其示例, 422
作为逻辑状态容器, 425

相互匹配, 434
多个，应用, 424
命名参数, 224
位置参数, 224
前缀, 223
公共构造函数, 227
安全性考量, 437
序列化和, 429
后缀，省略, 224
语法用于, 224
目标用于, 223
Visual Basic .NET 语法用于, 223
`CustomAttributeData` 类, 437
`CustomAttributeExtensions` 类, 430

## D

+   数据集合，LINQ 查询, 717
数据封装, 428
数据类型对于，自定义属性类, 428
另请参阅类型
`DataSerializer` 类, 612
数据提示, 339
日期格式化, 341
在 WinRT 中的日期和时间, 647
`DateTime`
结构, 647
类型, 349
`DateTimeFormat` 类型, 343
`DateTimeOffset` 结构, 647
死锁, 750, 761
`debuggable` 属性, 511
调试器
泛型和, 271
异步 I/O 操作和, 731
异步函数, 745
异常, 490
`decimal` 类型, 112, 118
声明委托, 392
声明方法，用于变数量的
参数, 220
声明属性, 231
在匿名类型中, 238

# 显示方法

- `Decoder` 类（Decoder class），356
- 解码 (Decoding)
- 字节 (bytes), 356
- 字符串 (strings), 356
- 减方法 (Decrement method), 791
- 加密 SecureStreams, 360
- 专用线程 (dedicated threads), 679
- 默认 AppDomain, 556
- 默认属性 (default properties)。参参 parameterful
- `DefaultMemberAttribute`, 246
- `DefaultParameterAttribute`, 212
- 类 (classes), 168
- 字段（fields），带有初始化的初始化, 184
- 属性 (properties), 230
- 类型 (types), 251
- 元数据中的定义表 (definition tables in metadata), 39
- 延迟方法 (Delay method), 722
- 延迟签名 (delayed signing), 76
- `Delegate` 类 (Delegate class), 397
- 委托字段 (delegate fields), 257
- 委托类型 (delegate types)
- 扩展方法用于 (extension methods for), 202
- 序列化 (serializing), 618
- WinRT, 647
- 委托 (delegates), 249。另请查看回调函数 (callback functions)
- 添加/删除 (adding/removing), 604
- 数组，返回引用 (arrays, returning reference in), 405
- 回调方法，调用 (callback method, invoking), 399
- 回调实例方法 (calling back instance methods), 395
- 使用...回调静态方法 (calling back static methods with), 394
- 使用...调用私有成员 (calling private members with), 394
- 链式 (chaining), 400, 404
- 链式，C# 的支持 (chaining, C# support for), 404
- 链式，结果变量 (chaining, result variable and), 404
- 由...定义的类 (class defined by), 396, 397
- 构造函数 (constructors), 398
- 逆变类型参数 (contravariant type parameters), 279
- 协变类型参数 (covariant type parameters), 279
- 创建 (creating), 392
- 定义 (defining), 408
- ...的定义 (definitions for), 407
- 扩展方法以及 (nextension methods and), 203
- 垃圾回收 (garbage collection), 401
- 通用 (generic), 278, 407
- ...的初始化 (initialization of), 398
- 不变类型参数 (invariant type parameters), 279
- 动态调用 (invoking dynamically), 417
- 多路复委托类 (MulticastDelegate class), 397
- 反射以及 (reflection and), 416
- 从链中移除 (removing from chains), 403
- 语法 (syntax), 408
- ...的语法快捷方式 (syntax shortcuts for), 409, 410, 213
- 用于任务 (for tasks), 715
- 取消注册 (unregistering), 260
- `Delete` 方法，抛出的异常 (Delete method, exceptions thrown by), 532
- 删除运算符 (delete operator), 93
- `DeleteAsync` 方法, 742
- 部署程序 (deploying assemblies), 60
- 私有地 (privately), 79
- 派生类 (dederived class), 311, 312
- 派生类型，前提条件 (derived types, preconditions and), 502
- 反序列化 (deserialization)
- 状态的 (of application state), 616
- 集合对象的 (of collection objects), 622
- 控制 (controlling), 619
- 数据反卷/解滚 (derrolling data), 624
- ...的定义 (definition of), 611
- 格式化一致性 (formatter consistency), 615
- `ISerializable` 接口 (ISerializable interface), 625
- 匹配的序列化方法 (matching serialization method), 628
- 对象图的 (of object graphs), 615
- 对象的，不同对象的 (of objects, of different objects), 633
- 覆盖程序集/类型 (overriding assembly/type), 640
- ...的快速上手 (quick start for), 613
- 设置 (setting up), 628
- 单例类型的 (of singleton types), 633
- ...的流上下文 (streaming contexts for), 631
- 代理...的 (surrogates for), 636
- 类型绑定 (type bindings), 641
- 类型实例的 (of type instances), 624
- `DeserializeFrom` 方法, 615
- 反序列化对象 (deserializing objects), 182
- 诊断命名空间 (diagnostics namespace), 688
- 字典类型，序列化 (dictionary type, serialization), 626
- 直接内存访问 (direct memory accesses), 386
- 禁用优化标志 (DisableOptimizations flag), 511
- 类型消除歧义 (disambiguating types), 99
- 分发器类 (Dispatcher classes), 723
- `DispatcherUnhandleException` 事件, 488
- 显示方法 (Display method), 283

# Dispose 方法 (Dispose method)

- `Dispose` 方法, 260, 358, 512, 533, 648
- 避免 (avoiding), 535
- 显式调用 (calling explicitly), 337
- `finally` 块中 (in finally block), 535
- 原生资源清理 (native resource cleanup and), 534
- `Task` 对象 (Objects), 708
- `WaitHandle` 类 (Wait class), 780
- 分布式应用程序，未处理的异常 (distributed applications, unhandled exceptions in), 488
- `DllMain` 方法, 671
- DLLs
- ...的互操作性 (interoperability of), 34
- 性能问题以及 (performance issues and), 672
- 线程攻击与分离 (thread-attack and thread-detach)
- 通知 (notifications), 671
- 双检查锁定 (double-check locking), 807
- 双精度类型 (double type), 112
- 从网络下载程序 (downloading assemblies from web), 458
- `dynamic.exe`, 99
- 动态表达式 (dynamic expressions), as object types, 147
- `dynamic` 关键字 (dynamic keyword), 214
- 动态类型 (dynamic type), 112
- ...的示例 (example of), 145
- `var` 关键字 (var keyword), 146
- 动态可扩展应用程序 (dynamically extensible applications), 583
- 构建 (building), 588
- 扩展性框架 (MEF), 598
- `DynamicAttribute` 方法, 145
- `dynamicInvocation` 方法, 417
- 动态化 (dynamification), 147
- `EnsureCapacity` 方法, 337
- `EnsureInitialized` 方法, 811
- `EnsureExecutionStack` 方法, 489
- `Enter` 方法, 790
- 重载，不建议 (overloading, discouraged), 476
- `Monitor` 类 (Monitor class), 795
- `Enum` 类 (Enum class), 362
- `Enum` 类型 (Enum type), 664
- 枚举类型 (enumerated type), 661
- 位标志，带有 (bit flags, defined with), 368
- 派生类 (classes derived from), 362
- 将符号转换为... (converting symbols into), 366
- 将值转换为... (converting values into flags), 370
- 声明 (declaring), 363
- 定义的符号 (defined symbols in), 370
- 定义 (defining), 367
- 显示所有值 (displaying all values for), 365
- 扩展方法用于 (extension methods for), 202
- 格式化 (formatting), 364
- `isDefined` 以及 (isDefined and), 371
- 映射到字符串 (mapping to strings), 364
- 方法 (methods), 371
- 多符号 (with multiple symbols), 364
- 参数验证 (parameter validation), 366
- 作为原始类型 (as primitive types), 363
- 序列化 (serializing), 618
- ...的结构 (structure of), 362
- 常量字段 (symbols as constant fields), 362
- 底层类型 (underlying types for), 363
- 用户界面显示 (user interface display of), 365
- 枚举类型 (enumerating types), 588
- WinRT 中的枚举类型 (enumeration types, in WinRT), 646
- 临时垃圾收集 (ephemeral garbage collector). See collection
- 结束代码 (epilogue code), 102
- 等于运算符，可空类型 (equality operators, nullable types, and), 444
- `Equals` 方法 (Equals method), 139, 238, 332, 388
- 覆盖 (overriding), 140, 141
- ...的属性 (properties of), 141
- `System.Object`, 92
- 错误消息 (error messages), 157
- 错误。查看异常处理器 (errors. See exceptions; exception handler)
- 升级策略 (escalation policy), 577
- 早期绑定 (early binding), 589
- 显式构建类型 (explicitly constructing types), 353
- 无状态的 (stateless), 356
- `Encoding` 类 (Encoding class), 352
- 属性 (properties), 352
- 编码 (encodings), 350
- 属性值 (property values), 354
- `EndBackground.Processing.`, 755
- `EndsWith` 方法，比较字符串 (EndsWith method, comparing strings), 325
- `WaitForConnection` 方法, 743
- `Endx` 方法, 481
- 异步函数以及 (asynchronous functions and), 741
- 类命名规范 (class naming convention), 251

# 异常 (exceptions)

- 代码约违背 (code contract violations), 500
- 方法签名 (method signatures), 741
- `void` 返回类型 (void return type), 253
- 事件日志，查看...中的未处理异常 (event log, viewing unhandled exceptions in), 485
- 用于类库对比 应用程序开发者 (for class library vs. application developers), 478, 485
- CLS 对象 (CLS objects), 458
- 定义的 (defined), 453
- `EventArgs` 类 (EventArgs class), 251
- `EventAwaiter` 类 (EventAwaiter class), 741
- `EventDef` 表 (EventDef table), 39
- `EventHandler` 委托类型 (WinRT), 647
- `EventStore` 类型 (EventStore type), 262
- 事件 (events), 249, 282
- 不同的实现 (differing implementations of), 492
- ...的示例代码 (example code for), 453
- 由...抛出的异常 (exceptions thrown by), 457
- `finally` 块 (finally blocks), 456, 478
- 指南 (guidelines), 478, 485
- 高错误率方法 (high error rate methods), 493
- 用于...语言 (language for), 457
- `_add` 前缀 (_add prefix), 257
- 应用程序架构设计 (architecting applications for), 250
- 自动重置 (auto-reset), 784
- 编译器的实现 (compiler implementation of), 256
- 定义 (defined), 24
- 委托 (delegates), 249
- 委托，添加/删除 (delegates, adding/removing), 604
- 设计以暴露类型 (designing types to expose), 250
- 显式实现 (explicitly implementing), 260
- 成员，定义 (members, defining), 252
- 上的元数据 (metadata on), 604
- 管理编译器以及 (managing compilers and), 467
- ...的机制 (mechanics of), 453
- 迁移代码用于 (migrating code for), 459
- 非 CLS 对象 (non-CLS objects), 458
- 用于...的通知 (notifications for), 456
- 性能问题 (performance issues), 492
- ...中的问题 (problems with), 477
- 运行时以及 (runtime and), 451
- 运行的 (running), 452
- 运行时 (runtime), 453
- 运行环境 (runtime environment), 454
- 运行时的 (runtime), 455
- 运行时的 (runtime), 456
- 运行时的 (runtime), 457
- 运行时的 (runtime), 458
- 运行时的 (runtime), 459
- 运行时的 (runtime), 460
- 运行时的 (runtime), 461
- 运行时的 (runtime), 462
- 运行时的 (runtime), 463
- 运行时的 (runtime), 464
- 运行时的 (runtime), 465
- 运行时的 (runtime), 466
- 运行时的 (runtime), 467
- 运行时的 (runtime), 468
- 运行时的 (runtime), 469
- 运行时的 (runtime), 470
- 运行时的 (runtime), 471
- 运行时的 (runtime), 472
- 运行时的 (runtime), 473
- 运行时的 (runtime), 474
- 运行时的 (runtime), 475
- 运行时的 (runtime), 476
- 运行时的 (runtime), 477
- 运行时的 (runtime), 478
- 运行时的 (runtime), 479
- 运行时的 (runtime), 480
- 运行时的 (runtime), 481
- 运行时的 (runtime), 482
- 运行时的 (runtime), 483
- 运行时的 (runtime), 484
- 运行时的 (runtime), 485
- 运行时的 (runtime), 486
- 运行时的 (runtime), 487
- 运行时的 (runtime), 488
- 运行时的 (runtime), 489
- 运行时的 (runtime), 490
- 运行时的 (runtime), 491
- 运行时的 (runtime), 492
- 运行时的 (runtime), 493
- 运行时的 (runtime), 494
- 运行时的 (runtime), 495
- 运行时的 (runtime), 496
- 运行时的 (runtime), 497
- 运行时的 (runtime), 498
- 运行时的 (runtime), 499
- 运行时的 (runtime), 500
- 运行时的 (runtime), 501
- 运行时的 (runtime), 502
- 运行时的 (runtime), 503
- 运行时的 (runtime), 504
- 运行时的 (runtime), 505
- 运行时的 (runtime), 506
- 运行时的 (runtime), 507
- 运行时的 (runtime), 508
- 运行时的 (runtime), 509
- 运行时的 (runtime), 510
- 运行时的 (runtime), 511
- 运行时的 (runtime), 512
- 运行时的 (runtime), 513
- 运行时的 (runtime), 514
- 运行时的 (runtime), 515
- 运行时的 (runtime), 516
- 运行时的 (runtime), 517
- 运行时的 (runtime), 518
- 运行时的 (runtime), 519
- 运行时的 (runtime), 520
- 运行时的 (runtime), 521
- 运行时的 (runtime), 522
- 运行时的 (runtime), 523
- 运行时的 (runtime), 524
- 运行时的 (runtime), 525
- 运行时的 (runtime), 526
- 运行时的 (runtime), 527
- 运行时的 (runtime), 528
- 运行时的 (runtime), 529
- 运行时的 (runtime), 530
- 运行时的 (runtime), 531
- 运行时的 (runtime), 532
- 运行时的 (runtime), 533
- 运行时的 (runtime), 534
- 运行时的 (runtime), 535
- 运行时的 (runtime), 536
- 运行时的 (runtime), 537
- 运行时的 (runtime), 538
- 运行时的 (runtime), 539
- 运行时的 (runtime), 540
- 运行时的 (runtime), 541
- 运行时的 (runtime), 542
- 运行时的 (runtime), 543
- 运行时的 (runtime), 544
- 运行时的 (runtime), 545
- 运行时的 (runtime), 546
- 运行时的 (runtime), 547
- 运行时的 (runtime), 548
- 运行时的 (runtime), 549
- 运行时的 (runtime), 550
- 运行时的 (runtime), 551
- 运行时的 (runtime), 552
- 运行时的 (runtime), 553
- 运行时的 (runtime), 554
- 运行时的 (runtime), 555
- 运行时的 (runtime), 556
- 运行时的 (runtime), 557
- 运行时的 (runtime), 558
- 运行时的 (runtime), 559
- 运行时的 (runtime), 560
- 运行时的 (runtime), 561
- 运行时的 (runtime), 562
- 运行时的 (runtime), 563
- 运行时的 (runtime), 564
- 运行时的 (runtime), 565
- 运行时的 (runtime), 566
- 运行时的 (runtime), 567
- 运行时的 (runtime), 568
- 运行时的 (runtime), 569
- 运行时的 (runtime), 570
- 运行时的 (runtime), 571
- 运行时的 (runtime), 572
- 运行时的 (runtime), 573
- 运行时的 (runtime), 574
- 运行时的 (runtime), 575
- 运行时的 (runtime), 576
- 运行时的 (runtime), 577
- 运行时的 (runtime), 578
- 运行时的 (runtime), 579
- 运行时的 (runtime), 580
- 运行时的 (runtime), 581
- 运行时的 (runtime), 582
- 运行时的 (runtime), 583
- 运行时的 (runtime), 584
- 运行时的 (runtime), 585
- 运行时的 (runtime), 586
- 运行时的 (runtime), 587
- 运行时的 (runtime), 588
- 运行时的 (runtime), 589
- 运行时的 (runtime), 590
- 运行时的 (runtime), 591
- 运行时的 (runtime), 592
- 运行时的 (runtime), 593
- 运行时的 (runtime), 594
- 运行时的 (runtime), 595
- 运行时的 (runtime), 596
- 运行时的 (runtime), 597
- 运行时的 (runtime), 598
- 运行时的 (runtime), 599
- 运行时的 (runtime), 600
- 运行时的 (runtime), 601
- 运行时的 (runtime), 602
- 运行时的 (runtime), 603
- 运行时的 (runtime), 604
- 运行时的 (runtime), 605
- 运行时的 (runtime), 606
- 运行时的 (runtime), 607
- 运行时的 (runtime), 608
- 运行时的 (runtime), 609
- 运行时的 (runtime), 610
- 运行时的 (runtime), 611
- 运行时的 (runtime), 612
- 运行时的 (runtime), 613
- 运行时的 (runtime), 614
- 运行时的 (runtime), 615
- 运行时的 (runtime), 616
- 运行时的 (runtime), 617
- 运行时的 (runtime), 618
- 运行时的 (runtime), 619
- 运行时的 (runtime), 620
- 运行时的 (runtime), 621
- 运行时的 (runtime), 622
- 运行时的 (runtime), 623
- 运行时的 (runtime), 624
- 运行时的 (runtime), 625
- 运行时的 (runtime), 626
- 运行时的 (runtime), 627
- 运行时的 (runtime), 628
- 运行时的 (runtime), 629
- 运行时的 (runtime), 630
- 运行时的 (runtime), 631
- 运行时的 (runtime), 632
- 运行时的 (runtime), 633
- 运行时的 (runtime), 634
- 运行时的 (runtime), 635
- 运行时的 (runtime), 636
- 运行时的 (runtime), 637
- 运行时的 (runtime), 638
- 运行时的 (runtime), 639
- 运行时的 (runtime), 640
- 运行时的 (runtime), 641
- 运行时的 (runtime), 642
- 运行时的 (runtime), 643
- 运行时的 (runtime), 644
- 运行时的 (runtime), 645
- 运行时的 (runtime), 646
- 运行时的 (runtime), 647
- 运行时的 (runtime), 648
- 运行时的 (runtime), 649
- 运行时的 (runtime), 650
- 运行时的 (runtime), 651
- 运行时的 (runtime), 652
- 运行时的 (runtime), 653
- 运行时的 (runtime), 654
- 运行时的 (runtime), 655
- 运行时的 (runtime), 656
- 运行时的 (runtime), 657
- 运行时的 (runtime), 658
- 运行时的 (runtime), 659
- 运行时的 (runtime), 660
- 运行时的 (runtime), 661
- 运行时的 (runtime), 662
- 运行时的 (runtime), 663
- 运行时的 (runtime), 664
- 运行时的 (runtime), 665
- 运行时的 (runtime), 666
- 运行时的 (runtime), 667
- 运行时的 (runtime), 668
- 运行时的 (runtime), 669
- 运行时的 (runtime), 670
- 运行时的 (runtime), 671
- 运行时的 (runtime), 672
- 运行时的 (runtime), 673
- 运行时的 (runtime), 674
- 运行时的 (runtime), 675
- 运行时的 (runtime), 676
- 运行时的 (runtime), 677
- 运行时的 (runtime), 678
- 运行时的 (runtime), 679
- 运行时的 (runtime), 680
- 运行时的 (runtime), 681
- 运行时的 (runtime), 682
- 运行时的 (runtime), 683
- 运行时的 (runtime), 684
- 运行时的 (runtime), 685
- 运行时的 (runtime), 686
- 运行时的 (runtime), 687
- 运行时的 (runtime), 688
- 运行时的 (runtime), 689
- 运行时的 (runtime), 690
- 运行时的 (runtime), 691
- 运行时的 (runtime), 692
- 运行时的 (runtime), 693
- 运行时的 (runtime), 694
- 运行时的 (runtime), 695
- 运行时的 (runtime), 696
- 运行时的 (runtime), 697
- 运行时的 (runtime), 698
- 运行时的 (runtime), 699
- 运行时的 (runtime), 700
- 运行时的 (runtime), 701
- 运行时的 (runtime), 702
- 运行时的 (runtime), 703
- 运行时的 (runtime), 704
- 运行时的 (runtime), 705
- 运行时的 (runtime), 706
- 运行时的 (runtime), 707
- 运行时的 (runtime), 708
- 运行时的 (runtime), 709
- 运行时的 (runtime), 710
- 运行时的 (runtime), 711
- 运行时的 (runtime), 712
- 运行时的 (runtime), 713
- 运行时的 (runtime), 714
- 运行时的 (runtime), 715
- 运行时的 (runtime), 716
- 运行时的 (runtime), 717
- 运行时的 (runtime), 718
- 运行时的 (runtime), 719
- 运行时的 (runtime), 720
- 运行时的 (runtime), 721
- 运行时的 (runtime), 722
- 运行时的 (runtime), 723
- 运行时的 (runtime), 724
- 运行时的 (runtime), 725
- 运行时的 (runtime), 726
- 运行时的 (runtime), 727
- 运行时的 (runtime), 728
- 运行时的 (runtime), 729
- 运行时的 (runtime), 730
- 运行时的 (runtime), 731
- 运行时的 (runtime), 732
- 运行时的 (runtime), 733
- 运行时的 (runtime), 734
- 运行时的 (runtime), 735
- 运行时的 (runtime), 736
- 运行时的 (runtime), 737
- 运行时的 (runtime), 738
- 运行时的 (runtime), 739
- 运行时的 (runtime), 740
- 运行时的 (runtime), 741
- 运行时的 (runtime), 742
- 运行时的 (runtime), 743
- 运行时的 (runtime), 744
- 运行时的 (runtime), 745
- 运行时的 (runtime), 746
- 运行时的 (runtime), 747
- 运行时的 (runtime), 748
- 运行时的 (runtime), 749
- 运行时的 (runtime), 750
- 运行时的 (runtime), 751
- 运行时的 (runtime), 752
- 运行时的 (runtime), 753
- 运行时的 (runtime), 754
- 运行时的 (runtime), 755
- 运行时的 (runtime), 756
- 运行时的 (runtime), 757
- 运行时的 (runtime), 758
- 运行时的 (runtime), 759
- 运行时的 (runtime), 760
- 运行时的 (runtime), 761
- 运行时的 (runtime), 762
- 运行时的 (runtime), 763
- 运行时的 (runtime), 764
- 运行时的 (runtime), 765
- 运行时的 (runtime), 766
- 运行时的 (runtime), 767
- 运行时的 (runtime), 768
- 运行时的 (runtime), 769
- 运行时的 (runtime), 770
- 运行时的 (runtime), 771
- 运行时的 (runtime), 772
- 运行时的 (runtime), 773
- 运行时的 (runtime), 774
- 运行时的 (runtime), 775
- 运行时的 (runtime), 776
- 运行时的 (runtime), 777
- 运行时的 (runtime), 778
- 运行时的 (runtime), 779
- 运行时的 (runtime), 780
- 运行时的 (runtime), 781
- 运行时的 (runtime), 782
- 运行时的 (runtime), 783
- 运行时的 (runtime), 784
- 运行时的 (runtime), 785
- 运行时的 (runtime), 786
- 运行时的 (runtime), 787
- 运行时的 (runtime), 788
- 运行时的 (runtime), 789
- 运行时的 (runtime), 790
- 运行时的 (runtime), 791
- 运行时的 (runtime), 792
- 运行时的 (runtime), 793
- 运行时的 (runtime), 794
- 运行时的 (runtime), 795
- 运行时的 (runtime), 796
- 运行时的 (runtime), 797
- 运行时的 (runtime), 798
- 运行时的 (runtime), 799
- 运行时的 (runtime), 800
- 运行时的 (runtime), 801
- 运行时的 (runtime), 802
- 运行时的 (runtime), 803
- 运行时的 (runtime), 804
- 运行时的 (runtime), 805
- 运行时的 (runtime), 806
- 运行时的 (runtime), 807
- 运行时的 (runtime), 808
- 运行时的 (runtime), 809
- 运行时的 (runtime), 810
- 运行时的 (runtime), 811
- 运行时的 (runtime), 812
- 运行时的 (runtime), 813

# FxCopCmd.exe.

`FieldInfo` 对象，转换为
`RuntimeFieldHandle`, 609
支持的字段, 230

在装箱值类型中，更改, 136
定义的, 24, 151, 177
定义, 178
在未初始化的情况下定义, 184
封装, 228
初始化, 182, 187
使用方便语法的初始化, 183
内联初始化, 179
私有的, 168, 228, 231

`Dispose` 方法，在, 535
抛出的异常, 457
适度使用, 478
`try` 块和，和, 457
`FirstChanceException` 事件, 573
`fixed` 语句, 548
`Flags` 特性, 368
`FlagsAttribute` 类, 430
`Flatten` 方法, 703
`float` 类型, 112
`FlushAsync` 方法, 742
`For` 方法 (`Parallel` 类), 713, 714
`ForAll` 方法, 718
强制垃圾回收, 522, 539
`ForEach` 方法 (`Parallel` 类), 713, 714
前台线程
强制, 679
vs. 后台线程, 688
`Format` 方法, 344, 364
重载, 344
vs `ToString` 方法, 364
`FormatterConverter` 类型, 628
`Formatter` 类型, 623, 628
格式化，字符串，346
`Forms` 命名空间，`Timer` 类, 723
框架类库。参见 FCL (Framework
Class Library)
其中的异步函数, 742
类型。参见 FCL 类型
框架投影, 645, 649
可终化队列, 543
终化列表和, 544
命名, 544
`Free` 方法, 548
友元程序集, 154
在模块中的, 156
友好名称, 563
`FromAsync` 方法, 743
`FromBase66` 方法, 356
`FromCurrentSynchronizationContext`
方法, 711
`Func` 委托, 279, 408
函数，回调。参见回调函数
`FxCopCmd.exe`, 480

`FieldSetter` 方法, 566
文件扩展名
用于 WinRT 组件, 644
.wmdn, WinRT, 645
文件名，版本控制，带有, 66
`FileAttributes` 类型, 367
`FileDef` 表, 47, 181
`FileNotException` 异常, 384
`FileStream`
类, 532
I/O 操作, 728
对象，异步和同步
类型, 525, 537
终化, 525, 542
垃圾回收和, 544
列表, 542
可终化队列和, 544
`Finalize` 方法, 525, 526, 542
专门用于 CLR 线程, 344
继承的, 543
内存泄漏和, 526
重写, 479
与析函数的相似性, 526
`SystemObject`, 92
`finally` 块, 455, 456. 另另 catch 调用，
`try` 块
作为回调方法, 497
受约束执行区域和, 475

# GAC (全局程序集缓存)

# G

+ GAC (全局程序集缓存), 72
安装到, 72
所需的权限, 73
从...中卸载程序集, 73
`GACutil.exe`, 72
Windows 安装开关, 73
垃圾回收, 507
算法, 507
异步 I/O 操作和, 731
用于位图, 538
字节数组方法和, 548
`Collect` 方法, 523
压缩阶段, 509
并发 vs. 非并发方法, 521
调试和, 510
依赖问题, 537
`Dispose` 方法, 512
vs. `Dispose` 方法, 535
终化对象, 544
`Finalize` 方法和, 526
强制, 529
分代的, 513
由...假设, 514
代代, 513
句柄表, 545, 547
空闲线程和, 517
大对象和, 519
延迟方法, 522
管理器, 567
标记阶段, 508
内存构建和, 517
内存压缩, 521
内存使用, 524
监控, 524
原生资源和, 538
通知, 518, 523
对象生命周期和, 510
生命周期，手动控制, 545
`OutOfMemory` 异常, 510
性能目标, 515
固定对象, 548

+ 计数算法, 508
修正后的对象, 544
根和, 509
服务器方法, 520
符号, 522
线程和, 673
`Timer` 对象和, 721
触发器, 519
用于原生资源, 525
在加载的 AppDomains 上, 571
弱引用和, 550
工作站方法, 520
`GCCollection` 枚举类型, 523
`Handle` 类型, 545
显式的, 548
`Handle` 类型, 546
`LatencyMode` 属性, 521
`GCNotification` 类, 518
`GCSettings` 类, 521
`GCWatch` 方法, 551
代代, 1, 2, 513, 514, 516
的, 516
提升到, 515
泛参数，限制类型, 285
集合类, 125, 270
逆变和协变类型
参数, 281
委托, 278, 407
接口, 277, 278, 297, 303
列表算法, 266
命名空间, 313
vs. 非泛型版本, 304
类型标识, 275
类型参数, 305
泛型方法, 265, 281
示例, 282
重写, 286
静态, 270
类型推断和, 283
泛型类型变量
操作数, 292
转换, 290

# GetWindowsRuntimeBuffer 方法

相互比较, 292
与 null 比较, 291
设置为默认值, 291
泛型类型, 265
构造, 596
定义, 273
继承和, 274
`out` 和 `ref` 参数, 282
参数, 269
类型参数, 266
用于类型对象, 272
`using` 指令和, 276
泛型
向后兼容, 270
益处, 267
约束, 267
显式声明, 281
`in` 和 `ref` 关键字, 281
f FCL, 270
基础, 271
接口和, 275
成员, 277
概述, 278
性能, 279
可变性, 268
变异和, 280
`GetAssemblyName`, 269
`GetAsync` 方法, 291
`AvailableThreads`, 291
`BaseException`, 272
`ByteArray` 方法, 292
`GetCharCount`, 272
`Chars` 方法, 273
`CustomAttribute`, 274
`Decoder` 方法, 274
`Domain` 方法, 275
`Encoding` 方法, 276
`Enumerator`, 277
`Enum` 方法, 277
`EnumValues`, 278
`Format` 方法, 297
`GenericArguments`, 303
`HashCode` 方法, 281
`Invocation` 方法, 281
`Lower` 方法, 281
`MinValue` 方法, 282
`MaxValue` 方法, 282
`NumericValue`, 282
`Object` 方法, 283
`Real` 方法, 283
`Runtime` 方法, 285
`String` 方法, 285
`Stream` 方法, 286
`Text` 方法, 286
`Unicode` 方法, 286
`UnderlyingType`, 286

# GAC (全局程序集缓存)

# G

+ GAC (全局程序集缓存), 72
安装到, 72
所需的权限, 73
从...中卸载程序集, 73
`GACutil.exe`, 72
Windows 安装开关, 73
垃圾回收, 507
算法, 507
异步 I/O 操作和, 731
用于位图, 538
字节数组方法和, 548
`Collect` 方法, 523
压缩阶段, 509
并发 vs. 非并发方法, 521
调试和, 510
依赖问题, 537
`Dispose` 方法, 512
vs. `Dispose` 方法, 535
终化对象, 544
`Finalize` 方法和, 526
强制, 529
分代的, 513
由...假设, 514
代代, 513
句柄表, 545, 547
空闲线程和, 517
大对象和, 519
延迟方法, 522
管理器, 567
标记阶段, 508
内存构建和, 517
内存压缩, 521
内存使用, 524
监控, 524
原生资源和, 538
通知, 518, 523
对象生命周期和, 510
生命周期，手动控制, 545
`OutOfMemory` 异常, 510
性能目标, 515
固定对象, 548

+ 计数算法, 508
修正后的对象, 544
根和, 509
服务器方法, 520
符号, 522
线程和, 673
`Timer` 对象和, 721
触发器, 519
用于原生资源, 525
在加载的 AppDomains 上, 571
弱引用和, 550
工作站方法, 520
`GCCollection` 枚举类型, 523
`Handle` 类型, 545
显式的, 548
`Handle` 类型, 546
`LatencyMode` 属性, 521
`GCNotification` 类, 518
`GCSettings` 类, 521
`GCWatch` 方法, 551
代代, 1, 2, 513, 514, 516
的, 516
提升到, 515
泛参数，限制类型, 285
集合类, 125, 270
逆变和协变类型
参数, 281
委托, 278, 407
接口, 277, 278, 297, 303
列表算法, 266
命名空间, 313
vs. 非泛型版本, 304
类型标识, 275
类型参数, 305
泛型方法, 265, 281
示例, 282
重写, 286
静态, 270
类型推断和, 283
泛型类型变量
操作数, 292
转换, 290

# GetWindowsRuntimeBuffer 方法

相互比较, 292
与 null 比较, 291
设置为默认值, 291
泛型类型, 265
构造, 596
定义, 273
继承和, 274
`out` 和 `ref` 参数, 282
参数, 269
类型参数, 266
用于类型对象, 272
`using` 指令和, 276
泛型
向后兼容, 270
益处, 267
约束, 267
显式声明, 281
`in` 和 `ref` 关键字, 281
f FCL, 270
基础, 271
接口和, 275
成员, 277
概述, 278
性能, 279
可变性, 268
变异和, 280
`GetAssemblyName`, 269
`GetAsync` 方法, 291
`AvailableThreads`, 291
`BaseException`, 272
`ByteArray` 方法, 292
`GetCharCount`, 272
`Chars` 方法, 273
`CustomAttribute`, 274
`Decoder` 方法, 274
`Domain` 方法, 275
`Encoding` 方法, 276
`Enumerator`, 277
`Enum` 方法, 277
`EnumValues`, 278
`Format` 方法, 297
`GenericArguments`, 303
`HashCode` 方法, 281
`Invocation` 方法, 281
`Lower` 方法, 281
`MinValue` 方法, 282
`MaxValue` 方法, 282
`NumericValue`, 282
`Object` 方法, 283
`Real` 方法, 283
`Runtime` 方法, 285
`String` 方法, 285
`Stream` 方法, 286
`Text` 方法, 286
`Unicode` 方法, 286
`UnderlyingType`, 286

# 中间反汇编工具 (Intermediate Disassembler utility)

编译, 244
命名, 245
参数, 244
`INEFFICIENT` 符号, 199, 329
继承参数, 432
继承, 295
用于接口, 297
接口的, 298
多个, 295
`Object` 类和, 296
前置条件的的, 502
继承的成员冲突, 170
`InitializeLifetimeServices` 方法, 567
初始化器, 235
初始化
集合, 236
对象, 106, 235
初始化字段, 182, 187
内联 (inline), 179
使用方便的语法, 183
内联数组, 390
内联字段识别, 179
内联代码, 247
`InnerExceptions` 集合, 699
`Insert` 方法, 338
`InsertAt` 方法, 358
实例构造函数, 181, 384
显式调用, 185
不创建类型, 182
默认, 181
已定义, 151
定义多个, 182
继承, 181
`virtual` 方法和, 182
实例字段
`AppDomains` 和, 566
性能和, 567
`nerial`, 619
实例方法, 163, 595
调用, 199
带委托的回调, 365
用于 `Char` 类型, 318
线程安全, 760
`volatile` 关键字, 267
`int` 类型, 112

`Int32` 字段，在 `Task` 对象中, 708
`Int32` 变量, 静态方法的, 768
知识产权
IL 代码和, 19
NGen exe 和, 20
`IntelliSense`, 200
`interface` 关键字, 297
接口方法
调用, 302
使用可空类型调用, 498
强类型, 304
用于值类型, 319
接口类型, 约束, 288
接口
vs. 基类型, 312
装箱和, 306, 308
与集合相关的, 313
将泛型类型参数约束为, 305
`dynamic`, 296
示例, 297
泛型, 203
泛型与非泛型的对比, 304
继承, 297, 298
包含的项目, 296
方法, 调用, 300
多个实现实现, 305
命名规范, 297
非泛型,
作为参数类型, 306
`public` 方法, 299
具有相同方法, 307
`static-ic` 成员和, 297
`String` 类型和, 300
类型参数, 305
类型安全和, 309
值类型和, 301
它们的变量, 300
版本控制, 313
`virtual` 方法和, 299
可见性-访问性, 297
WinRT, 646
`Interlocked` 类, 768, 769, 773, 803
805, 810
`interlocked` 构造, 762, 768
中间反汇编工具。
参见 `ILDas.exe`

841

# InternalsVisibleTo 属性

# J

`InternalsVisibleTo` 属性. 155
`InteropServices` 命名空间, 424, 531
`InvalidOperationException` 异常, 587
`InvariantCulture` 属性, 342
不变的类型参数, 279
`Invoke` 方法, 396, 403, 595, 603
`Parallel` 类, 714
调用类型方法, 603
I/O 完成端口, 731
I/O 操作, 727
异步的, 729, 731, 746
取消, 751
上下文切换和, 731
事件处理器和, 742
忽略 `SynchronizationContext` 对象, 750
IRPs 中的, 728
同步的, 752
线程阻塞和, 731
线程优先级, 754
浪费资源和, 728
I/O 请求包 (IRPs), 728
`IOException` 异常, 532
`IOTaskScheduler`, 712
`OutputStream` 接口, 655
`ProducerConsumerCollection` 接口, 820
`IRandomAccessStream` 接口, 655, 657
`is` 运算符, 955
IS-A 关系, 312
`isCancellationRequested` 属性, 698
`isDefined` 方法, 366, 370, 431
用于位标志-枚举类型, 371
`enum` 方法, 366
`ISerializable` 接口, 625, 629, 630
为其定义类型, 630
特殊构造函数, 629
`SerializationSurrogate`
接口, 640
类型, 637
`isSurrogateSelector` 接口, 639
`jagged` 数组, 375
JIT 编译器, 122
优化, 15
安全代码和, 14, 16
`JITFunction`, 122
`Join` 方法, 680
内核构造, 何使用,806
760, 761, 778, 784
vs. 用户模式构造, 778, 784
内核模式栈, 671
内核对象, 671
键/值对, 哈希码, 142
关键字, vs. 类型名称, 113
`lambda` 表达式, 410, 411
异步的, 746
益处, 413
分离方法, 314
语言标识符, 326
语言设置, 59
大型对象, 519
`LastIndexOf` 方法, 329
晚绑定, 589
`lazy` 类, 810
懒性初始化, 807
`LazyInitializer` 类, 811
`LazyThreadSafetyMode`, 811
租管理器, 567
`Leave` 方法, 790
字母大小写, 318
`LimitedConcurrencyLevel`, 712

# MEF (托管扩展框架)

在其中的数据类型, 274
缓冲和合并, 720
并行处理, 719
操作顺序, 718
从这里处理数据, 718
顺序的, 717
最好地, 719
匿名类型, 239
语言集成查询, 717
查询集合的, 717
标准运算符, 717
查询对象, 717
`List` 类 (泛型), 226
链接列表, 添加到, 257
类型, 114
锁, 361
`Machine.config` 文件, 64
`Main` 方法, 43, 764
维持状态, 482
`MakeRefType` 方法, 608
`MakeGeneric` 方法, 596
优先级排序, 687
升级策略, 577
性能关注, 15
性能, vs. 未托管, 15
使用其减少过程, 17
状态和, 477
作为 WinRT 组件, 660
托管调试助手 (MDAs), 538
托管扩展框架 (MEF), 598
托管堆
从这里分配资源, 506
数组中的, 374
示例的, 507
垃圾回收和, 507
合并到程序集, 5
组件的, 5
元数据, 5
清单表, 47, 49
`ManifestResourceDef`, 47
手动重置事件, 782
`ManualResetEvents` 类, 794, 804
垃圾回收中的标记对象, 508
`Marshal` 类, 360
`MarshalByRefObject` 类, 564, 567, 599, 798
`MarshalByValType` 类型, 568
按值封箱对象, 566
`Match` 方法, 434
`Math` 类, 759
`Maximum` 方法, 776
`Max` 方法, 759
`MaxValue` 字段, 317
MBCS (多字节字符集),转换为 Unicode, 350
MDAs (托管调试助手), 538
MEF (托管扩展框架), 598
`Load` 方法 (`AppDomain` 类), 585, 616
加载的, 585
序列化和, 719
`Loadfile`, 586
`LoadFrom` 方法, 586
序列化和, 717
使用 URL 加载程序集, 586.参见程序集加载
Library 函数, 10
本地参数, 回调方法引用, 413
隐式类型本地变量, 212
定位程序集, 63
`lock`, 799
扩展性问题, 814
锁定线程, 双重检查, 807
`Locktaken` 变量, 799
`long` 类型, 112, 113
慢代理代码值, 333
小写/大写之间的转换, 318
低延迟垃圾回收模式, 521

## 成员访问性

成员访问性, 156, 166
类, 602
类型, 599
`Memberwise` 方法, 182
`System.Object`, 92
`memcpy` 函数, 378
`MemoryStream` 类, 656
分配, 506, 507, 509, 510, 511, 513, 517, 521, 524, 526, 527
垃圾回收和, 507, 508, 509, 510, 511, 513, 517, 521, 524, 526, 527
垃圾回收中的压缩, 507, 508, 509, 510, 511, 513
压力, 507, 508, 509, 510, 511, 513, 517, 521, 524, 526, 527
回收资源, 539
合并 LINQ 结果, 720
元数据, 5
清单表, 47, 49
在属性上的, 603
对象, 614

# MethodInfo

方法, 417
对象, 617
`RuntimeMethodHandle`, 609
方法, 162
访问器, 228, 231, 247, 248
匿名类型和, 240
回调, 249
调用, 102, 103, 163
第一次调用, 111
第二次调用, 144
仅编译, 277
冲突解决, 170, 171
合约, 在抛出时维持, 483
转换运算符, 195
声明为常量, 224
声明返回类型, 223
已定义, 242
定义, 在
用于编码类, 355
用于枚举类型, 371
示例的, 163
显式, 和状态损坏, 476
显式接口方法实现
(ElMis), 303, 308, 310
扩展, 198, 255
泛型, 265, 270, 281, 283, 286
泛型与非泛型, 284
实例构造函数, 181, 184
接口, 调用, 302, 448
在从委托链中移除后调用, 255
标记为 async, 733
非虚 vs. 虚, 165
运算符重载, 191
`out` 和 `ref` 参数, 282
重载, 数量-, 286
覆盖, 172
重写, 299
参数.参见参数
参数类型, 214
部分, 204
传递可数量参数
到, 220
性能问题, 167
多态的, 166

# newobj 指令

- 公有的, 299
- 引用, 35
- 可靠性合约文档, 496
- 可靠的, 497
- 返回类型, 395
- 特定的与泛型的拆, 283
- 静态, 106
- 表, 301
- 线程安全, 759
- 将输入转换为事件, 256
- 元组类型和, 241
- 类型构造器, 187
- 类型参数，定义, 282
- 虚拟的，133, 169
- 虚拟的，更改为 override, 172
- 虚拟实例, 108
- WinRT, 646, 650
- `MethodWithReturn` 方法, 568
- Microsoft Silverlight ，其 AppDomains 和 574
- Microsoft Spy++, 683
- Microsoft SQL Server, AppDomains, 以及 575
- Microsoft Visual Studio, Checked 设置, 117
- Microsoft Windows NT 内核, 670
- 从 .NET Framework 版本迁移, 459
- `MinValue` 字段, 317
- `ModuleDef` 表, 39, 81
- `ModuleRef` 表, 39, 81
- 模块
- 构建类型到, 35
- 合并到程序集, 45
- 在友元程序集中, 156
- `Monitor` 类, 476, 794
- 常用方法, 795
- 示例代码, 796
- 将类型对象的引用传递到中, 798
- 相关问题, 798
- 作为静态类，避免, 798
- 监控
- `AppDomains`, 571
- 内存使用, 524
- 对象生命周期, 546
- `MPGO.exe`, 221
- `mscorEE.dll` 文件, 554
- `mscorLib.dll`, 35, 558
- `mscorWks.dll`, 554
- `msiexec.exe`, 61
- `MulticastDelegate` 类, 397
- 非公共字段, 398
- 多维数组, 385, 386
- 多个程序集, 46, 48
- 多核, 677. 另见 CPUs
- 处理器能力的, 682
- 利用, 682
- 线程饥饿在, 684
- UI 元素移除和, 682
- 用户效率, 682
- 多重继承, 295. 另见 interfaces
- 多线程操作系统, 684
- `MultiWebRequest` 类, 770
- 类, 780, 785
- 锁 (lock), 792
- 类型, 525
- 互斥锁, 785

# N

- 裸约束, 288
- 命名参数, 209, 424
- 参数，其求值顺序与, 210, 规则和指南, 211
- `NamedPipeServer` 类, 743
- 命名空间, 97
- 别名，创建, 99
- 程序集和, 101
- 创建, 100
- WinRT, 645
- 原生 C+, 659
- 原生资源
- 清理代码用于, 534
- 数量固定, 538
- 垃圾回收和, 525, 538
- 包装, 530, 532
- `NetworkStream` 对象, 355
- `new` 运算符, 92, 506
- `delete` 运算符和, 93
- 换行符, 322
- `NewLine` 属性, 322
- `NewMailEventArgs`, 253
- `newobj` 指令, 321, 845

# NGen.exe

- `NGen.exe`, 16, 19
- 知识产权和, 20
- `Normal` 标志, 546, 547
- 用于异常, 456
- 用于垃圾回收, 518, 523
- 用于线程附加/分离, 671
- 兴趣在于, 260
- 与泛型类型变量比较, 291
- 使用...初始化局部变量, 213
- 在 WRT 中, 647
- 可空类型, 288, 441
- 装箱 (boxing), 447
- 对 C# 的支持, 443
- 使用...调用接口方法, 448
- 对 CLR 的支持, 447
- 空合并运算符和, 446
- 运算符和，和, 444
- 重载运算符, 445
- 性能和, 445
- 解箱 (unboxing), 448
- 可空值类型, 646
- 数字类型，解析为, 348
- `NumberInfo` 类型, 343
- Numbers，枚举类型, 361
- `NumberStyles` 参数, 348
- 数字类型, 117. 另见
- 识别格式, 340
- `NumTimesAppearsEquals` 方法, 331
- `NumTimesAppearsInternal` 方法, 332
- 对象标识性，检查, 140
- 对象生命周期，手动控制, 545
- 面向对象编程 (OOP), 160
- `ObjectDisposed` 异常, 534
- `ObjectHandle` 类型, 595
- `ObjectInvariant` 方法, 502
- 对象
- 分配和初始化, 106
- 类型之间的转换, 93
- 损坏状态，避免, 228
- 创建, 92, 106, 596
- `Equals` 方法, 139
- 格式化, 344
- `GetHashCode` 方法, 1142
- 哈希码, 142
- 初始器, 235
- 不变性, 498, 501
- 引用封化, 564
- 类型, 23, 112
- `OnDeserialization` 方法, 629
- `OneManyLock` 类, 802
- 性能结果, 804
- `OneManyResourceLock` 类, 804
- `NewMail` 方法, 254
- `ThreadException` 方法, 488
- `op.Addition` 方法, 193
- 开放类型, 272
- `OpenAsync` 方法, 753
- `OpenExiting` 方法, 780
- 操作数，作为泛型变量, 292
- 操作系统不稳定性, 34
- `OperationCanceled` 异常, 652
- 操作
- 取消, 696
- 设置时间后取消, 700
- 调用方法后, 698
- 协作式取消, 696
- 防止取消, 698
- 运算符重载方法, 191
- 内部调用, 194
- CLR 的处理, 191
- 核心数字类型, 193
- 示例的, 192
- 命名规则, 194

# O

- 混淆器利用, 199
- `Object` 类, 296, 362
- 继承, 296
- 对象相等性, 139
- 检查, 140
- 属性, 141
- 对象图序列化, 614
- 序列化多个, 615
- 对象句，包装, 378

# ParseExact 方法

- 运算符，列表, 193
- 重载定义, 152
- 用于参数的, 191
- 支持, 191
- 不支持, 193
- 运算符
- 二进制, 192
- 检查和未检查, 116
- 空合并, 446
- 和可空类型, 444
- 一元, 192
- `op_Implicit` 方法, 197
- `op_Implicit` 方法, 197
- `OptimizedArray` 方法, 763
- 优化代码, 14, 277, 763
- 与 Volatile 类和, 765
- 可选属性, 212
- 可选参数, 209
- 参数，其求值顺序与, 210
- 规则和指南, 211
- `OrderedTaskScheduler`, 713
- 序数检查, 329
- `out` 关键字
- 基于方法的重载, 216
- 与 `ref` 关键字, 215
- `out` 参数, 282
- `OutOfMemory` 异常, 510
- 溢出，检查和未检查, 115
- 开销字段, 795
- 重载
- 数组基, 286
- 与可空类型和, 445
- 重载运算符.* 运算符重载
- `override` 方法, 172
- 覆盖方法, 299
- 线程锁的所有权, 791
- `Parallel LINQ`, 717
- 缓冲和合并, 720
- 并行处理查询, 719
- 跨越 CPU 核心的分区, 720
- 保持操作顺序, 718
- 顺序和并行查询, 717
- 提前停止查询, 719
- `ParallelEnumerable` 类, 717
- `ParallelLoopResult` 实例, 716
- `ParallelLoopState` 对象, 716
- `ParamArray` 属性, 221
- `ParamDef` 表, 39
- 带参数属性, 227, 242
- 从不支持的语言反序列化, 247
- 选择, 246
- `ParameterInfo` 对象, 602
- 无参数构造函数, 186, 235
- 无参数属性, 227
- 参数
- 定义常量, 224
- 定义类型, 214, 223
- 默认值，更改, 211, 212
- 用于索引器, 244
- 命名的, 209
- 可选的, 209
- `out` 关键字对比 `ref` 关键字, 215
- `params` 关键字, 221
- 引用传递, 215
- 通过方法传递, 214
- 方法中的类型, 214
- 类型的，接口, 306
- 验证, 366
- 变量，弱。强, 223
- `params` 关键字, 221
- `Parse` 方法, 348, 366, 370
- 异常处理, 493
- 重载, 349
- 参数, 349
- 性能和, 350
- 跳过空格, 348
- `ParseCombining`, 333
- `ParseExact` 方法, 349

# P

- 打包程序集, 60
- `Parallel` 类, 713, 714
- 性能问题, 714

# 解析

- 日期和时间, 349
- 字符串, 348
- `partial` 关键字, 159
- `partial` 方法, 204
- 效率的, 205
- 覆盖类型, 205
- `private` 关键字和, 207
- 用于类型的, 207
- 规则和指南, 207
- 运行时性能和, 205
- `sealed` 类和, 205
- 在 Visual Studio 中, 206
- 传递数组, 382
- 通过引用传递参数, 215
- 路径名称，加载程序集, 586
- 局部变量, 549
- PDB (程序数据库) 文件, 15
- PE (可执行文件) 文件
- 封存, 47
- 用于编译的开关, 47
- 组件的, 38
- 将资源文件嵌入到, 53
- PE32
- 文件, 6
- 头部, 38
- PE32 头部, 5
- `PerfMon.exe`, 524
- 性能5
- 性能计数器, 524
- 绑定句柄和, 608
- 上下文切换与, 672
- DLLs 和, 672
- 双重检查锁定和, 808
- 异常处理和, 492
- 执行上下文和, 695
- 超线程和, 567
- 实例字段和, 567
- I/O 操作和, 731
- 带有数量数量的方法, 222
- 使用任务管理器监控, 569
- `Parallel` 类和, 714
- 反射和, 589
- 任务和, 708
- 线程池和, 692
- 线程和, 670, 674, 681
- 线程同步和, 758
- 线程同步锁和, 790
- 性能监视，测试异常处理, 493
- PerView, 525
- 周期性计算密集型操作, 720
- PEVerifyexe, 186
- 固定标志, 546
- 钉住对象, 548
- 故障点，的, 471. 另见
异常: 异常处理

# 公钥与私钥

- 原始类型、溢出以及, 115
- 线程排序, 684, 754
- 按应用, 687
- 用于的类, 685
- 高优先级, 685
- 空闲优先级类, 685
- 空闲优先级级别, 687
- 重要性, 688
- 优先级映射, 686
- 优先级提升, 774
- 进程类, 686
- 提高和降低优先级, 687
- 实时类, 685
- 相对优先级类, 685
- 关键关键型优先级类, 687
- 用于 Windows Store 应用, 687
- 零页线程, 684, 686
- 排序Scheduling, 712
- 优先级
- 在反反转中, 756
- 线程, 697
- 私有程序集, 67
- 强名称, 79
- 私有字段, 168, 231
- 私钥。 见公钥与私钥
- 私有部署的程序集, 61
- 私有方法
- 部分方法作为, 207
- 序列化和, 622
- 类型构造函数, 188
- 私有线程锁, 797
- 问题签名, 487
- 进程类, 688
- 进程
- 创建, 扩展性本质, 675
- 创建，对比创建线程, 675
- 定义, 670
- 示例, 558
- 隔离, 557
- 进程优先级类, 686
- 降低, 使用托管代码, 177
- 终止, 477, 574
- 每个的线程, 674
- 浪费的, 识别, 675
- 处理器架构, 加载程序集的, 585
- `ProcessThread` 类, 688
- 错误处理中的生产力与可靠性, 469
- 程序顺序, 765
- 程序类型, 43
- 序言代码, 102
- 属性
- 访问器可见性, 248
- 访问器方法, 231
- 自动实现, 231
- 后备字段, 230
- 行为和, 248
- 编译器结果, 244
- 引起的混惑, 232
- C# 对的支持, 231
- 声明, 231
- 声明，在匿名类型中, 238
- 定义, 24, 152
- 绑定, 230
- 智能绑定, 232
- 示例, 229
- 泛型访问器方法, 248
- 元数据, 231
- 关于数据, 603
- 带参数的, 227, 246
- 无参数的, 227
- s 对公有字段, 425
- 返回不同的值, 233
- 线程同步和, 233
- 在 Tuple 类型中, 241
- Visual Studio 调试器和, 234
- 即使在使用时, 233
- `PropertyDef` 表, 39
- `PropertyInfo` 类型, 603
- 公钥与私钥
- 程序集, 67. 另见强名称, 命名
- 程序集
- 创建, 69
- 在 CSP 容器中, 78
- 延迟签名, 76
- 在硬件设备中，保护, 78
- 哈希以减少空间, 71
- 用于发布者策略程序集, 786

# 公有

- 公有
- 构造函数，定义, 195
- 字段，对比属性, 425
- 方法、接口和, 299
- 类型, 25, 154
- 发布者策略控制, 86
- 发布者策略 元素, 858
- 发布值, 808
- `Pulse` 方法, 813
- `PulseAll` 方法, 813
- 方法目的, xxiii
- 实时优先级类, 685
- 矩形，构造, 185
- 递归锁，避免, 806
- 递归线程锁, 786
- `ref` 关键字
- 基于重载方法, 216
- v. out 键, 215
- `ref` 参数, 282
- 引用计数, 508
- `ReferenceEquals` 方法, 140, 331
- 引用，检查, 157
- 元数据中的引用表, 39
- 引用类型变量，设置为, 288
- 引用类型，类型, 118, 320
- 它们的数组, 373
- 类作为, 119
- 将值类型转换为, 125
- 示例代码, 121
- 示例, 119
- 字段布局, 123
- 泛型, 269
- 空合并运算符和, 446
- 与值类型重叠, 124
- 性能问题, 119
- 作为主要约束, 287
- `ref` 关键字 对比 out 键, 215
- 序列化, 618
- 共享代码, 277
- 交换, 218, 219
- 与类型构造函数, 188
- v. 值类型, 122
- 引用
- 程序集, 70, 98
- 强名称程序集, 74
- 类型, 80
- 反射, 141, 148, 430
- 发现成员, 599
- 异常处理和, 485
- 对象模型，发现, 602
- 性能问题, 589
- 序列化和, 614
- 类型发现与, 590, 604
- 类型安全, 589
# Q
- 排序函数, 391
- 量子, 672
- 提前结束, 673
- 查询，LINQ. 见 LINQ
- `QueueNotification`, 519
- C# 代码中的问号, 443
- 队列，线程安全的, 813
- `QueueWorkItem` 方法, 409, 693, 700, 724

# R
- 触发事件，线程安全的方式, 254
- 理性类型, 195
- RCWs (运行时封装器), 453
- `Read` 方法，在 I/O 操作中, 728
- `Read` 方法 (`volatile`), 765, 767, 768
- 只读文件，设置, 368
- `ReadAsync` 方法, 729, 733, 753
- `ReadBlock` 方法, 742
- `ReaderLock` 类, 802
- 读写锁, 801
- `ReaderLockSlim` 方法, 800
- `ReadLineAsync` 方法, 742
- `ReadToEnd` 方法, 342
- 只读字段, 177
- 定义, 178
- 实时操作系统, 684

# 序列化
- .NET Framework 反射 API, 583
- 反射成员，泛型和, 271
- 反射命名空间, 431, 588
- 反射类型, 588, 589
- 层次, 600
- `ReflectionOnlyGetMethod`, 591
- `ReflectionOnlyLoadFrom` 方法, 587
- `ReflectionOnlyLoad` 方法, 587
- 区域设置, 326
- `CancellationToken` 类, 699
- `CancellationSource` 类, 698
- `RegisterForContention` 方法, 523
- 注册程序集, 74
- 关系运算符，可空类型和, 444
- 相对优先级类, 685
- `ReleaseMutex` 方法, 785
- 可靠Monitor 特性, 496
- 问题设置, 487
- 错误处理中的可靠性对比生产力, 469
- `Remove` 方法, 230, 308
- `RemoveEventHandler` 方法, 359
- `RemoveMemoryPressure` 方法, 538
- `RemoveParticipant` 方法, 805
- `Replace` 方法, 338
- `ReportStatus` 方法, 772
- `ResetAbort` 方法, 579, 580
- 解析类型, 593
- 资源文件，添加, 539
- 资源泄漏, 531
- 资源，访问, 505
- 响应文件, 36
- 存活的对象, 544
- 返回类型，发现信息, 402
- 返回数组, 382
- 反向工程，防止, 19
- 根, 508
- 垃圾收集, 509
- `Run` 方法, 745
- 运行时
- 绑定器, 148
- 句柄, 608
- 运行时封装器 (RCWs), 644
- `RuntimeException` 类, 478
- 安全位置, 580
- `SafeHandle` 类, 527
- 派生, 528
- `SafeHandle` 命名空间, 529, 530, 531
- `SafeWaitHandle` 类, 529
- 卫星程序集, 59
- `sbyte` 类型, 112
- 可扩展性，线程和, 674
- 调度任务, 711
- 读/写语义, 815
- 调度线程, 683, 684
- 密封类, 168
- 部分方法和, 205
- 次级约束, 288
- `SecureString` 类, 357
- 解密对象, 360
- FCL 支持, 358
- 将对象作为密码传递, 358
- 安全字符串, 357
- 安全，类, 168
- `SecurityCritical` 特性, 489, 695
- 安全设置，线程池和, 694
- `Semaphor` 类, 780, 784
- 信号量, 784
- v. 自动重置事件, 784
- 同步构造结构, 778
- `SemaphoresSlim` 类, 794, 815
- 顺序查询, 717
- 序列化, 589
- `AddValue` 方法和, 627
- 状态, 616
- 组装和, 616
- 使用克隆, 615
- 集合对象, 622

# SerializationBinder 类

- 序列化（继续）
- 控制, 619
- 控制数据, 624
- 类型转换, 728
- 定义, 730
- 定义, 711
- 格式性, 520
- 实例类型, 519
- `ISerializable` 接口, 625, 630
- 匹配反序列化, 628
- 多个对象图, 615
- 命名空间, 623
- .NET 框架支持, 612
- 对象图, 614
- 存活的对象, 522
- 实例类型, 633
- 特殊构造函数类型, 628
- 流内容, 631
- 代理选择器, 639
- 类型, 625
- XML 流, 612, 614
- 避免, 619
- `SerializationBinder` 类, 640
- `SerializationException` 类, 615, 616, 618, 622
- `SerializeTo` 方法, 714
- 运行时垃圾收集, 520
- 异步实现, 751
- 服务的, 161
- `SetAt` 方法, 358
- `SetMaxThreads` 方法, 724
- `SetMinThreads` 方法, 724, 726
- `SetType` 方法, 626, 635
- `SetValue` 方法, 603
- 并行类和, 714
- `shim` DLL, 554
- 短类型, 112
- `SignalAndWait` 方法, 805
- 签名数据类型, 117
- 签名文件, 70
- Silverlight 应用
- `AppDomains` 和, 574
- 运行在, 687
- 序列化，线程方法, 748
- `SimpleHybridLock` 方法, 793
- `SimpleSpinLock` 方法, 773
- `SimpleWaitLock` 方法, 782, 784
- 简化应用, 682
- `SimulateNewMail` 方法, 256
- 单一维度数组, 375
- 单实例应用, 781
- 单例类, 809
- 单例类型的序列化, 633
- `Sleep` 方法, 774
- `SN.exe`, 68
- 延迟签名使用, 77
- `Soap` 命名空间, 614
- `SoapFormatter`
- 类, 614
- 对象, 614
- 软件发布者数字 ID 用于
- 身份验证, 488
- `SomeMethod` 方法, 565, 566
- OS 调试扩展, 525
- 源码
- 编译, 3
- 在之间拆分, 159
- 保护, 267
- 源码控制, 159
- 自旋锁, 773. 另见线程同步
- 自旋循环，线程让出 CPU 和, 775
- `SpinLock` 方法, 775
- `SpinLocks`, 818
- 旋转的线程，使用混合锁, 791
- `SimpleWait` 方法, 774
`Spy++`, 683
- SQL Server, `AppDomains` 和, 575
- `stackalloc` 语句, 388
- `StackOverflowExceptions`, 497

strings
栈空间 (stack space), 102
检查, 489
堆栈跟踪 (stack trace), 461, 462
已完成, 462
构造, 462
解释, 463
`StackTrace` 属性, 461
`Start` 方法 (`Thread` 类), 679
`StartNew` 方法, 710
`StartsWith` 方法, 比较字符串, 325
启动时间, 改进, 19, 21
线程饥饿, 684
状态损坏
销毁, 476
异常处理， 以及 477
`FailMethod`, 480
托管代码， 以及 477
缓解, 475
终止进程, 477
状态机, 返回模型, 749
无状态编码和解码, 356
语句, 检查的和未检查的, 116
静态类, 158
静态构造函数. 见类型构造函数
在泛型类型上定义, 273
静态事件, 152
静态字段, 177
定义, 178
初始化, 189
内存泄漏及, 510
静态成员
接口和, 297
`MarshalByRefObject` 类以及, 567
静态方法
对于数组, 380
调用, 106
回调, 使用委托程序, 394
调用运算符重载方法, 带有 194
对于 `Char` 类型, 318
`nextension` 特性, 203
`Finalize` 方法以及, 526
对于`Int32` 变量, 768
线程安全, 759, 760
`volatile` 关键字, 767
`StaticDelegateDemo` 方法, 394
`Stop` 方法 (`Parallel` 类), 716
序列化的流式上下文, 631
`StreamReader` 类型, 350
流 (streams), 656
`StreamWriter` 类型, 350, 537
最终化及, 538
`String` 类
哈希表, 计数, 330
方法, 338
密封的 (sealed), 323
字符串池 (string interning), 329
`String` 对象. 见 strings
不可变性, 569
`String` 类型, 112, 320
构造, 320
接口和, 300
由方法重载定义的, 325
作为原生类型类型, 320
`StringBuilder` 类, 198, 345
创建对象, 366
成员, 337
方法, 338
`StringBuilder` 类型, 336
`StringComparer` 类, 329
`StringComparison` 类型, 324
`StringInfo`, 333
strings
base-64 编码/解码, 356
更改其中字符的大小写, 325
字符数组, 337
字符, 检查, 333
克隆, 335
比较, 323
连接 (catatenating), 322
构造, 320
高效构造, 336
转换为字节, 353
将 Unicode 转换为 MBCS, 350
复制, 335
自定义格式化器, 345
日期格式化, 341
安全地删除, 358
编码, 350
格式化, 344, 346
将多个对象格式化为, 344
不可变性, 323
池化, 329
将枚举类型映射到, 364
在元数据中, 332
数字格式化, 341
作为对象表示, 339
解析, 348
池化, 332
安全的, 357
在源代码中, 321
用途, 324
字面面量 (verbatim), 322
WinRT, 647
优化, 795
公共索引, 797
关系, 795
类型对象和, 795
同步上下文任务调度器, 711
`SynchronizationContext` 类, 749
同步线程. 见 thread
同步
同步 I/O 操作, 752. 见 I/O 操作
`FileStream` 对象以及, 753
System Monitor器, 524
System 命名空间, 22, 23
System.Collections.Generic 命名空间, 270
System.Decimal 类型, 118, 198
System.Diagnostics.ConditionalAttribute
强名称工具 (SN.exe), 68
强命名程序集
特征, 66
组件, 68
压缩, 74
创建, 67
全局部署, 72
私有部署, 79
获取其密钥, 68
引用, 74
安全性, 76
抗篡改性性, 75
唯一标识, 67
验证, 76
特性 (attribute), 206
System.Exception 类, 状态损坏和, 474
类型, 460
SystemException 类型, 466
System.InvalidCastException 类型, 95
System.Object 类型, 26, 91
delete 操作符, 93
new 操作符, 92
受保护方法, 92
公共方法, 92
System.Reflection.AssemblyName 类, 68
System.Runtime.ProfileOptimization 类, 16
System.namespace, 97
System.Type 对象, 类型指针, 110
结构化异常处理 (SEH), 453. 见 exceptions; handling.
Substring 方法, 335
SubstringElements, 333
SuppressMessage 特性, 440
Surrogate 对象, 639
用于序列化的代理类型, 336
Unicode 元素, 333
挂起线程, 774
同步块, 794
索引, 105
初始化, 795
Task 类
FromAny 方法, 822
与线程同步, 814
Task Manager, 670, 675
监控性能, 675
Task 对象, 701
数组, 710
字段, 707
ContinueWith , 705
创建标志, 701
CurrentId 属性, 708
释放, 708
工厂, 709
Int32 字段, 708
状态, 708
查询, 708
辅助状态, 707
WaitingForActivation 状态, 709
TaskFactory 类型, 709, 710
TaskLogger 类, 738
任务, 700
取消, 704
CancellationToken 对象, 带有 705
子任务, 707
组合, 707
构造函数和, 201
死锁情况, 702
延迟, 722
委托程序, 传递, 715
异常检测, 703
抛出的异常, 704
性能问题和, 708
读取/写语义, 815
返回 void, 使用 709
在任务完成时自动启动, 705
状态, 707
辅助状态, 707
同步上下文任务, 711
任务调度器, 711, 712
与线程同步, 807
处理的异常, 702
唯一 ID, 708
等待完成, 702
Tasks 命名空间, 651, 700, 709
TaskScheduler 对象, 711
TaskScheduler 类型, 派生自, 712
TEB (线程环境块), 671
临时变量, 284
已终止应用程序, 在 Reliability Monitor 查看
终止进程, 477, 574
文本元素. 见 characters
TextElementEnumerator 方法, 333
线程阻塞, I/O 操作和, 731
Thread 类, 668
线程环境块 (TEB), 671
线程内核对象, 671
线程锁, 异步函数和, 734
线程池, 692
异步调用方法, 693
子任务, 707
在其中继续任务, 705, 707
死锁情况, 724
延迟任务, 792
执行上下文, 695
启发式性质, 692
限制线程数量, 724
并行性能, 713
并行处理, 抛出异常时 716
性能和, 692
处理顺序, 725
在队列中, 693
调度方法调用, 720
在其中调度任务, 712
安全设置和, 694
顺序方法执行, 713
线程管理中, 723
线程同步锁和, 725
工作线程管理, 724
在工作项中, 693
线程优先级, 754
线程安全集合类, 818
队列, 813
线程安全, 759
线程同步异步函数和, 757
异步, 814
自动重置事件和, 782
避免, 759
# ThreadAbortException 异常
阻塞, 避免, 805
阻塞计数器, 804
类库和, 759
条件变量模式, 811
构造结构, 805
双检查锁定, 807
缺点, 757
异常处理和, 476
混合, 790
混合构造结构, 创建构造结构
活锁和死锁, 761
lock, 189
锁, 476, 725
锁扩展性, 814
m_opCount 字段, 772
Mutex 对象, 786
并行执行, 805
性能问题, 758
基本构造结构, 760
优先级提升, 禁用, 774
私有锁, 797
属性和, 233
读取/写锁, 801, 804
递归锁, 786
递归锁, 避免, 806
指定同步对象, 811
自旋锁逻辑, 774
自旋锁, 773
任务对比., 807
让出线程时, 775
ThreadException 异常, 580
线程事件, 488
线程模型, 748
Threading 命名空间, 695, 720, 778

# 类型参数

- 可扩展性, 674
- 调度, 683, 684
- 开始, 679
- 饥饿, 684
- 挂起, 774
- 关键时间优先级级别, 687
- 时间片, 672
- 用户模式栈, 671
- Windows Store 应用，已移除的 API, 678
- 线程模型, 748
- 线程优先级排序以及, 687

## 线程

SharingData 类, 766, 767

- ThrowCancellationRequested 方法, 704
- 抛出异常, 466. 另参见异常:
  - 异常类型
  - 关键时间优先级级别, 687
  - 时间片, 672
- 提前结束, 673
- Timer 类, 720, 723
- Timer 对象的垃圾回收, 721
- timer 命名空间，Timer 类, 723
- ToArrayInvariant 方法, 318
- ToObject 方法, 367
- 撕裂读, 762
- ToSingle 方法, 310
- Tostring 方法, 134, 238, 318, 335, 337, 339, 364, 365, 569
  - 数字格式化, 341
  - 输出格式, 369
  - 输出, 364
  - 重写, 339
  - 无参数, 340
  - 参数, 340
  - 与 Format 方法对比, 364
- System.Object, 92
  - ToString, 格式字符串为 null, 341
- ToUpperInvariant 方法, 318
- Transaction 类, 797
- TransactionScope 类, 475
- 触发垃圾回收, 519
- try 块, 454. 另参见 catch 块；finally 块
  - 作为回调方法, 497
  - 约束执行区域和, 475
  - finally 块和, 457
  - 线程和, 671
- TryParse 方法, 366, 370, 493
  - 异常处理与, 494

 元组 (Tuple)

- 类, 241
  - 类型, 237, 240
  - 属性和, 241
- 类型参数, 266
- n-类型构造函数, 187
  - 调用, 188
  - 避免按顺序调用, 189
  - 默认, 187
  - 已定义, 151
  - 定义, 188
  - 避免在值类型内部定义, 189
  - 使用其初始化单例对象, 189
  - 内部相互引用, 189
  - 命名规范, 190
  - 私有, 188
  - 线程同步锁, 189
  - 未处理的异常, 189
  - 类型定义示例, 153
- 类型推断
  - 泛型方法和, 283
  - 概述, 283
- 类型对象指针, 105
- 类型对象, 591
  - 转换为 RuntimeTypeHandle, 609
  - 转换为 TypeInfo 对象, 592
  - 针对泛型类型, 272
  - 获取, 591
  - 从编译时的类型名称获取, 592
  - 开放，创建, 272
  - sync 块和, 795
- 类型参数, 266
- 约束到接口, 305
- 约束, 287, 288
- 构造函数的对比, 289
- 逆变型与协变, 279
- 泛型, 281
- 命名规范, 266
- 重写方法和, 286
- 变性与, 280

# 类型安全语言

- 类型安全, 219, 267
  - 接口和, 308, 309
  - 保护, 277
  - 反射和, 589
- 泛型类型变量, 290, 291, 292
- typeDef 表, 39
- TypeInfo 类, 602
- TypeInfo 对象, 592
  - 查询, 593
- typeInfo 对象, 592
- typelex 指令, 17
- typeof, 429, 592
- typeRef 表, 40
- 类型, 24. 另参见 CTS (公共类型系统)
  - 跨程序集, 597
  - 作为 和 is, 596
  - 别名，创建, 99
  - 模糊引用, 99
  - 匿名, 237, 238, 239
  - 元数, 273
  - 程序集, 25
  - Backus-Naur 语法，用于 592
  - 构建到模块, 35
  - 使用 is/as 操作符进行强制转换, 95
  - catch, 456
  - 通用属性和方法, 602
  - 实例化, 594
  - 转换, 628
  - 之间的转换, 195
  - 为其创建对象, 596
  - 内部数据字段, 105
  - 声明, 214
  - 定义, 35, 105, 251
  - 消除歧义, 99
  - 发现成员, 599, 604
  - 动态构建, 590
  - 枚举, 361
  - 穷举, 588
  - 示例定义, 28
  - 异常, 463, 466
  - 异常派生的层级, 593
  - 带有事件, 250
  - 外部, 35
  - 字段布局, 123
  - 通用格式, 341
  - 泛型, 255, 266, 279, 274, 596
  - 泛型标识标识, 275
  - 泛型接口, 278
  - 帮助文档, 310
  - 助手, 169
  - 从表达式中推断, 212
  - 初始化静态字段, 189
  - 调用成员, 603
  - 与关键字对比, 113
  - 针对泛型的限制, 285
  - 链表, 274
  - 监听事件, 258
  - 字面量, 114
  - 位置, 81
  - 成员可访问性, 156
  - 成员, 24, 151
  - 方法表, 301
  - 程序集间的移动, 83
  - 命名空间, 97, 99
  - 命名规范, 273
  - 可空类型, 441, 443, 445
  - 基于元数的重载, 286
  - 部分, 159
  - 性能问题, 167
  - 原始类型, 111
  - 属性, 593
  - 公共, 25, 154
  - 查询, 600
  - 识别格式, 340
  - 引用, 118
  - 被引用的程序集, 98
  - 引用, 35
  - 反射, 588, 589, 600
  - 解析, 593
  - 决议, 80
  - 限制访问, 25
  - 返回名称, 339
  - 运行时句柄, 608
  - 安全性, 95
  - 序列化, 617, 618, 620
  - 有符号的, 117
  - 单例, 633
  - 代理，用于 636

# 值类型

- SystemObject 派生, 91
- Tuple, 237, 240
  - 唯一名称, 99
  - 未卸载, 191
  - 值, 118, 277
  - 可见性, 154, 166
  - Visual Studio 提示信息, 234
  - WinRT, 646
  - 互操作性, 449
  - 无实例构造函数, 182
  - 非托管回调函数, 391
  - 非托管 C++ 编译器和, 2
  - CLR 互操作性与, 30
  - 性能与托管对比, 15
  - 未观察的事件, 703
  - 取消方法, 260
  - 不安全代码, 17
  - 不安全修饰符, 388
  - Load 方法, 586
  - 方法, 595
  - 大写/小写之间的转换, 318
  - Uri 类型, 648
  - UI 元素，移除, 682
  - int 类型, 112
  - long 类型, 112
  - 一元操作符, 192
  - 可空类型和, 444
  - 可空类型, 448
  - 值方法, 135
  - 装箱和拆箱, 124, 126
  - 装箱和拆箱, 124, 126
  - 调用虚方法, 133
  - 修改字段, 136
  - 复杂度, 138
  - 构造函数, 184
  - 转换为引用类型, 125
  - 默认构造函数, 186
  - 定义, 132
  - 在...上定义构造函数, 185
  - 避免在...中定义构造函数, 818
  - 示例代码, 121
  - 示例, 119
  - 字段布局, 123
  - 不变性, 138

# 值类型（继续）

- 虚实例方法, 108
- 初始化字段, 187
- 虚方法, 163, 165
- 接口方法，用于 319
- 调用, 133
- 接口和, 301, 299
- 调用指令，用于 165
- 原生代码，用于 277
- 构造函数方法和, 182
- 可空类型, 441, 443, 646
- out 关键字对比 ref 关键字, 215
- 最小化, 166
- 与引用类型重叠, 124
- 性能, 167
- 与引用类型对比, 122
- 安全性, 168
- 序列化, 618
- 版本控制与, 169
- 带有类型构造函数, 188
- 可见性，类型，是 154, 166
- 拆箱和字段拷贝, 127
- Visual Studio 可验证性, 186
- 调试器和属性, 234
- 调用虚方法, 165
- 异常调试, 490
- 何时使用, 121
- 异常，添加到调试器, 491
- WinRT, 646
- 异常对话框, 490
- ValueType 类, 362
- IDE，使用...添加程序集, 51
- var 关键字, 237
- IntelliSense, 在, 206
- 与 dynamic 对, 146
- 使用...发布应用, 61
- 与 dynamic 关键字对比, 214
- 由于多核导致的速度, 682
- 变量
- 目标平台，设置, 8
- 可克隆, 301
- 提示信息，查看, 214
- 隐式类型, 212, 237
- volatile
- 使用 null 初始化, 213
- Windows Runtime 组件项目, 659
- 接口类型, 300
- 临时, 284
- 类, 765, 767, 768, 773, 805, 808
- 变性限制, 280
- 字段, 177
- 向量, 375. 另参见数组
- 关键字, 767
- 逐字字符串, 322
- volatile 构造, 762, 766
- 验证
- 泛型的验证, 284
- C# 支持, 767
- 泛型和, 290
- 缺点, 767
- Volatile.Read, 254
- IL 和, 16

# Wintellect Power Threading Library

- 命名弱的程序集，66, 68
- 仅限私有的部署，67
- WeakReference 类，549
- WeakTrackResurrection 标记，546, 549
- WebClients, 异步函数，以及 744
- 网络下载的程序集，586
- Web Forms, 异步，751
- WhenAll 方法，747
- WhenAny 方法，747
- Windows, 抢占式多线程操作系统，684
- Windows Action Center, 查看未处理的异常，486
- Windows Error Reporting，488
- Windows Forms, 线程模型，748
- Windows Installer 服务，661
- Windows NT 内核，670
- Windows Presentation Foundation (WPF), 线程模型，748
- Visual Studio 中的 Windows Runtime Component 项目，659
- Windows 调度器，异步操作以及，694
- Windows Store 应用，36
- 用 C# 实现的 WinRT 组件，659
- 移除了 ithread APIs，678
- 线程模型，748
- 线程优先级排序以及，687
- WinRT 组件，643
- WindowsRuntimeBuffer 类，658
- WindowsRuntimeBufferExtensions 类，657, 658
- WindowsRuntime 指令，657
- WindowsRuntimeStorageExtensions 类，654
- WindowsRuntimeSystemExtensions 类，653
- WindowsRunTime (WinRT)，31。参见 WinRT
- WinMDExp.exe，659

## WinRT
- 数组，648, 660
- 调用异步 APIs，649, 653
- 基类型，645
- 取消 APIs，653
- 类，646
- 集合，648
- 核心概念，645
- 日期和时间，647
- 委托，647
- 枚举类型，646
- 事件，647
- 异常，647
- 显式调用方法，648
- 由……暴露的功能，643
- 文件名和命名空间，645
- 框架投影，649
- IAsyncXX 类，651
- 将 IAsync 方法转换为 .NET Framework Task 方法，654
- IBuffer 接口，656
- IClosable/Disposable 接口，648
- 接口，642
- JavaScript 示例代码，664
- 将 CLR 类型映射到，659
- 将内存地址传递给 CLR，656
- 元数据，659
- 方法，640, 650
- .NET 互操作性，654
- 可空值类型，646
- 将数据块传递给 CLR，656
- 属性，647
- StorageFile，转换为 .NET XElement，655
- 字符串，647
- 结构，646
- 类型系统，646
- 类型系统互操作性，649
- URIs，648
- 值类型，646

## WinRT components
- CLR 投影以及，645
- 作为 COM 组件，644
- 在 C# 中定义，658
- FCL 类型以及，644
- 文件扩展名，644
- 作为托管组件，660
- 由……使用的元数据，644
- 多态以及，646
- 类型系统，645
- 用于 Windows Store 应用，659
- WinRTAsyncSync 方法，650
- Wintellect Power Threading Library，690

## WithCancellation method
- WithCancellation 方法，719, 751
- WithMergeOptions 方法，720
- 线程池中的工作项，693
- Worker 方法，764
- 工作站垃圾回收模式，520
- WoW64 技术，9
- 封装原生资源，530, 532
- Write 方法，131, 345
- 抛异常，534
- Write 方法 (Volatile 类)，765, 767, 773, 808
- WriteAsync 方法，742
- WriteLineAsync 方法，342
- WriteLine 方法，130, 131, 138, 164, 345, 385

## X
- Xml 命名空间，DispatcherTimer 类，723
- XML 配置文件。参见配置文件
- XML 元素，转换。195
- XML Web 服务应用程序，AppDomains 以及，575
- XmlSerializer 类，612

## Y
- Yield 方法，775

## Z
- 零基索引数组，374
- 零长度数组，382
- 零页线程，684, 686

## 关于作者

JEFFREY RICHTER 是 Intellect (http://www.Wintellect.com/) 的联合创始人，这是一家培训和咨询公司，致力于帮助公司更快地产出更好的软件。Jeffrey 编写或合写了许多关于 Microsoft .NET Framework 和 Win32 编程的书籍，包括 Intellect's CLR via C# 第四版（Microsoft Press, 2012）、Windows via C/C++ 第五版（Microsoft Press, 2007）以及 Programming Server-Side。
