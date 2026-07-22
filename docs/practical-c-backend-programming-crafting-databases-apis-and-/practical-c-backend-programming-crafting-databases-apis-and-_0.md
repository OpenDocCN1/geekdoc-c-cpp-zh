# Practical C++ 后端编程：为高性能后端构制数据库、API 和 Web 服务器



# 前言

《实用 C++ 后端编程》是一份全面的指南，为读者提供了必要的工具和知识，帮助他们成为精通 C++ 后端的开发人员。本书重点关注现实应用和实际实现，带领读者领略后端开发的多个领域，是任何有志成为后端开发者或现任后端开发人员的不可或缺的资源。

从基础知识开始，本书介绍了 `C++`，为该语言、其结构以及与后端编程的核心概念奠定了坚实的基础。随后，读者将深入学习后端开发中更复杂的元素。通过引人入胜的章节、用例和示例，读者将接触到并发编程等高级主题，探索使用线程和多进程来处理密集型计算任务，从而为构建可扩展应用程序奠定基础。

本书深入探讨了 API（特别是 `gRPC`）、以及缓存策略和数据库管理，并使用 `MongoDB` 作为首选的 NoSQL 数据库。在此过程中，读者将学习如何在实际场景中实现这些技术，从零开始构建一个博客应用程序，从而弥补理论与实际实现之间的鸿沟。书中专门有一个章节介绍应用程序安全，其中教授了身份验证、授权和数据库安全，并演示了如何在博客应用程序中实施这些措施。

本书的另一个极其重要的部分是涵盖测试策略，教授读者如何使用 `Google Test` (`gtest`) 创建健壮且无故障的后端解决方案。最后，这段旅程将在在 `AWS` 上部署应用程序的逐步引导中告终，确保读者具备了将其应用程序推上线所需的必要技能。

## 在本书中，你将学习如何：

*   `C++` 编程的详细概述，兼顾初学者和经验丰富的编码人员。
*   并发编程的实战探索，以设计可扩展且高效的应用。
*   全面理解 API 的用法，特别是使用 `gRPC` 框架。
*   深入研究 `MongoDB` 以实现有效的 NoSQL 数据库管理和操作。
*   实现缓存策略以进行性能优化的步骤。
*   策略性地使用 `Nginx` 处理包括负载均衡在内的 Web 服务器需求。
*   为数据库、API 和 Web 服务器实施安全措施的实操指南。
*   使用 `Google Test` 进行健壮应用程序测试和调试的说明。
*   在 `AWS` 上部署应用程序的逐步指导，确保满足真实环境的就绪要求。
*   通过构建和完善博客应用程序来实际应用相关概念。





# 序言

当今的软件工程师需要多种能力来跟上技术飞速发展的步伐。他们还需要具备数据库、应用程序编程接口（API）、Web 服务器以及其他相关技术的知识。本书通过使用强大且灵活的 C++ 编程语言，旨在作为后端开发的全面指南。本书通过理论讨论、真实世界示例和动手练习的结合，向读者教授 C++ 应用开发的基础知识。

书的第一部分侧重于解释 C++ 以及为什么许多程序员认为它是胜任这项工作的最佳语言。本书提供了 C++ 的全面概述，涵盖了从语言基础到并发等前沿特性的所有内容。C++ 标准模板库（`STL`）是 C++ 程序员的一套强大工具箱，书中对其进行了详细的探讨。

书的后半部分深入了算法和数据库，这是后端开发的核心内容。它解释了如何使用各种算法来简化复杂问题、增强功能并优化代码。本书深入探讨了如何使用广名的 NoSQL 数据库 `MongoDB` 来实践 CRUD 操作。

第三部分，书籍深入探讨了构建和利用 API 的细节，重点是 `gRPC` 框架。`gRPC` 框架是创建分布式程序和服务的可靠且高效的工具。它帮助程序员创建可以扩展到大量请求而不牺牲性能的 API。这一节还深入探讨了保护 API 和 Web 服务器的话题。

测试和调试过程占据了书第四部分的大部分。通过使用 `Google Test` 框架，详细介绍了如何创建测试用例以及如何排除可能出现的问题。得益书中对如何设置持续测试环境的解释，代码始终处于可部署状态。

