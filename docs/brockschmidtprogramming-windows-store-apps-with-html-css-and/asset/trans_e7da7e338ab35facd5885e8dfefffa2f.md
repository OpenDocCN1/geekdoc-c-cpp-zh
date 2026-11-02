

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_149_0.png)

## 性能与内存分析

除了出色的调试工具外，Visual Studio 还提供了其他工具，帮助你评估应用的性能、分析其内存使用情况，并发现和诊断影响应用用户体验及其对系统影响的问题。在本章结束前，我想简要介绍一下可用的工具，并给出进一步学习的指引，因为这个主题本身就足以写成一本书！（如果不想展开，一个通用的建议是按 `performance` 标签筛选 //build 2013 视频，结果会相当丰富。）

首先，“编写高效的 JavaScript”主题非常值得一读（“使用 JavaScript 的最佳实践”下的相关主题也一样），因为它解释了在你的代码中应该做和不应该做的各种事项，以帮助 JavaScript 引擎发挥最佳性能。有一件事你不必担心，那就是 querySelector 和 getElementById 的性能；它们使用得非常频繁，因此都经过了高度优化。请记住这一点，因为就我自己而言，任何以 "query" 开头的函数听起来都像是要完成大量工作，但这里并非如此。

接下来，当涉及用户活动时，以及该内存是否被正确释放。请参阅 Visual Studio 2012 中 Windows 应用商店应用的 JavaScript 内存分析（MSDN 博客）以及分析 Windows 应用商店应用中的内存使用情况。 |
| JavaScript 函数计时（也称为 JavaScript 分析器） | 显示有关 JavaScript 函数调用在何时何地发生，以及代码各部分花费多少时间的数据。关于 JavaScript 应用性能问题的 JavaScript 分析器（MSDN 博客）提供了相关演练。另请参阅《分析 Windows 应用商店应用中的 JavaScript 性能》，其中涵盖本地和远程计算机。 |
| CPU 采样 | 与 JavaScript 函数计时工具类似，但适用于托管（C#/Visual Basic）和本机（C++）代码。只有在编写同时包含 JavaScript 和另一种语言的多语言应用时，此工具才派得上用场。 |

上述大多数工具都有视频演示：可以观看 Channel 9 上的 Visual Studio 2013 性能和诊断中心视频，以及 //build 2013 大会上的《使用 Visual Studio 2013 诊断 JavaScript Windows 应用商店应用中的问题》，两者均由 Andrew Hall 讲解，他是这方面的真正专家。请注意，这段视频中看到的一切（控制台应用分析器除外）都可以在我们一直在使用的 Visual Studio Express 版本中使用；如果你想跳过第一个视频中关于 XAML UI 响应性的部分，可以直接跳到大约 13:30，那里讲的就是 JavaScript 工具。

### 提示
在第一个视频中，用 XAML/C# 和 HTML/JavaScript 编写的演示应用出现响应性问题，主要是因为为了生成图库视图的缩略图而加载了完整尺寸的图像文件。正如视频中提到的，使用 Windows.Storage.StorageFile.getThumbnailAsync 完全可以避免这种情况，并获得更好的性能。这个 API 会利用缩略图缓存和其他机制，避免加载完整图像文件所带来的内存开销和 CPU 成本。

