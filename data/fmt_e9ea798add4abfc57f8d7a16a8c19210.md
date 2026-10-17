
## 第 13 章 I/O：示例

尽管 Swift 内置的懒性集合似乎可能消除了自定义代码的需求，但事实并非如此：Swift 的标准库并没有实现真正的懒性行为（即在计算结果后对其进行缓存）。相反，它每次访问时都会重新计算，除非整个集合一次性转换为非懒性集合，而这正是我们试图规避免的。

将该示例应用于我们的单词列表示例，效果是显著的：从属性初始化单词的时间从 756 ms 降到 26 ms，提升了 29 倍，使得这种变体比我们之前使用的初始化整个单词列表更快。图 13.3 显示了所有时间。

不过，我们对懒性变体必须稍微小心一点，因为如果我们进行线性搜索，当项目被检索时，所有的懒性都会消失，导致我们在意料之外的时间花费 700+ 毫秒。为了避免这种情况，我们需要将搜索从使用 `indexOfObject:` 的线性搜索切换到使用 `indexOfInSortedRange:options:usingComparator:` 的二分搜索，并带有 `BinarySearchingFirstEqual` 选项。

二分搜索在每次搜索期间只会加载 n 个项目，对于提到的 26K 单词列表，每次搜索大约解码 15 个项目。

![](img/29111a88ed1326b01d04057a653fdbec_297_0.png)

图 13.3 包含懒性属性列表的 iPhone 游戏字典加载对比

## 避免中间表示

现在我们已经有了自己的属性列表，第 12 章的另一个问题浮现在脑海：属性列表读取之所以缓慢且耗费内存，部分是因为我们必须为对象图创建一个临时但完整的内存表示，即作为字典、数组和 Foundation 数字对象的表示。

从我们自己的属性列表中反归化 `SampleObject` 的代码见示例 13.11。

### 示例 13.11 无中间表示的列表反归化

```objc
(instancetype)initWithBinaryPlist:(MPWBinaryPropertyList*)aPlist
{
    if (self=[super init]) {
        [plist parseDictUsingContentBlock:^(MPWBinaryPropertyList*)plist
```

这与键值对归档代码非常相似，只是解码字典和数组等复合对象的代码被封装在块内部。这种差异的原因是，与键归档不同，普通的属性列表不存储任何关于对象类的信息。在归档中，类信息存储在归档中，并由反归化器实例化正确类的对象，然后调用 `initWithWithCoder:` 消息。相反，我们必须将解码特定字典或数组的知识传递给解码它们的方法。

将该示例应用于我们的单词列表示例，效果是显著的：从属性初始化单词的时间从 756 ms 降到 26 ms，提升了 29 倍，使得这种变体比我们之前使用的初始化整个单词列表更快。图 13.3 显示了所有时间。

不过，我们对懒性变体必须稍微小心一点，因为如果我们进行线性搜索，当项目被检索时，所有的懒性都会消失，导致我们在意料之外的时间花费 700+ 毫秒。为了避免这种情况，我们需要将搜索从使用 `indexOfObject:` 的线性搜索切换到使用 `indexOfInSortedRange:options:usingComparator:` 的二分搜索，并带有 `BinarySearchingFirstEqual` 选项。

二分搜索在每次搜索期间只会加载 n 个项目，对于提到的 26K 单词列表，每次搜索大约解码 15 个项目。

![](img/29111a88ed1326b01d04057a653fdbec_297_0.png)

图 13.3 包含懒性属性列表的 iPhone 游戏字典加载对比

## 避免中间表示

现在我们已经有了自己的属性列表，第 12 章的另一个问题浮现在脑海：属性列表读取之所以缓慢且耗费内存，部分是因为我们必须为对象图创建一个临时但完整的内存表示，即作为字典、数组和 Foundation 数字对象的表示。

从我们自己的属性列表中反归化 `SampleObject` 的代码见示例 13.11。

## 逗号分隔值