部署程序在书的最后一章中讨论。它详细解释了如何使用最流行的云平台 `AWS` 进行应用部署。这一节还讨论了部署过程中必须考虑的各种因素，如安全性、可扩展性和性能。

在整本书中，你将构建一个博客应用程序来练习所学的技能。这种方法确保了读者不仅在吸收理论，而且在实践中使用它。这本书与其他书籍的不同之处在于它对实际应用的强调。到本书结束时，读者将会在 C++ 后端开发方面拥有坚实的基础，并能够将所学应用于创建高效、健壮且安全的应用程序。



Web 的初始阶段完全是静态且只读的。这一阶段通常被称为 Web 1.0，主要由通过链接连接的 HTML 页面组成。交互极少，用户只能通过链接进行导航。内容由特定个人创建并发布，用户仅仅是消费者。这一阶段主要是关于信息传播，Web 是巨大的数字图书馆。

### 动态 Web (Web 2.0)
Web 2.0 动态交互网站的引入标志着重大变化。得于 JavaScript 和 AJAX 等技术，网站现在可以动态生成页面。这意味着 Web 页面不再是静态的，而是根据用户的操作做出反应。这一阶段见证了用户生成内容的崛起，用户现在能够为 Web 贡献。博客、维基和论坛在此期间变得流行。

... [后续...]

### 社交 Web
`Facebook`、`Twitter` 和 `YouTube` 等社交媒体平台的出现扩展了 Web 上可能的边界。这些平台不仅允许用户生成内容，还促进了用户之间的互动。这一阶段向社区驱动、参与式内容发生了转变。Web 变成了一个社交空间。

### 移动 Web
智能手机和移动设备的爆炸开启了移动 Web 时代。网站必须适应在较小的屏幕和不同设备上显示，这导致了响应式 Web 设计的兴起。随着渐进式 Web 应用 (`PWA`) 等技术的出现，Web 应用与原生应用之间的界限开始模糊，它允许 Web 应用安装在用户的设备上并离线工作。

### 可编程 Web
今天，我们处于可编程 Web 时代，其标志是 API、微服务和云计算。Web 不仅仅是浏览网站。它是一个构建在任何环境和任何设备上运行的复杂应用程序的平台。API 允许不同的软件应用程序相互通信并交换数据，从而创建复杂的集成应用程序。微服务架构允许将应用程序拆分为独立开发、部署和扩展的小型服务。云计算为托管这些应用和服务提供了基础设施，提供了可扩展性、灵性和成本效益。

## 服务端：深度解析

在 Web 生态系统中，服务端或后端通常被称为“服务器”，它是驱动 应用程序功能的核心组件。它可以被认为是 Web 应用程序的大脑，负责处理请求、业务逻辑、数据管理等更多内容。

### 服务器架构
在基础层，服务器是管理网络中集中资源或服务的计算机或系统。虽然客户端（通常是 Web 浏览器）运行在用户的设备上并提供交互的用户界面，但服务器在后台处理这些交互。

服务器的主要角色是等待客户端的请求，处理这些请求，然后返回相应的响应。为了实现这一点，服务器通常托管 Web 服务器软件，例如 `Apache`、`Nginx` 或 `IIS`，用于监听 `HTTP(S)` 请求。当请求进来时，该软件将请求重定向到服务器上运行的相关应用程序。

### 后端语言与框架
Web 应用程序的后端托管在服务器并在后台运行，它是负责处理基础逻辑、数据存储以及驱动体验的 API 的关键组件。后端语言的选择受到许多因素的影响。PHP, Python, Ruby, Java, JavaScript (Node.js) 和 C++ 是一些常用的编程语言。除了编程语言，还有许多框架可以辅助开发，例如 Django (Python)、Rails (Ruby) 和 Express (Node.js)。这些框架提供的代码片段使得开发变得更容易。





1. 初始化一个空的推荐列表。
2. 获取用户购买的书籍列表。
3. 确定所购书籍中最常见的类型。
4. 过滤平台书籍数据库，仅包含该类型的书籍。
5. 根据平均评分对过滤后的书籍进行排序。
6. 将高 rating 的书籍添加到推荐列表中。
7. 返回推荐列表。




