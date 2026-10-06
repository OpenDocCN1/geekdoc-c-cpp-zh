

# 列表 1-43 获取序列 bigint 长度的 fold 函数

```fsharp
let mySeq = { 1..10 }
let length = Seq.fold (fun acc n -> acc + n) 0I mySeq
printf "the bigint length of seq is %A" length
```

# collect

`collect` 函数将用户定义的函数应用于集合中的每个元素，并合并结果。该函数的一个良好应用是 LINQ 的 `SelectMany` 扩展方法。`SelectMany` 方法会展平层级结构并返回二级集合中的所有元素。下面的示例首先生成一个列表列表，然后合并所有内容。参见列表 1-44。

# 列表 1-44 collect 函数

```fsharp
let generateListTo x = [0..x]

// 生成列表 [0:1]; [0;2]; [0;1;3]
let listOfLists = [1..3] |> List.map generateListTo

// 合并结果
// seq [0; 1; 0; 2; 0; 1; 2]
let result = listOfLists |> Seq.collect (fun n -> n)
```

> 提示 如果你可以使用内置的 `id` 函数，最后一行可以重写为 `Seq.collect id`。

# append

此方法接受两个集合并返回一个新集合，其中第一个集合的元素后紧跟着第二个集合的元素。LINQ 的 `Concat` 函数提供了相同的功能。参见列表 1-45。

# 列表 1-45 append 函数

```fsharp
// 以下操作拼接两个数组并生成
// 一个包含 [1;2;3;4;5;6] 的新数组
printf "%A" (Array.append [| 1; 2; 3|] [4; 5; 6])
```

![](img/63aaf94e22830ab98ce16c5946be8ef6_55_0.png)

# 数学运算

除了转换函数外，F# 还提供了一系列丰富的函数用于对集合执行数学运算：

- **min 和 max**: `min` 和 `max` 函数用于查找集合中的最小值或最大值。这些函数就像 LINQ 的 `min` 和 `max` 函数。参见列表 1-46。

**列表 1-46** min 和 max 函数

```fsharp
let myList = [1..10]
let min = myList | List.min    // min 是 1
let max = myList | List.max    // max 是 10
```

**average**: `average` 函数用于获取集合中所有元素的平均值。由于 F# 没有到 `float` 的隐式类型转换，以下代码生成一个 `int` 且不支持 *DivideBy* 运算符，这意味着操作数必须转换为支持除法的数据类型，例如 *float* 或 *float32*。参见列表 1-47。

**列表 1-47** 用于整数的 average 函数

```fsharp
let myList = [1..10]

// 无法编译，因为 int 不支持 "DivideBy"
let myListAverage = myList | List.average
```

你可以使用 `map` 将整数元素更改为 *float* 元素。同样，*float* 也是一个将整数转换为 *System.Double* 的函数。参见列表 1-48。

**列表 1-48** float 序列中的 average 函数

```fsharp
let myList = [1..10]

// 平均值是 float 类型 5.5
let myListAverage = myList
    |> List.map float
    |> List.average
```

**sum**: `sum` 函数返回集合中元素的和。*sum* 结果取决于输入序列元素的类型。列表 1-49 中的示例展示了这一点。

**列表 1-49** *sum* 函数

```fsharp
let mySeq = seq { 1..10 }

// sum 是 55
let result = mySeq | Seq.sum
```

# zip 和 zip3