我和学生考虑的另一种用于启动数据的编码方案是 CSV，但我们从未付诸行动，因为我们使用懒性属性列表列表（lazy property list）已经取得了良好的结果。很久以后，我才正式开始处理 CSV 文件，那是一个由客户提供的包含 16,000 条记录的 25-MB 数据库转储文件，用于将其格式化为电话簿。由于 Mac OS X 内置了高质量的 PDF 生成功能，现在此类数据库发布任务可以使用 Cocoa 程序完成，而无需通过像 Adobe InDesign 或 Quark XPress 这样大型且缓慢的第三方应用程序。

然而，普通的复杂的链接-调试循环交互性不足，无法处理图形化调整，因此我想从我编写的实时编程环境（live-programming environment）中访问这些数据。在实时编程环境中，显示会在每次按键后更新，程序求值时间必须远少于 100 毫秒以保持交互体验。然而，我使用的基于 Scanner 的代码处理该文件需要 4.8 秒。在两次按键之间等待 4.8 秒会让体验失去“实时性”，因此这并不是一个可行的方案。

回顾本章开头的数据字典，我们看到，如果使用基本的 C-String 处理将文件拆分为行是非常快的，而且一旦我们能够访问行索引，就可以按任何顺序访问单独的，而无需按顺序处理它们。凭借此和基础性能方程中的项*成本（cost）*，我们有了解决方案：只读取显示可见目录部分所需的条目（可能只有一个或两个），而不是全部 16,000 条条目。

这个特定数据集足够简单，`componentsSeparated` 方法就足以解析单行并将它们转换为字典（示例 13.13）。所有 16,000 条条目的总时间仅下降到 1.5 秒——仍然太慢了，但每条目的的时间为 98 μs，且每页约 200 条，这意味着数据读取时间仅为 20 ms——这已经足够快了，无论是整体还是读取时间，都被渲染时间所击败。

### 示例 13.13 简易 CSV 读取器

```objc
- (NSString*) lineAtIndex(int anIndex)
{
    int *offsets=[lineOffsets] integers;
    int offset=offsets[anIndex];
    int nextOffset=offsets[anIndex+1];
    int len = nextOffset-offset-[self eolLength];
    return [subdataWithStart:bytes+offset length:len ];
}
```

- 4. 记录很大：有 133 个字段，每条记录平均 1.3 KB。
- 5. http://www.cocoawithlove.com/2009/11/writing-parser-using-scanner.html

```objc
- (NSDictionary*) dictionaryAtIndex:(int) anIndex
    return [NSDictionary
            dictionaryWithObjects:[self lineAtIndex:anIndex]
            componentsSeparatedByString:fieldDelimiter
            forKey:[self headerKeys]];
```

我们略微损失了处理速度这一事实在很大程度上无关；重要的部分是提供随机访问，以便我们可以解析所需的条目。

## 公共交通时间表数据

CSV 带来的另一个大问题是以公共交通时间表数据的形式出现的，为了回答这个问题：“使用公共交通我附近有哪些出行选择？”这个问题所需的数据包括附近站点的位置以及距离这些站点的时刻差。柏林的公共交通公司 Berliner Verkehrsbetriebe (BVG) 以 Google 的通用传输馈送规范 (GTFS) 格式提供这些数据。一个 GTFS 馈送由包含 CSV 文件的压缩包组成；BVG 馈送的文件如图 13.1 所示。它们代表了服务的站点、存在的线路以及特定线路服务于站点的具体时间。

对于当前的问题，感兴趣的数据位于 `stops.txt` 和 `stop_times.txt` 文件中，其提取部分在示例 13.14 中。正如你可以想象的（并在表 13.1 中验证），最大的集合是描述所有站点时间的那个；它重量为 118 MB，包含 300 万条条目。

### 示例 13.14 站点和时间数据