## 优化
## 优化
最后，考虑如何优化算法。这可能涉及减少冗余步骤、使用更高效的数据结构或利用并行处理。对于书籍推荐算法，优化可能涉及缓存用户的购买历史，这样在每次进行推荐时就不需要从数据库中检索，或者它可能涉及使用优先级队列来高效地选择评分最高的书籍。

## 测试
设计算法的最后一步是对其进行彻底测试。这涉及到使用各种输入运行算法，以确保它产生预期的输出。对于书籍推荐系统，你可能针对具有明确体类型偏好的用户、购买过多种类型书籍的用户以及尚未购买的用户对算法进行测试。总而言之，设计算法是一个系统且迭代的过程，涉及到理解问题、定义流程、编写伪代码、优化算法以及进行彻底测试。一个设计良好的算法可以在高效、可靠的后端系统与缓慢且易出错的系统之间产生区别。因此，对于任何开发者来说，在算法设计上花费时间都是一项值得的投资。

## 排序算法
排序是计算机科学中最基础的操作之一，理解不同的算法对于后端开发人员至关重要。让我们来看看`泡排序`、`插入排序`和`归并排序`，看看它们是如何运行的。

### 泡排序
泡排序是一种简单的算法，它重复遍历列表，比较相邻元素，如果它们的顺序错误则进行交换。重复遍历列表，直到列表排序完成。（image/image-4.jpg）图 3.1 泡排序算法。以下是使用泡排序算法的示例程序：

```cpp
void bubbleSort(int arr[], int n) {
  for(int i = 0; i < n-1; i++) {
    for(int j = 0; j < n-i-1; j++) {
      if(arr[j] > arr[j+1]) {
        // 交换 arr[j] 和 arr[j+1]
        int temp = arr[j];
        arr[j] = arr[j+1];
        arr[j+1] = temp;
      }
    }
  }
}
```
下面提供的演练过程是对上述代码工作原理的逐步解释：
- 函数 `bubbleSort`接收两个参数：一个整数数组 `arr[]`和一个表示数组大小的整数 `n`。
- 外层循环运行 `n-1` 次，其中 `n` 是数组的大小。这是因为在每次遍历数组时，最大的元素都会“泡”到它在数组末部的正确位置。因此，在 `n-1` 次遍历后，最小的元素将处于其正确位置，数组将完成排序。
- 内层循环运行 `n-i-1` 次。这是因为外层循环每通过一次，前 `n-i` 个元素中的最大元素就会放置在该区域的末尾，因此在下一次通过中不需要考虑它。
- 在内层循环内部，代码检查当前元素 `arr[j]` 是否大于下一个元素 `arr[j+1]`。如果是，说明这些元素的顺序是错误的（因为我们的目标是升序），它们需要交换。
- 交换通过临时变量 `temp` 完成。将 `arr[j]` 的值存储在 `temp` 中，然后将 `arr[j]` 设置为 `arr[j+1]` 的值，最后将 `arr[j+1]` 设置为存储在 `temp` 中的值。

这个过程一直持续，直到整个数组按升序排序。该算法被称为“泡排序”的原因是因为在每次迭代中，最大的未排序元素都会“泡浮”到它的正确位置。

### 插入排序
插入排序是一种简单的排序算法，它逐个项目构建最终的排序数组（或列表）。对于大型列表，它的效率远低于`快速排序`、`堆排序`或`归并排序`等算法。（image/image-5.jpg）图 3.2 插入排序算法。以下是使用插入排序的示例程序：

```cpp
void insertionSort(int arr[], int n) {
  for(int i = 1; i < n; i++) {
    int key = arr[i];
    int j = i - 1;
    // 将 arr[0..i-1] 中大于 key 的元素后移一位
    while (j >= 0 && arr[j] > key) {
      arr[j+1] = arr[j];
      j--;
    }
    arr[j+1] = key;
  }
}
```
以下是其工作原理的逐步解释：
- `insertionSort` 函数接收两个参数：一个整数数组 `arr[]`和数组大小 `n`。
- 外层循环从第二个元素运行到数组的最后一个元素。变量 `i` 是要插入排序序列 `arr[0..i-1]` 的元素。
- `key` 变量持有当前元素的值并与其左侧元素进行比较。
- 内层循环 `while(j >= 0 && arr[j] > key)` 将 `arr[0..i-1]` 中大于 `key` 的元素后移一位。
- 移动过程持续直到找到 `key` 的正确位置或到达数组开头。然后将 `key` 放在其正确位置。
- 外层循环移动到下一个元素，重复此过程直到整个数组排序。被称为插入排序是因为通过将每个项目插入其适当的位置工作。