`zip` 函数将两个序列合并为对序列。`zip3` 函数正如其名，将三个序列合并为三元组。`zip` 示例见列表 1-50。你可以在 MSDN (http://msdn.microsoft.com/en-us/library/ee370585.aspx) 上找到 `zip3` 的示例。

列表 1-50 zip 函数

```fsharp
let myList = [ 1 .. 3 ]
let myList2 = [ "a"; "b"; "c" ]

// zip 结果是 [(1, "a"), (2, "b"), (3, "c")]
let result = List.zip myList myList2
```

# rev

`rev` 函数反转列表或数组中的元素。示例代码见列表 1-51。

列表 1-51 rev 函数

```fsharp
let reverseList = List.rev [ 1 .. 4 ]

// 打印反转后的列表，即 [4;3;2;1]
printf "%A" reverseelist
```

> 注意 Seq 并没有实现 `rev` 函数。

# sort

`sort` 函数使用 `Operators.compare` 对列表进行排序。如果原始元素的顺序被保留，则这被称为稳定排序。`Seq` 和 `List` 上的 `sort` 函数是稳定的，而 `Array.sort` 则不是稳定排序。参见列表 1-52。

列表 1-52 sort 函数

```fsharp
let sortedList = List.sort [1; 8; -2]
// 打印排序后的列表
printf "%A" sortedList
```

# 转换为 Seq/List/Array

每种集合类型都有其独特的用法。通过函数将一种类型转换为另一种是常见的。示例见列表 1-53。

- `toList` 用于将 seq 转换为 list。
- `toArray` 用于将 seq 转换为 array。
- `toSeq` 用于将 list 转换为 seq。
- `toArray` 用于将 list 转换为 array。
- `toSeq` 用于将 array 转换为 seq。
- `toList` 用于将 array 转换为 list。

**列表 1-53**  seq、list 和 array 示例

```fsharp
// 定义序列
let mySeq = { 1..5 }
// 定义列表
let myList = [1..5]
// 定义数组
let myArray = [|1..5 |]
// seq 转换为 list
let myListFromSeq = mySeq | Seq.toList
// seq 转换为 array
let myArrayFromSeq = mySeq | Seq.toArray
// list 转换为 seq
let seqFromList = myList | List.toSeq
// list 转换为 array
let arrayFromList = myList | List.toArray
// array 转换为 seq
let seqFromArray = myArray | Array.toSeq
// array 转换为 list
let listFromArray = myArray | Array.toList
```

# 从 Seq/List/Array 转换

与 C# 使用 *from* 前缀不同，F# 使用 *of* 前缀将一种集合转换为另一种。示例见列表 1-54。

- `ofList` 用于将 list 转换为 seq。
- `toArray` 用于将 array 转换为 seq。
- `ofSeq` 用于将 seq 转换为 list。
- `ofSeq` 用于将 seq 转换为 array。
- `toList` 用于将 array 转换为 list。

**列表 1-54** seq、list 和 array 转换

```fsharp
// 定义序列
let mySeq = { 1..5 }
// 定义列表
let myList = [1..5]
// 定义数组
let myArray = [|1..5 |]
// list 转换为 seq
let seqFromList = Seq.ofList myList
// array 转换为 seq
let seqFromArray = Array.toList
// seq 转换为 list
let listFromSeq = mySeq | Seq.ofList
// seq 转换为 array
let arrayFromSeq = mySeq | Seq.toArray
// array 转换为 list
let listFromArray = myArray | Array.toSeq (注：此处原文逻辑似乎有误)
```

# 表 1-3 集合函数

| Function | Array | List | Seq | Map | Set | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| append | O(m+n) | O(min,n) | O(1) | | | 拼接两个集合。 |
| add | | | O(logN) | O(logN) | | 添加新元素并返回新集合。 |
| average / averageBy | O(n) | O(n) | O(n) | | | 获取所有元素的平均值。 |
| blit | O(n) | | | | | 返回数组的切片。 |
| cache | | | O(n) | | | 缓存元素。 |
| cast | | | O(n) | | | 将元素转换为指定的类型。 |
| choose | O(n) | O(n) | O(n) | | | 如果不为 None 则选择该元素。 |
| collect | O(n) | O(n) | O(n) | | | 将函数应用于每个元素并合并结果。 |
| compareWith | | | O(n) | | | 使用给定的函数逐元素比较元素。 |
| concat | O(n) | O(n) | O(n) | | | 拼接两个集合。 |
| contains | | | | O(logN) | | 测试指定的元素。 |
| containsKey | | | | O(logN) | | 测试元素是否在 map 的域内。 |
| count | | | | | O(logN) | 统计集合中的元素数量。 |
| countBy | | | O(n) | | | 计算生成的键的数量。键由函数生成。 |
| copy | O(n) | | O(n) | | | 创建集合的副本。 |
| create | O(n) | | | | | 创建数组。 |
| delay | | | O(1) | | | 返回根据给定序列规范构建的序列。 |
| difference | | | | O(m*logN) | | 返回包含 set1 中不在 set2 中的元素的新集合。 |
| distinct/ /distinctBy | | | O(1) | | | 返回去除了重复元素的新 seq。 |
| empty | O(1) | O(1) | | O(1) | O(1) | 创建一个空集合。 |
| exists | O(n) | O(n) | O(n) | O(logN) | O(logN) | 测试是否有元素满足条件。 |
| exists2 | O(min(n,m)) | | O(min(n,m)) | | | 测试输入序列的对应对是否满足给定的谓词。 |
| fill | O(n) | | | | | 将元素范围设置为指定值。 |

