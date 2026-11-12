

设置和启动内核，是为每个发出的内核必须支付的开销成本。对于执行时间短的 GPU 内核，这种开销成本可能占整体端到端执行时间的相当大比例。

使用图进行工作提交分为三个不同的阶段：定义、实例化和执行。

- 在定义阶段，程序会创建图中操作的描述，以及它们之间的依赖关系。
- 实例化会对图模板进行快照，对其进行验证，并执行大部分工作的设置和初始化，目的是尽量减少启动时需要完成的工作。生成的实例称为可执行图。
- 可执行图可以像任何其他 CUDA 工作一样启动到流中。它可以启动任意多次，而无需重复实例化。

## 3.2.5.6.1. 图结构

操作在图中形成一个节点。操作之间的依赖关系是边缘。这些依赖关系约束操作的执行顺序。

一旦操作所依赖的节点完成，该操作即可随时被调度。调度由 CUDA 系统决定。

### 3.2.5.6.1.1. 节点类型

图节点可以是以下之一：

- kernel
- CPU 函数调用
- 内存拷贝
- memset
- 空节点
- 子图：用于执行单独的嵌套图。参见图 11。

![](img/c13b0ff67eed8f2c7b32afa2a587a8d6_53_0.png)

### 图 11 子图示例

## 3.2.5.6.2. 使用 Graph API 创建图

图可以通过两种机制创建：显式 API 和流捕获。以下是创建和执行下图的示例。

![](img/c13b0ff67eed8f2c7b32afa2a587a8d6_54_0.png)

### 图 12 使用 Graph API 创建图示例

```
// Create the graph - it starts out empty
cudaGraphCreate(&graph, 0);

// For the purpose of this example, we'll create
// the nodes separately from the dependencies to
// demonstrate that it can be done in two stages.
// Note that dependencies can also be specified
// at node creation.
cudaGraphAddKernelNode(&a, graph, NULL, 0, &nodeParams);
cudaGraphAddKernelNode(&b, graph, NULL, 0, &nodeParams);
cudaGraphAddKernelNode(&c, graph, NULL, 0, &nodeParams);
cudaGraphAddKernelNode(&d, graph, NULL, 0, &nodeParams);

// Now set up dependencies on each node
cudaGraphAddDependencies(graph, &a, &b, 1); // A->B
cudaGraphAddDependencies(graph, &a, &c, 1); // A->C
cudaGraphAddDependencies(graph, &b, &d, 1); // B->D
cudaGraphAddDependencies(graph, &c, &d, 1); // C->D
```

## 3.2.5.6.3. 使用流捕获创建图

流捕获提供了一种从现有基于流的 API 创建图的机制。将工作启动到流中的代码段（包括现有代码）可以通过调用 `cudaStreamBeginCapture()` 和 `cudaStreamEndCapture()` 来括起来。参见下文。

```
cudaGraph_t graph;
cudaStreamBeginCapture(stream);
kernelA<<< ..., stream >>>(...);
kernelB<<< ..., stream >>>(...);
libraryCall(stream);
kernelC<<< ..., stream >>>(...);
cudaStreamEndCapture(stream, &graph);
```

调用 `cudaStreamBeginCapture()` 会将流置于捕获模式。当流正在被捕获时，启动到流中的工作不会被排队执行。相反，它会被追加到一个正在逐步构建的内部图中。然后通过调用 `cudaStreamEndCapture()` 返回此图，该调用也会结束流的捕获模式。由流捕获主动构建的图称为 *捕获图*。

流捕获可以用于任何 CUDA 流，除了 `cudaStreamLegacy`（“NULL 流”）。请注意，它 *可以* 用于 `cudaStreamPerThread`。如果程序正在使用旧版流，则可能可以将流 0 重新定义为每线程流，而不会产生功能变化。参见默认流。

可以使用 `cudaStreamIsCapturing()` 查询流是否正在被捕获。

### 3.2.5.6.3.1. 跨流依赖关系和事件

流捕获可以处理使用 `cudaEventRecord()` 和 `cudaStreamWaitEvent()` 表达的跨流依赖关系，前提是正在等待的事件已记录到同一个捕获图中。

当在处于捕获模式的流中记录事件时，会产生一个 *捕获事件*。捕获事件表示捕获图中的一组节点。