### 快速排序
快速排序是一种高效的排序算法，基于分治法。它通过从数组中选择一个“基准”元素并根据其他元素是否大于它将其分为两个子数组。然后对子数组进行递归排序。（image/image-6.jpg）图 3.3 快速排序算法。以下是快速排序的代码：

```cpp
void quickSort(int arr[], int low, int high) {
  if (low < high) {
    // pi 是分区索引，arr[pi] 现在位于正确位置
    int pi = partition(arr, low, high);
    // 分别排序分区前后的元素
    quickSort(arr, low, pi - 1);
    quickSort(arr, pi + 1, high);
  }
}
int partition(int arr[], int low, int high) {
  int pivot = arr[high]; // 基准
  int i = (low - 1); // 较元素的索引
  for (int j = low; j <= high - 1; j++) {
    // 如果当前元素小于基准
    if (arr[j] < pivot) {
      i++;
      swap(arr[i], arr[j]);
    }
  }
  swap(arr[i + 1], arr[high]);
  return (i + 1);
}
```
提供的演练是对代码的逐步解释：
- `quickSort` 函数是实现快速排序的主函数。它接收三个参数：一个数组 `arr[]`以及两个整数 `low`和`high`，它们代表待排序数组部分的起始和结束索引。
- `quickSort` 函数首先检查 `low < high`。这是为了确保至少有两个元素需要排序。如果 `low` 不小于 `high`，函数直接返回。
- 如果 `low < high`，函数继续分区数组。分区由 `partition` 函数完成，它接收与 `quickSort` 相同的参数并返回一个整数 `pi`，分区索引。`partition` 函数确保 `arr[pi]` 元素位于正确位置。
- 分区后，`quickSort` 函数递归地排序 `pi` 之前和之后的元素。
- `partition` 函数通过从数组中选择基准元素（在此例中为 `arr[high]`）并将其他元素分为两个部分：小于基准的部分和大于基准的部分。它用 `i` 跟踪较小元素的索引。
- `partition` 函数使用`for`循环遍历数组。如果当前元素 `arr[j]` 小于基准，它递增 `i` 并交换 `arr[i]` 和 `arr[j]`。
- 在处理完所有元素后，`partition` 函数将基准元素与 `arr[i + 1]` 处的元素交换，有效地将基准放在排序数组的正确位置。它最后返回 `i + 1`，即基准的索引。
`swap` 函数是一个交换两个变量值的标准函数。它没有在提供的代码中显示，但它是通用的工具函数。
快速排序不是稳定排序，这意味着相等排序项目的相对顺序不会保留。尽管它的最坏情况时间复杂度为 $O(n²)$，但`QuickSort` 是排序数组最快的算法之一，并广泛使用。

### 归并排序
归并排序也基于分治法。它通过将未排序列表划分为 $N$ 个子列表（每个子列表包含一个元素被视为已排序），然后重复合并子列表以生成新的排序列表，直到只下一个子列表。（image/image-7.jpg）图 3.3 归并排序算法。以下是归并排序的代码：

```cpp
void mergeSort(int arr[], int l, int r) {
  if (l < r) {
    // 等于 (l+r)/2，但避免 l 和 r 的溢出
    int m = l + (r - l) / 2;
    // 排序第一和第二部分
    mergeSort(arr, l, m);
    mergeSort(arr, m + 1, r);
    // 合并排序部分
    merge(arr, l, m, r);
  }
}
void merge(int arr[], int l, int m, int r) {
  int n1 = m - l + 1;
  int n2 = r - m;
  int L[n1], R[n2];
  for (int i = 0; i < n1; i++) L[i] = arr[l + i];
  for (int j = 0; j < n2; j++) R[j] = arr[m + 1 + j];
  int i = 0, j = 0, k = l;
  while (i < n1 && j < n2) {
    if (L[i] <= R[j]) {
      arr[k] = L[i];
      i++;
    } else {
      arr[k] = R[j];
      j++;
    }
    k++;
  }
  while (i < n1) {
    arr[k] = L[i];
    i++;
    k++;
  }
  while (j < n2) {
    arr[k] = R[j];
    j++;
    k++;
  }
}
```
归并排序是稳定排序，比`泡排序`和`插入排序`更高效，时间复杂度为 $O(n \log n)$。

