

# 474 C++ 与 R 中的并行计算

使用 Rmpi 或 multicore 进行仿真。与之前的进展一致，这将通过 R 的 Rmpi 接口来实现。

有两个包提供了 RngStreams：reclyer 和 rstream。前者实际上是 Rmpi 中的一个功能，可以方便地访问，如下所示：

```r
> Library (Rmpi)
> mpi.spawn.Rslaves(nslaves = 4)
> 4 slaves are spawned successfully. 0 failed.
> master (rank 0, comm 1) of size 5 is running on: cos
> slave1 (rank 1, comm 1) of size 5 is running on: cos
> slave2 (rank 2, comm 1) of size 5 is running on: cos
> slave3 (rank 3, comm 1) of size 5 is running on: cos
> slave4 (rank 4, comm 1) of size 5 is running on: cos
> mpi.setup.rstream(seed = 1:6)
> Loading required package: reclyer
> mpi.remote.exec(runif(1))
X1 X2 X3 X4
1.000109498 0.701715 0.476142 0.04690119
```

请注意，在使用此方法之前需要安装 reclyer 包。如果是这种情况下，mpi.setup.rstream 的作用是将 R 默认的随机数生成器替换为 RngStreams 的骨干生成器。看起来 reclyer 的 rstream 实现比 rstream 包要慢。因此，从现在开始我们的讨论将集中在 rstream 上。关于这两个主题及其用法新新雪的进一步讨论，可以在 Karl, et al. (2011) 中找到。

第一步是加载 rstream 包

```r
> library (rstream)
```

这具有将 S4 类 rstream 引入当前 R 工作空间的效果。rstream 类的实例可以从派生类 rstream.mrg32k3a 创建，该派生类提供了对现在已为熟悉的 RngStreams 骨干生成器的访问。使用如下形式的语法可以创建一个新的 rstream 对象：

```r
newRstreamObj <- new("rstream.mrg32k3a", seed = Seed)
```

带有一个整数种子组件向量。随后创建的 rstream.mrg32k3a 对象将自动具有与最近创建的对象相比移除 2^27 个状态的初始种子。rstream.sample 函数通过以下命令从 newRstreamObj 返回 n 个随机数的样本：

```r
rstream.sample(newRstreamObj, n)
```

由于 rstream 对象作为指针存储在底层语言代码中，因此在将其发送到 Rmpi 的另一个节点之前需要进行“打包”（pack）。同样的过程也用于保存 rstream 对象，以便在未来的 R 会话可用。打包通过以下方式完成：

```r
rstream.packed(newRstreamObj) <- TRUE
```

在打包之前必须通过以下方式解包（unpack）：

```r
rstream.packed(newRstreamObj) <- FALSE
```

在此之外，结合 Rmpi 使用 rstream 的过程相对简单。对于 p 个进程的情况，执行以下步骤序列：

- 1. 创建 rstream.mrg32k3a 类的实例，
- 2. 使用 rstream.packed 打包每个对象。
- 3. 在每个处理器上加载 rstream 包，
- 4. 使用 mpi.send.Robj 将 rstream 对象发送到 p 个处理器，
- 5. 使用 mpi.recv.Robj 在每个处理器上接收对象，
- 6. 使用 rstream.packed 函数在每个处理器上解包 rstream 对象。

此时，每个节点上的随机数将对应于“独立”流，并可以按照任务分配的任何顺序使用。

我们为 R 中的 rstream 设计的方案示例在下所示的 rstream 摘录中。

```r
> library (rstream)
> library (rmpi)
> mpi.spawn.Rslaves(nclaves = 3)
3 slaves are spawned successfully. 0 failed.
master (rank 0, comm 1) of size 4 is running on: localhost
> slave1 (rank 1, comm 1) of size 4 is running on: localhost
> slave2 (rank 2, comm 1) of size 4 is running on: localhost
> slave3 (rank 3, comm 1) of size 4 is running on: localhost
> create a list of lists. rstream.mg32k3 objects
> rgList <- vector(length = 4, mode = "list")
> rgList <- c(new("rstream.mg32k3a", c(1, 2, 3, 4, 5, 6)), replicate(3, "rstream.mg32k3a"))
> pack the objects that will be sent to the processors
> for(i in 1:4) rstream.packed(rgList[[i]]) <- TRUE
> load the package and send the packed rstream objects
> library(rstream)
> for(i in 1:3) mpi.send.Robj(rgList[[i]])
> mpi.setup.rstream(seed = 1:6)
> mpi.recv.Robj(myRng)
> unpack the objects on the processors
> rstream.packed(myRng) <- FALSE
> generate the random numbers
> mpi.remote.exec(rstream.sample(myRng, 1))
X1 X2 X3 X4
1.000109498 0.701715 0.476142 0.0469019
> rstream.sample(rgList[[1]], 1).
```