```
stop_id,stop_code,stop_name,stop_desc,stop_lat,stop_lon...
903001,U Hansaplatz (Berlin),52.518111,13.342165...
903002,S Bellevue (Berlin),52.5197640,13.349619...
903003,S Tiersgarten (Berlin),52.514400,13.336490...
903004,U Turstr. (Berlin),52.5258370,13.3424010...

trip_id,arrival_time,departure_time,stop_id,stop_sequence...
18:16:00,18:16:00,906310...
18:18:00,18:18:00,906364...
18:19:00,18:19:00,906311...
18:21:00,18:21:00,906365...
```

> 6. https://developers.google.com/transit/gtfs/reference

## 第 13 章 I/O：示例

表 13.1 柏林的主要 GTFS 文件

| 文件 | 内容 | 大小 | 行数 |
| :--- | :--- | :--- | :--- |
| routes.txt | 公交、电车和地铁 | 37 KB | 1.3K |
| stops.txt | 站点列表 | 75 KB | 13K |
| stop_times.txt | 所有站点的时刻 | 118 MB | 3M |
| transfers.txt | 线路间的换乘 | 330 KB | 13K |
| trips.txt | 每条线路可能有不同的行程 | 7.5 MB | 152K |

objc.io 的 Issue 4 为 iOS 提供了一个解决方案，以及一个从 GTFS 文件预填充 SQLite 数据库的导入器。示例 iOS 程序显示纯位置搜索和时间搜索的时间（毫秒）：3.6、3.2、2.5（位置+时间）、3.8、4.1、6.5、7.9（位置）。对于位置搜索大约 3 ms，我们希望尽可能获得即时反馈（100 ms 或更短）。此外，离线导入器在 MacBook Pro 上需要超过 2 分钟才能将 `stops.txt` 和 `stop_times.txt` 文件转换为 SQLite 数据库。数据库大小超过 120 MB，这取决于数据是包含在应用中（使应用相当敏捷）还是下载。让我们看看是否可以做到这一点。

## 站点

该文件仅包含 13,000 条条目，我们可以在启动时轻松地将其读入内存中的 `StopList`，其中包含一个 `BusStop` 数组。每个 `BusStop` 都有文件中的纬度和经度，以及名称和 ID。读取 CSV 的速度足够快，我们可以直接保留文件，而不转换为其他格式，只需花一点时间对 CSV 读取进行增强。

我们使用 `CLLocation` 通过 `distanceFromLocation` 获取精确距离比较；尽管该方法非常准确，但每次搜索需要 3.3 ms 且内存密集，每次站点搜索都需要初始化 `CLLocation`。我们可以使用 k-d树等空间结构来优化查找，但在纬度（或经度，并不重要）上进行简单的排序索引，并通过二分搜索裁剪结果，可以将结果时间减少到设备上的约 45 ms，之后优化可能就没有意义了。

索引是一个简单的结构体数组，包含一个浮点数和一个指向 `BusStop` 数组的整数：

```c
typedef struct {
    float latitude;
    int anIndex;
} LatIndex;
```

> 7. http://www.objc.io/issue-4

从 `BusStop` 实例初始化后，我们使用基于块的 `qsort()` 函数对其排序。我们必须使用自定义二分搜索，标准库中的要求精确匹配，而对于纬经度，我们只需要找到最近的条目。

## 站点时刻查找

站点时刻有点挑战性，仅仅是因为它们非常多，大约三百万个。我们无法在启动时用相当快的 CSV 解析器读取 118-MB 的数据文件。我们也无法实时搜索 CSV 文件，因为条目不是按时刻排序，而是按 `trip-id` 排序。最后，在 CoreData 实现中将时间增加了 100 次搜索时间，如果这里不是这样就好了。

幸运的是，站点时刻非常简单：小时、分钟和 ID。由于它们的范围范围是 0 到 23（数据中为 0 到 31，允许环绕）并代表 0 到 59 的范围，我们可以分别用 5 位和 6 位的整数表示它们。我们将站点 ID 映射到约 13K 个站点的数组索引，因此每个站点时刻有 31 位来表示，对应示例 13.15 所示的结构。对于 300 万个时刻，这将是一个 12 MB 的数组，大约是 CSV 或 SQLite 表示法的十分之一。