## 搜索算法
搜索算法是计算机科学的基础，用于从简单的数据检索到复杂问题的解决等应用。在各种搜索算法中，两种因其简单性和高效性脱颖而出：线性搜索和二分搜索。

### 线性搜索
线性搜索正如其名，以线性或顺序方式搜索列表。它是最基本的搜索算法，通过逐个遍历列表中的所有元素，直到找到所需的元素或检查完所有元素。尽管简单，线性搜索非常通用，能够处理已排序和未排序甚至带有重复元素的列表。线性搜索的过程可以总结为：从列表的第一个元素开始，将每个元素与目标元素比较。如果当前元素匹配目标，搜索结束并返回元素的位置。如果检查完所有元素后未找到目标元素，搜索得出该元素不在列表中。（image/image-8.jpg）图 3.4 线性搜索算法。以下是线性搜索的示例代码：

```cpp
int linearSearch(int arr[], int n, int x) {
  for (int i = 0; i < n; i++) {
    if (arr[i] == x) {
      return i; // 找到元素，返回索引
    }
  }
  return -1; // 未找到元素
}
```
在后端开发中，线性搜索对于小型数据集或未排序数据是有用的。然而，随着数据集增大，由于其最坏情况和平均时间复杂度为 $O(n)$，线性搜索可能会变得越来越低效。

### 二分搜索
二分搜索是一种高效的搜索算法，特别是对于大型排序数据集。与顺序扫描列表元素的线性搜索不同，二分搜索采用分治策略，在每次比较后有效地将搜索空间缩小一半。（image/image-9.jpg）图 3.5 二分搜索算法
二分搜索算法通过将目标值与排序列表的中间元素进行比较来操作。二分搜索背核心思想是：如果目标值等于中间元素，则搜索成功并返回元素的位置。如果目标值小于中间元素，目标只能位于下半部分（左侧）。相反，如果目标值大于中间元素，目标只能位于上半部分（右侧）。

```cpp
int binarySearch(int arr[], int l, int r, int x) {
  while (l <= r) {
    int mid = l + (r - l) / 2;
    if (arr[mid] == x)
      return mid;
    if (arr[mid] < x)
      l = mid + 1;
    else
      r = mid - 1;
  }
  return -1;
}
```
对于较大的排序数据集，二分搜索比线性搜索快得多，最坏和平均时间复杂度为 $O(\log n)$。然而，它要求数据集是排序的。

## 图算法
图算法是后端开发中各种操作的基础，特别是在数据分析、网络和路径查找领域。让我们讨论三种图算法：深度优先搜索（DFS）、广度优先搜索（BFS）和 Dijkstra 算法。

### 深度优先搜索（DFS）
深度优先搜索（DFS）是计算机科学中用于遍历或搜索图的基础算法。正如名称所示，它深入图，尽可能地遍历一个分支，直到没有更多节点。一旦到达末尾，它会回溯并开始探索下一个分支。DFS 使用栈结构来记住要访问的顶点。栈遵循后进先出（LIFO）原则，意味着最近发现且未完全探索的顶点是下一个要探索的。这种方法在回溯之前尽可能沿着每个分支深入探索。（image/image-10.jpg）图 3.6 深度优先搜索的应用。以下是 DFS 的 C++ 实现：

```cpp
#include <list>
#include <iostream>
class Graph {
  int V;
  std::list<int> *adj;
public:
  Graph(int V);
  void addEdge(int v, int w);
  void DFS(int v);
};
Graph::Graph(int V) {
  this->V = V;
  adj = new std::list<int>[V];
}
void Graph::addEdge(int v, int w) {
  adj[v].push_back(w);
}
void Graph::DFS(int v) {
  bool *visited = new bool[V];
  for (int i = 0; i < V; i++)
    visited[i] = false;
  std::list<int> stack;
  visited[v] = true;
  stack.push_back(v);
  while (!stack.empty()) {
    v = stack.back();
    std::cout << v << " ";
    stack.pop_back();
    std::list<int>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
      if (!visited[*i]) {
        visited[*i] = true;
        stack.push_back(*i);
      }
  }
}
```

