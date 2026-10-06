

# 第10章 文件

`sales.dat` 文件包含了在示例运行中用户输入的数据。图10-13显示了程序的流程图。

## 程序 10-3

```
1 // 用于存储天数的变量
2 Declare Integer numDays
3
4 // 循环的计数器变量
5 Declare Integer counter
6
7 // 用于存储销售额的变量
8 Declare Real sales
9
10 // 声明一个输出文件。
11 Declare OutputFile salesFile
12
13 // 获取天数。
14 Display "你有多少天的销售额?"
15 Input numDays
16
17 // 打开名为 sales.dat 的文件。
18 Open salesFile "sales.dat"
19
20 // 获取每天的销售额并将其
21 // 文件。
22 For counter = 1 To NumDays
23 // 获取第 # 天的销售额
24 Display "输入第 # 天的销售额", counter
25 Input sales
26
27 // 将金额写入文件。
28 Write salesFile sales
29
30 End For
31 // 关闭文件。
32 Close salesFile
33 Display "数据已写入 sales.dat。"
```

## 程序输出（输入部分加粗显示）

你有多少天的销售额?
5 [Enter]
输入第 #1 天的销售额
1000.00 [Enter]
输入第 #2 天的销售额
2000.00 [Enter]
输入第 #3 天的销售额
3000.00 [Enter]
输入第 #4 天的销售额
4000.00 [Enter]
输入第 #5 天的销售额
5000.00 [Enter]
数据已写入 sales.dat。

## 图 10-12 sales.dat 的内容

| 1000.00 分隔符 | 2000.00 分隔符 | 3000.00 分隔符 | 4000.00 分隔符 | 5000.00 分隔符 | EOF |

## 图 10-13 程序 10-3 的流程图

![](img/c939132f7878c7f339c6977b3fc885_415.png)

## 使用循环读取文件并检测文件末尾

程序通常必须在不知道文件中存储了多少个项目的情况下读取其文件内容。例如，由程序 10-3 创建的 `sales.dat` 文件可以存储任意数量的项目，因为程序会询问用户他有多少天的销售。如果用户输入 5 作为天数，程序将获取 5 个销售金额并将其存储在文件中。如果用户输入 100 天数，程序将获取 100 个销售金额并将其存储在文件中。如果你想编写一个程序来处理文件中所有的项目，无论其中有多少个项目，这就会带来一个问题。例如，假设你需要编写一个程序来读取文件中所有的金额并计算它们的总和。你可以使用循环来读取文件中的项目，但如果程序尝试读取文件末尾之后的内容，就会发生错误。程序需要某种方法来知道何时到达文件末尾。

大多数编程语言都为此类目的提供了一个库函数。在我们的伪代码中，我们将使用 `eof` 函数。该函数的通用格式如下：

```
eof(fileName)
```

`eof` 函数接受一个文件名作为参数，如果到达文件末尾则返回 True，如果未到达文件末尾则返回 False。程序 10-4 中的伪代码显示了如何使用 `eof` 函数的示例。程序显示了 `sales.dat` 文件中的所有销售金额。

## 程序 10-4

```
// 声明一个输入文件。
Declare File inputFile
// 声明一个变量来存储从文件中
// 读取销售金额。
Declare Real sales
// 打开 sales.dat 文件。
Open inputFile "sales.dat"
Display "这些是销售金额："
// 读取文件中的所有项目
// 并显示它们。
While NOT eof(inputFile)
  Read inputFile
  Display currencyFormat(sales)
End While
// 关闭文件。
Close inputFile
```

## 程序输出

这些是销售金额：

```
$1,000.00
$2,000.00
$3,000.00
$4,000.00
$5,000.00
```

## 10.2 使用循环处理文件

仔细观察第 15 行：

```
While NOT eof(inputFile)
```

当你阅读这段伪代码时，你自然会想：*当不在文件末尾时...* 这个语句也可以写成：

```
While eof(inputFile) == False
```

虽然这在逻辑上是等价的，但大多数程序员更倾向于使用第 15 行所示的 NOT 运算符，因为它更清楚地说明了正在测试的条件。图 10-14 显示了程序的流程图。

## 图 10-14 程序 10-4 的流程图

![](img/c939132f7878c7f339c6977b3fc885_417.png)

## Spotlight：文件操作

Kevin 是一位为当地企业制作商业广告的自由制作人。在制作商业广告时，他通常会拍摄几个视频。随后他将这些视频剪辑在一起。他要求你设计以下两个程序：

1. 一个允许他输入每个视频的时长（秒）并将其保存到文件的程序。
2. 一个读取文件内容、显示这些时长并计算视频总时长的程序。

这里是第一个程序的通用算法：

1. 获取视频数量。
2. 打开一个输出文件。
3. 对于每个视频：
   获取视频的时长。
   将其写入文件。
4. 关闭文件。

程序 10-5 显示了第一个程序的伪代码。10-15 显示了流程图。

## 程序 10-5

```
1 // 声明一个输出文件。
2 Declare outputFile
3 // 用于存储视频数量的变量
4 Declare Integer numVideos
5
6 // 用于存储视频时长的变量
7 Declare Real runningTime
8
9 // 循环的计数器
10 Declare Integer counter
11
12 // 获取视频数量。
13 Display "项目中有多少视频?"
14 Input numVideos
15
16 // 打开输出文件。
17 Open outputFile "time.dat"
18
19 // 对于每个视频
20 For counter = 1 To numVideos
21 // 获取视频的时长。
22 Display "第 # 天视频的时长"
23 Input runningTime
24
25 // 将时长写入文件。
26 Write outputFile runningTime
27
28 End For
29 // 关闭文件。
30 Close outputFile
31 Display "时长已写入 time.dat。"
```

## 程序输出（输入部分加粗显示）

项目中有多少视频?
6 [Enter]
输入第 #1 天视频的时长
24.5 [Enter]
输入第 #2 天视频的时长
12.2 [Enter]
输入第 #3 天视频的时长
14.6 [Enter]
输入第 #4 天视频的时长
20.4 [Enter]
输入第 #5 天视频的时长
22.5 [Enter]
输入第 #6 天视频的时长
19.3 [Enter]
时长已写入 time.dat。

## 图 10-15 程序 10-5 的流程图

![](img/c939132f7878c7f339c6977b3fc885_419.png)

这里是第二个程序的通用算法：

1. 将累加器初始化为 0。
2. 打开输入文件。
3. 当未到达文件末尾时：
   从文件中读取一个值。
   将该值加到累加器。
4. 关闭文件。
5. 显示累加器作为总时长。

## 程序 10-6

```
// 声明一个输入文件。
Declare File inputFile

// 用于存储从文件中
// 读取的时长的变量。
Declare Real videoRunningTime

// 总时间的累加器，
// 初始化为 0。
Declare Real total = 0

// 打开输入文件。
Open inputFile "time.dat"

// 显示 "这是项目中每个视频的时长（秒）："

// 读取文件中的所有时长，
// 显示它们，并计算它们的总和。
While NOT eof(inputFile)
  // 读取一个时长。
  Read inputFile videoRunningTime

// 显示该视频的时长。
  Display videoRunningTime

// 将 videoRunningTime 加到 total。
  Set total = total + videoRunningTime
End While

// 关闭文件。
Close inputFile

// 显示总时长。
Display "视频的总时长为 ",
  total, "秒。"
```