### 示例 13.15 站点时刻的高效二进制编码

```c
typedef struct {
    unsigned int stopIndex:20;
    unsigned int hour:5,minute:6;
} StopTime;
```

### 示例 13.16 索引结构

```c
typedef struct {
    int bytime[32][60]; // 小时，分钟
} Buckets;
```

```c
typedef struct {
    Buckets bucketOffsets;
    StopTimes[];
} AllTimes;
```

## 第 13 章 I/O：示例

将此结构映射到内存后，按时间查找变得非常高效，每次查找仅需约 53.4 μs，大约比使用 CoreData 执行相同操作快了 8,000 倍。我曾在第 12 章中提到过，映射二进制表示是获得最佳性能的有效方法；这就是该概念的一个示例。你可能认为，将数据库查询替换为两个内存结构会以内存消耗为代价换取性能提升，但相反，我观察到内存消耗下降了，CoreData 方案约为 5 MB，而本方案约为 4 MB。此外，由于结构是映射的，内存保持着整洁，这对内存压力的贡献微乎其微，系统始终会剔除条目而无需触发内存警告。

我尝试了几种不同的组合搜索结果（位置和时间）的算法。最终结果最快的是双重嵌套循环，首先按位置过滤，然后在相关时间间隔的桶（buckets）中搜索找到的站点。

## 站点时间导入

我们如何将站点从 GTFS 结构提取到我们可以使用的高效二进制格式中？一旦我们得到了 `StopTime` 数组，就会创建一个桶索引以实现快速访问。由于我们按小整数进行排序，可以使用高效的桶排序（bucket sort），这是少数（非通用的）排序算法之一，其运行时间复杂度为 O(n)，而不是基于比较和元素交换的通用排序的理论下限 O(n log n)。示例 13.17 显示了代码；该算法步骤如下：

1. 确定各个桶的大小，每出现一次特定计数就增加桶计数。
2. 偏移量（Offsets）必须考虑之前所有桶的大小，因此累加切片。
3. 创建 `StopTimes` 的临时副本。
4. 执行实际桶排序：
   a. 根据小时和分钟将站点放入其桶中。
   b. 增加当前桶的偏移量。
5. 最后，使用传统的合并排序对每个桶内的偏移量进行排序。

### 示例 13.17 按首次时间后按站点 ID 高效排序站点

```c
-(void)sort
{
    StopTime *sorted=calloc(count+20, sizeof(StopTime));
    Buckets bucketSizes, bucketOffsets;
    bzero(&bucketSizes, sizeof bucketSizes);
    bzero(&bucketOffsets, sizeof bucketOffsets);
}

//--- 计算桶的大小
for (int i=0;i<count;i++) {
    StopTime current=times->times[i];
    if ( current.hour < 31 || current.minute < 60 ) {
        bucketSizes.bytime[current.hour][current.minute]++;
    }
}

// 将计数累加到偏移量
int currentOffset=0;
for (int h=0;h<30;h++) {
    for (int m=0;m<60;m++) {
        bucketOffsets.bytime[h][m]=currentOffset;
        currentOffset+=bucketSizes.bytime[h][m];
    }
}

memcpy(&times->bucketOffsets, &bucketOffsets, sizeof(times->bucketOffsets));

//// 按时间桶排序
for (int i=0;i<count;i++) {
    StopTime t=times->times[i];
    sorted[bucketOffsets.bytime[t.hour][t.minute]] =current;
    bucketOffsets.bytime[t.hour][t.minute]++;
}

// 在桶内按站点索引常规排序
for (int h=0;h<29;h++) {
    for (int m=0;m<60;m++) {
        int offset=bucketOffsets.bytime[h][m+1]-offset;
```