### 广度优先搜索（BFS）
广度优先搜索（BFS）是一种基础遍历算法，按广度顺序探索图的所有顶点，在移动到下一个深度之前探索当前深度所有的邻居。BFS 使用队列来存储要访问的顶点。队列遵循先入先出（FIFO）原则，意味着入队的顺序就是它们出队的顺序。（image/image-11.jpg）图 3.7 广度优先搜索算法。以下是 BFS 的 C++ 实现：

```cpp
#include <list>
#include <iostream>
class Graph {
  int V;
  std::list<int> *adj;
public:
  Graph(int V);
  void addEdge(int v, int w);
  void BFS(int s);
};
Graph::Graph(int V) {
  this->V = V;
  adj = new std::list<int>[V];
}
void Graph::addEdge(int v, int w) {
  adj[v].push_back(w);
}
void Graph::BFS(int s) {
  bool *visited = new bool[V];
  for (int i = 0; i < V; i++)
    visited[i] = false;
  std::list<int> queue;
  visited[s] = true;
  queue.push_back(s);
  while (!queue.empty()) {
    int curr = queue.front();
    std::cout << curr << " ";
    queue.pop_front();
    for (auto i : adj[curr]) {
      if (!visited[i]) {
        visited[i] = true;
        queue.push_back(i);
      }
    }
  }
}
```

### Dijkstra 算法
Dijkstra 算法以其发现者荷兰计算机科学家 Edsger Dijkstra 命名，是图论中的强大工具。它是一种贪心算法，用于解决非负边权图的单源最短路径问题，生成最短路径树。算法通过维护一个未访问节点集合并不断选择距离起始点临时距离最小的节点，然后访问其所有未访问的邻居。只有在发现更短路径时，才会更新节点的临时距离。该过程持续到所有节点都被访问，此时算法保证已找到从起点到所有其他节点的最短路径。Dijkstra 算法广泛应用于网络路由协议，特别是 IS-IS（中间系统到中间系统）和 OSPF（开放最短路径优先）。这些协议用于确定数据包到达特定目的地的最佳路线。（image/image-12.jpg）图 3.8 Dijkstra 算法。以下是 Dijkstra 算法的 C++ 实现：

```cpp
#include <iostream>
#include <limits>
#include <vector>
using namespace std;
// 实现 Dijkstra 算法的函数
void dijkstra(vector<vector<int>> > graph, int src) {
  int V = graph.size();
  vector<int> dist(V, INT_MAX); // 初始化距离值
  dist[src] = 0;
  vector<bool> processed(V, false);
  for (int count = 0; count < V; count++) {
    // 从未处理的顶点中选择距离起点最近的顶点
    int min = INT_MAX, u;
    for (int v = 0; v < V; v++) {
      if (processed[v] == false && dist[v] <= min) {
        min = dist[v],
        u = v;
      }
    }
    processed[u] = true;
    for (int v = 0; v < V; v++) {
      if (processed[v] == false && graph[u][v] && dist[u] + graph[u][v] < dist[v]) {
        dist[v] = dist[u] + graph[u][v];
      }
    }
  }
  for (int i = 0; i < V; i++)
    cout << i << " \t" << dist[i] << endl;
}
```

## 哈希算法
哈希是一种用于将一系列键值转换为索引范围的技术。哈希使得数据检索极其高效，接近常数时间 $O(1)$。我们将关注基础哈希函数、冲突解决以及一些应用。

### 简单哈希函数
哈希函数将数字或字符串映射到可以作为桶索引的小整数。哈希的思想是将键值对分布到桶中。简单的哈希函数可以是对数组的长度进行取模并取余数。

```cpp
unsigned int hashFunction(string key, int N) {
  unsigned int hashValue = 0;
  for (char c : key) {
    hashValue += c;
  }
  return hashValue % N;
}
```

### 冲突解决
当两个键哈希到同一个索引时就会发生冲突。有几种技术可以解决冲突：
- 链法：每个桶包含包含所有哈希到该索引的列表。
- 开放寻址：当发生冲突时，我们在数组槽中寻找另一个空桶。