当流等待捕获事件时，如果该流尚未处于捕获模式，则会将其置于捕获模式，并且流中的下一项将对捕获事件中的节点具有额外依赖关系。然后，这两个流都会被捕获到同一个捕获图中。

在流捕获中存在跨流依赖关系时，`cudaStreamEndCapture()` 仍必须在调用 `cudaStreamBeginCapture()` 的同一流中调用；这就是 *源流*。由于基于事件的依赖关系而正在被捕获到同一捕获图中的任何其他流，也必须重新连接回源流。下图对此进行了说明。所有正在被捕获到同一捕获图中的流在调用 cudaStreamEndCapture() 时都会退出捕获模式。未能重新连接到源流会导致整体捕获操作失败。

```
// stream1 is the origin stream
cudaStreamBeginCapture(stream1);

KernelA<<< ..., stream1 >>>(...);

// Fork into stream2
cudaEventRecord(event1, stream1);
cudaStreamWaitEvent(stream2, event1);

KernelB<<< ..., stream1 >>>(...);
KernelC<<< ..., stream2 >>>(...);

// Join stream2 back to origin stream (stream1)
cudaEventRecord(event2, stream2);
cudaStreamWaitEvent(stream1, event2);

KernelD<<< ..., stream1 >>>(...);

// End capture in the origin stream
cudaStreamEndCapture(stream1, &graph);

// stream1 and stream2 no longer in capture mode
```

上述代码返回的图如图 12 所示。

![](img/c13b0ff67eed8f2c7b32afa2a587a8d6_56_0.png)

### 3.2.5.6.3.2. 禁止和未处理的操作

同步或查询正在被捕获的流或捕获事件的执行状态是无效的，因为它们不表示已排期执行的项目。查询或同步涵盖活动流捕获的更广泛句柄（例如，当任何关联流处于捕获模式时的设备或上下文句柄）也是无效的。

当同一上下文中的任何流正在被捕获，且该流不是使用 cudaStreamNonBlocking 创建的时，任何尝试使用旧版流的操作都是无效的。这是因为旧版流句柄始终涵盖这些其他流；向旧版流排队会创建对正在被捕获流的依赖关系，而查询或同步它会查询或同步正在被捕获的流。

因此，在这种情况下调用同步 API 也是无效的。同步 API（例如 cudaMemcpy()）会将工作排队到旧版流，并在返回前对其进行同步。

![](img/c13b0ff67eed8f2c7b32afa2a587a8d6_56_1.png)

通过等待来自正在被捕获且与事件关联的捕获图不同的流中的捕获事件来合并两个独立的捕获图是无效的。从正在被捕获的流中等待非捕获事件也是无效的。

少数将异步操作排队到流中的 API 目前在图中不受支持，如果在正在被捕获的流中调用，它们会返回错误，例如 cudaStreamAttachMemAsync()。

### 3.2.5.6.3.3. 失效

在流捕获期间尝试无效操作时，任何关联的捕获图都会失效。当捕获图失效时，进一步使用任何正在被捕获的流或与图关联的捕获事件都是无效的，并会返回错误，直到使用 cudaStreamEndCapture() 结束流捕获。此调用将使关联流退出捕获模式，但也会返回错误值和 NULL 图。

## 3.2.5.6.4. 使用 Graph API

cudaGraph_t 对象不是线程安全的。用户有责任确保多个线程不会同时访问同一个 cudaGraph_t。

cudaGraphExec_t 不能与自身并发运行。cudaGraphExec_t 的启动将排在同一可执行图的先前启动之后。

图执行在流中进行，以便与其他异步工作进行排序。但是，流仅用于排序；它不约束图的内部并行性，也不影响图节点的执行位置。

参见 Graph API。

## 3.2.5.7. 事件

运行时还提供了一种方法，允许应用程序在程序的任何点异步记录事件，并查询这些事件何时完成，从而密切监控设备的进度并进行准确计时。当事件之前的所有任务（或者可选地，给定流中的所有命令）都完成时，事件即视为完成。流零中的事件在所有流中所有先前任务和命令完成后完成。

### 3.2.5.7.1. 创建和销毁

以下代码示例创建两个事件：

```
cudaEvent_t start, stop;
cudaEventCreate(&start);
cudaEventCreate(&stop);
```

销毁方式如下：

```
cudaEventDestroy(start);
cudaEventDestroy(stop);
```