初始步骤是导入 rstream 和 rmpi 包。生成三个从机，并创建一个列表向量来存放将发送到处理器的 rstream 对象。第一个 rstream 对象使用 `new` 函数和向量 (1, 2, 3, 4, 5) 创建。其余三个 rstream 对象类似地使用 `replicate` 创建并用于 `rgList`。`rgList[[1]]` 属于主进程，列表元素不需要打包。下一步是在每个从机上加载 rstream 包。这通过 `mpi.bcast.cmd` 函数实现。使用 `for` 循环配合 `mpi.send.Robj` 函数将打包的 rstream 对象发送到从机，处理器通过 `mpi.recv.Robj` 接收它们。使用 `mpi.bcast.cmd` 函数告诉每个从机解包其 rstream 对象，通过应用 `rstream.sample` 函数产生每个流的第一个随机数。将这些值与 MPI 和 OpenMP 示例中获得的值进行比较，显示我们复制了之前获得的流。

使用 multicore 包使用 rstream 更加简单。通过下面的代码使用 `mclapply` 可以获得与 Rmpi 相同的随机数：

```r
> library(rstream)
> library(multicore)
> rngList <- vector(length = 4, mode = "list")
> rngList <- c(new("rstream.mg32k3a", seed = c(1, 2, 3, 4, 5, 6)), replicate(3, new("rstream.mg32k3a")))
> mclapply(rngList, function(a) rstream.sample(a, 1))
```

[1]
[1] 0.000109498
[2]
[1] 0.701715
[3]
[1] 0.476142
[4]
[1] 0.0469019

因此，我们通过 OpenMP、MPI、Rmpi 和 multicore 生成了相同的随机流。

# 并行随机数生成

# 11.6 练习

11.1. 创建一个使用牛顿方法的列表 11.2 的替代版本。

11.2. 开发列表 11.3 中 MPI 的并行 ANOVA 程序，，用于 OpenMP。

11.3. 在练习 11.2 中，假设数据在 R 中如下生成：

```r
> set.seed(123)
> a <- rnorm(4000000)
> write(a, "aovVector.txt", ncol = 1)
```

将 aovVector.txt 中的数据读入 OpenMP 程序并进行重塑以匹配分析。执行重塑的代码所示：

```cpp
int j;
#pragma omp parallel for
for(int i = 0; i < 4; i++)
    for(int j = 0; j < 1000000; j++)
        pa[i][j] = ra[i * j];
```

其中 pa 和 ra 分别是持有从 R 创建的初始数组的指针以及用于重塑数据的 4 x 1000000 数组，行代表不同的“处理”。证明这种方法失败了，解释原因并修复问题。

11.4. MPI "broadcast" 函数的原型为

```cpp
void MPI::COMM_WORLD.Broadcast(void* buf, int count, MPI_Datatype datatype, int root)
```

该函数提供了处理器之间更直接的通信，使我们能够避免在 Send 和 Recv 中使用的循环。参数与 Send 的相同，直到遇到原型中的 root 参数。后一个参数代表要将其 buf 分发到所有处理器的处理器秩。所有处理器必须调用 Bcast。

11.5. Bcast 的相反效果可以通过 MPI 函数 Gather 获得。它将所有处理器的信息收集到一个处理器中（通常是处理器 0）。

```cpp
void MPI::COMM_WORLD.Gather(void* sendbuf, int count, MPI_Datatype datatype, void* recvbuf, int count, MPI_Datatype datatype);
```

数量 sendbuf 是指向从每个处理器发送到 0 的 count 个位置的指针。这些随后被收集到 recvbuf 中，recvbuf 需要在处理器 0 上定义，大小等于 count 与处理器数量（包括处理器 0）的积。与 Bcast 情况一样，Gather 函数必须由所有处理器调用。

# 练习

编写一个 MPI 程序从每个处理器发出问候消息。消息的正文应由秩为 0 的处理器使用 Bcast 函数发送。然后每个处理器应该提供其自己的自定义内容，例如，在打印到输出的消息中包含其特定的秩。