```cpp
// 使用链法
class MyHash {
  int BUCKET;
  list<int> *table;
public:
  MyHash(int b) {
    BUCKET = b;
    table = new list<int>[BUCKET];
  }
  void insert(int key) {
    int i = hash(key);
    table[i].push_back(key);
  }
  bool search(int key) {
    int i = hash(key);
    for (auto x : table[i])
      if (x == key)
        return true;
    return false;
  }
  void remove(int key) {
    int i = hash(key);
    table[i].remove(key);
  }
private:
  int hash(int key) {
    return key % BUCKET;
  }
};
```

# 第 5 章：使用 MongoDB 管理数据库
## 数据库在后端开发的作用
数据库在持久化存储、检索和处理数据的过程中起着至关重要的作用。对于任何应用程序，基本操作都是 CRUD：创建、读取、更新和删除。

## 执行 CRUD 操作
CRUD 操作是任何应用程序的基础，涉及到持久化存储。CRUD 代表创建、读取、更新和删除。

### 创建
在 MongoDB 中插入新文档使用 `insert_one` 或 `insert_many` 函数。创建一个用户：

```cpp
mongocxx::collection user_collection = db["users"];
bsoncxx::builder::stream::document user_doc;
user_doc << "username" << "new_user"
         << "email" << "new_user@blogapp.com"
         << "password" << "hashed_password";
user_collection.insert_one(user_doc.view());
```

### 读取
从集合中读取文档使用 `find` 函数。通过用户名查找用户：

```cpp
bsoncxx::builder::stream::document filter_builder;
filter_builder << "username" << "new_user";
auto cursor = user_collection.find(filter_builder.view());
for (auto doc : cursor) {
  std::cout << doc.to_json() << "\n";
}
```

### 更新
更新文档使用 `update_one` 或 `update_many` 函数。更新某个用户的邮箱：

```cpp
bsoncxx::builder::stream::document filter_builder;
filter_builder << "username" << "new_user";
bsoncxx::builder::stream::document update_doc;
update_doc << "$set" << "email" << "updated_email@example.com";
user_collection.update_one(filter_builder.view(), update_doc.view());
```

### 删除
删除文档使用 `delete_one` 或 `delete_many` 函数。删除用户：

```cpp
bsoncxx::builder::stream::document filter_builder;
filter_builder << "username" << "new_user";
user_collection.delete_one(filter_builder.view());
```

## 执行复杂查询：聚合和索引
聚合和索引是 MongoDB 的两个强大功能，允许我们执行复杂查询、过滤和排序数据，并提高数据库操作的效率。

### 执行聚合
MongoDB 中的聚合是对集合中的文档进行复杂数据分析的方法。它提供了一种处理数据记录并返回计算结果。聚合操作可以将多个文档的值组合在一起并对分组数据执行各种操作以返回单个结果。例如，在博客应用程序中，你可能想知道每个用户发布了多少帖子。可以使用 MongoDB 的聚合框架来实现。$group 阶段指定的标识符表达式对输入文档分组，并为每个唯一分组输出一个文档。然后使用$sum 操作符增加每个组的计数。

```cpp
mongocxx::collection posts_collection = db["posts"];
bsoncxx::builder::stream::document group_stage;
group_stage << "$group" << bsoncxx::builder::stream::open_document
            << "_id" << "$username"
            << "count" << bsoncxx::builder::stream::open_document
            << "$sum" << 1
            << bsoncxx::builder::stream::close_document
         << bsoncxx::builder::stream::close_document;
mongocxx::pipeline p;
p.aggregate(group_stage);
auto cursor = posts_collection.aggregate(p);
for (auto doc : cursor) {
  std::cout << doc.to_json() << "\n";
}
```

### 创建索引
在 MongoDB 中创建索引使用`create_index` 方法。在`username`字段上创建一个索引：

```cpp
bsoncxx::builder::stream::document index_builder;
index_builder << "username" << 1;
user_collection.create_index(index_builder.view());
```

# 第 4 章：掌握版本控制 - Git 和 GitHub
## 版本控制和仓库托管：概述
版本控制系统和仓库托管服务是软件开发中不可缺的工具，特别是对于后端编程。它们不仅有助于管理更改并保持项目组织，还能使协作更容易并提高代码库的质量。

## 探索 Git
Git 是一种广泛使用的版本控制系统，帮助开发者管理和跟踪更改。

### 4.1 Git 配置
首先，你需要在系统上安装 Git。你可以从其官方网站下载。
- Windows: `git-scm.com/download/win`
- MacOS: `brew install git`
- Linux (Ubuntu): `sudo apt-get install git`

安装 Git 后，你需要配置它。打开终端或命令提示符并输入以下命令：
- 设置你的名字：`git config --global user.name "Your Name"`
- 设置你的邮箱：`git config --global user.email "your_email"`

## 初始化 Git 仓库
要开始使用 Git，你需要在项目目录中初始化 Git 仓库。使用终端或命令提示符进入项目文件夹并输入 `git init`。该命令创建一个名为 .git 的子目录，其中包含所需的元数据。

## 跟踪更改
一旦仓库初始化，你就可以开始跟踪更改。使用 `git add .` 提交更改并使用 `git commit -m "Commit message"` 保存它们。

## 检查状态
你可以使用 `git status` 检查仓库的状态。该命令将显示任何已提交的更改、未提交的更改以及未跟踪的文件。

## 基础 Git 命令和工作流
### clone
当你想对现有仓库进行工作时，你可以克隆它。这会将仓库下载到你的本地机器。命令是 `git clone <repository URL>`。例如，如果你想为 GitHub 上托管的开源后端项目做贡献，你将从克隆仓库开始：

```bash
git clone https://github.com/username/repository.git
```
这会在当前文件夹中创建一个名为 repository.git 的目录。

### status
`git status` 命令用于显示工作目录和暂存区的状态。它显示哪些更改已提交，哪些尚未提交，哪些文件未被 Git 跟踪。

### add
`git add` 命令用于为下次提交准备更改。此命令告诉你你想在下次提交中包含某些文件的更新。要添加工作目录中的所有更改，使用 `git add .`。

### commit
`git commit` 命令用于将更改保存到本地仓库。每次提交都是你工作的“快照”，如果需要可以回滚。在提交中包含消息是良好的习惯，因为它为更改提供了上下文。这可以使用 `git commit -m "Your message here"` 完成。

### push
`git push` 命令用于将你的本地更改上传到远程仓库。在本地提交更改后，你可以将其与团队的其他成员共享。

### pull
`git pull` 命令用于从远程仓库获取并下载内容，并立即更新你的本地仓库最新更改。

### branch
`git branch` 命令用于管理 Git 中的分支。分支本质上是文件不同版本的指针。它允许你创建、列出删除删除。

### checkout
`git checkout` 命令用于在分支之间切换。当你切换到一个分支时，Git 会更新你的工作目录以匹配该版本。

### merge
`git merge` 命令用于将一个分支的更改合并到另一个分支。这通常在你完成功能开发或修复 Bug 时进行。

## 高级缓存策略
高级缓存可以显著提高应用程序的性能。缓存策略的选择取决于具体的需求。

### 缓存单个项目
在之前的示例中，我们缓存了整个列表。然而，如果获取数据的成本很高，可能会单独缓存它们。

```cpp
Post fetchPost(mongocxx::collection& postCollection, const std::string& postId) {
  Post post;
  std::string cacheKey = "post:" + postId;
  // 检查缓存
  if (cache.get(cacheKey, post)) {
    return post;
  }
  // 从数据库中获取
  post = postCollection.find_one(filter("_id" << postId));
  // 写入缓存
  cache.set(cacheKey, post);
  return post;
}
```

### 缓存旁 / 懒加载
缓存旁（Cache Aside）或懒加载策略意味着我们只在请求数据且缓存不存在时才将其加载到缓存。当从数据库读取成本很高时非常有效。

```cpp
// 伪代码逻辑
if (cache.exists(key)) {
  return cache.get(key);
}
data = db.query(key);
cache.set(key, data);
```

### 写入（Write-Through）策略确保缓存和数据库之间的数据一致性。当数据写入时，它同时写入缓存和数据库。

```cpp
void updatePost(mongocxx::collection& postCollection, const Post& post) {
  // 更新数据库
  postCollection.update_one(filter("_id" << post.id), update);
  // 更新缓存
  cache.set("post:" + post.id, post);
}
```

