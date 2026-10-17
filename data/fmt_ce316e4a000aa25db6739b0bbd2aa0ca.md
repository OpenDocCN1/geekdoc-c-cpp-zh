
```cpp
ret[i] = runSimulation();
}

return ret;

}
```

这段代码中没有实际的数学计算，所以问题似乎不在此处。猜测 `runSimulation` 方法有问题是个合理的假设。你可以在第 265 页的图 15.4 中看到该方法的代码。

即使你逐行阅读代码，你可能也会发现很难在这个代码中找到 bug。调试器可以通过允许你在任何点暂停执行并打印出你感兴趣的任何变量的值来帮助你。

为此，你应该退出调试器。在重启之前，我们插入一个新的“断点”。这仅仅是一个我们希望调试器暂停程序执行的地方，以便我们可以查看正在发生的事情。

你应该打开文件 `HedgingSimulator.cpp`，并点击窗口右侧边缘，靠近 `HedgingSimulator` 开始的第 39 行处。你需要点击图 15.3 中显示球体的边缘位置。如果在正确的位置点击，会出现一个代表断点的红色球体。

创建断点后，当你按下 **F5** 再次运行代码时，调试器将在断点处暂停执行。

现在，你可以通过按下 **F10** 来逐行跟踪代码中正在发生的事情。你可以在菜单中找到此命令：**Debug** → **Step Over**。

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_274_0.png)

图 15.3：插入断点。断点以源代码边缘的球体显示。你可以看到第 40 行的球体。点击边缘以添加和删除断点。

每次按下 `F10` 时，下一行代码将执行。你可以通过查看显示区域中标记为 `Locals` 的部分来观察局部变量值的变化。

如果你逐行执行代码，你应该能够看到利息计算是不正确的。找到问题后，你应该停止调试器并重新测试代码，直到 `testDeltaHedgingMeanPayoff` 通过。

完成这些后，代码中仍将保留一个故意留下的 bug。修复它留作练习。

## 15.3 使用 GDB 进行调试

`GDB`（Gnu 调试器）是一个免费的调试器，是 Unix 系统上使用的标准调试器。如果你在 Windows 上工作，应该跳过这一节，阅读第 15.4 节。

`GDB` 有一个命令行界面，对用户不太友好。实际上，如果你在 Unix 上开发 C++，你可能需要考虑使用某种形式的“GDB 前端”来使其更容易使用。例如，你可以将 `GDB` 与 `vim` 和 `emacs` 等流行文本编辑器集成。也有可用的集成开发环境，如 `Eclipse`。然而，我们将只讨论如何从命令行使用 `GDB`。

要使用 `GDB`，你必须做的第一件事是确保使用 `gcc` 的调试选项编译了你的代码。如果你使用的是我们的标准 `Makefile`，这将自动完成。`Makefile` 中的 `CFLAGS` 变量为此使用了 `-g` 和 `-D_GLIBCXX_DEBUG` 标志。如果你不关心调试，而是希望代码运行得尽可能快，你应该移除这些选项并替换为适当的优化选项。

### 15.3.1 使用 GDB 获取堆栈跟踪

`GDB` 最重要的用途是找到包含错误的代码行。`FMLib15` 包含一些故意的 bug。让我们看看如何使用 `GDB` 快速找到第一个 bug 的原因。

编译 `FMLib15` 后，你应该通过在 Unix shell 中输入以下命令在调试器中运行它。

```bash
gdb FMLib
```

注意，我们假设 `gdb` 在你的路径上，且当前工作目录包含 `FMLib15`。

`GDB` 将启动到一个状态，你可以输入命令来告诉 `GDB` 你希望它在此调试会话中如何表现。例如，你可能想输入命令让它暂停程序执行到特定行，或在特定错误发生时暂停执行。输入这些命令后，你将输入命令 `run`，你的程序将在调试器中执行。

我建议在输入 `run` 命令执行之前，至少给调试器以下指令：

1. 告诉调试器，如果任何代码调用终止 C++ 程序执行的 `abort` 函数时，暂停执行。通过输入以下内容做到这一点：

```bash
break abort
```

2. 告诉调试器，如果执行 `throw` 语句时，暂停执行。通过输入以下内容做到这一点：

```bash
catch throw
```

除了在这些事件发生之一时暂停外，当代码中出现某些错误时，`GDB` 也会暂停。例如，如果你试图访问程序没有访问权限的内存，会发生段错误。当这种情况发生时，`GDB` 会自动暂停，无需你进一步配置 `GDB`。

输入上述命令后，键入 `run`。这将执行 `FMLib` 直到发现第一个 bug 的位置。执行将在此时暂停。

以下是使用 `gdb` 在我的计算机上运行 `FMLib` 时出现的打印输出的末尾：

## 15.3.2 使用 GDB 设置断点和单步调试

```
Calling testPutCallParity()
testPutCallParity() passed.
Calling testDeltaHedgingMeanPayoff()
/usr/lib/gcc/x86_64-pc-cygwin/5.3.0/include/c++/debug/vector
        :406:error:
        attempt to subscript container with out-of-bounds index
        1000, but
        container only holds 1000 elements.
Objects involved in the operation:
sequence "this" @ 0x0xffffc7a0 {
    type = NSt7__debug6vectorIsAIdEEE;
}
Breakpoint 1, 0x000000018012c574 in abort () from /usr/bin/
cygwin1.dll
(gdb) backtrace
#0  0x000000018012c574 in abort () from /usr/bin/cygwin1.dll
```

前三行是由 `FMLib` 本身打印输出的。它们告诉我们函数 `testPutCallParity` 运行正常。但在函数 `testDeltaHedgingMeanPayoff` 中发生了一个问题。要看出这一点，只需注意我们有一条日志语句说 `testPutCallParity` 已通过，但没有针对 `testDeltaHedgingMeanPayoff` 的对应语句。

下一个错误告诉我们，错误是在名为 `vector` 的 C++ 文件的 `406` 行检测到的。这并不意味着 bug 在 `vector` 文件中，只是说它在那里被检测到。由于 `vector` 是标准 C++ 库的一部分，它包含 bug 的可能性极低。我们可以猜测，是我们自己的代码在使用有问题的 `vector`。

接下来的几行极难解释，对我们目前来说也没太大用处。让我们忽略它们，继续看最后一行。这告诉我们执行已停止在 `Breakpoint 1`。这意味着它是由于我们之前输入的命令 `break abort` 而停止的。有帮助的是，最后一行提到它停止在函数 `abort()` 中。不太有帮助的是，该行还告诉我们要哪个库包含 `abort` 函数及其内存地址。

要了解正在发生的事情，请输入命令

```
backtrace
```

该命令告诉调试器打印当前堆栈的状态。这只是一个列出当前正在运行哪些函数的列表。在堆栈的底部，你会看到程序的 `main` 方法；在顶部，你看到的是正在执行的当前函数。以下是 `backtrace` 在我的计算机上运行时的打印输出。

```
#0  0x000000018012c574 in abort () from /usr/bin/cygwin1.dll
#1  0x00000003f508a005 in cygstdc++-6!
_ZNK11__gnu_debug16_Error_formatter8_M_errorEv () from /usr/
bin/cygstdc++-6.dll
#2  0x00000001004246be in std::__debug::vector<double, std:::
allocator<double> >::operator[] (this=0xffffca0, __n=1000)
at /usr/lib/gcc/x86_64-pc-cygwin/5.3.0/include/c++/debug/
vector:406
#3  0x000000010041650f in HedgingSimulator::runSimulation (this
=0xffffcac0)
at HedgingSimulator.cpp:64
#4  0x0000000100416289 in HedgingSimulator::runSimulations (this
=0xffffcac0,
nsimulations=1) at HedgingSimulator.cpp:35
#5  0x0000000100416770 in testDeltaHedgingMeanPayoff ()
at HedgingSimulator.cpp:105
#6  0x0000000100416bd3 in testHedgingSimulator () at
HedgingSimulator.cpp:118
#7  0x0000000100402466 in main () at main.cpp:43
```

最后一行告诉我们，当执行 `main` 函数时发生了错误。错误实际上是在执行 `main.cpp` 的第 43 行时发生的。你可以从 `main.cpp:43` 的文本中看出这一点。

看倒数第二行，我们可以看到该行必须调用了 `testHedgingSimulator`。后者又调用了 `testDeltaHedgingMeanPayoff`。通过这种方式遍历堆栈，你可以看到所有当前正在执行的函数。

一般来说，堆栈的底部不会揭示太多关于问题成因的信息。要分析 bug，你应该从顶部开始向下查找，直到到达你编写的第一行代码。

在上面的例子中，第 #0 行是对函数 `abort()` 的调用。第 #1 行很难解释，但我们可以说的是，它不指涉我们编写的任何代码。第 #2 行正在执行 `vector` 的第 406 行。最后，在第 #3 行，我们到达了一些我们自己编写的代码。是 `HedgingSimulator.cpp` 的第 64 行包含问题。

让我们看看那行代码。

```
double S = pricePath[nSteps];
```

如果你查看相邻的代码，问题的原因应该相当明显。我们正在访问 `pricePath` 中索引为 `nSteps` 的元素，但实际上价格路径长度仅为 `nSteps`。我们可以看到代码实际上应该写成：

```
double S = pricePath[nSteps - 1];
```

既然我们知道如何修复这个 bug，我们应该结束调试会话。输入 `quit` 退出调试器。然后你可以终止正在运行的进程并退出调试器。

现在你应该修正代码，重新编译，并在调试器中再次运行它。代码仍然会失败，但堆栈跟踪应该会有所不同，表明 bug 在其他地方。

在调试器暂停程序之前的打印输出现在应该如下所示：

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_278_0.png)

除了最后一行外，所有打印输出都是由我们的测试库生成的。它告诉我们 `HedgingSimulator.cpp` 第 106 行处的一个 `ASSERT_APPROX_EQUAL` 语句已失败。

如果我们在文本编辑器中查看该代码，我们会发现在运行 `testDeltaHedgingMeanPayoff` 时出现了问题。

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_278_1.png)

我们可以看到，我们期望对冲模拟的损益（PnL）大约为零，但实际上它是一个荒谬的大数 $-5.90148 \times 10^{300}$。显然，我们的 `HedgingSimulator` 类中的 `runSimulations` 函数存在数学错误。不幸的是，在这种情况下，如果在 `gdb` 中运行 `backtrace` 命令，它不会提供太多额外信息。

为了进一步取得进展，首先要做的是通读 `runSimulations` 代码，看看是否有明显的问题。以下是代码：

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_278_2.png)

```
std::vector<double> ret(nSimulations);
for (int i = 0; i < nSimulations; i++) {
    ret[i] = runSimulation();
}
return ret;
```

这段代码中没有实际的数学计算，所以这似乎不太可能是问题所在。看来 `runSimulation` 方法才是问题所在。你可以在第 265 页的图 15.4 中看到该方法的代码。

即使你逐行阅读，可能也很难发现这段代码中的 bug。调试器可以通过允许你在任何点暂停执行并打印你感兴趣的任何变量的值来帮助你。

为此，你应该退出调试器并重启。但这次在执行 `run` 命令之前输入命令

```
break HedgingSimulator::runSimulation
```

这将在 `runSimulation` 函数的开头暂停执行。

当程序暂停时，你会看到类似于以下输出。

```
Calling testDeltaHedgingMeanPayoff()
Breakpoint 5, HedgingSimulator::runSimulation (this=0xffffc920)
    at HedgingSimulator.cpp:41
41      double T = toHedge->getMaturity();
```

这表明执行已暂停在 `HedgingSimulator.cpp` 的第 41 行。给定的代码行尚未执行。要执行它，请输入 `next`。

这应该已经为局部变量 `T` 分配了一个值。要查看被分配的值，请输入 `print T`。

现在你可以逐行单步执行 `runSimulation` 函数，同时检查变量的值。你应该能够确认 `runSimulation` 函数中利息的计算存在问题，然后你可以修复它。

代码中仍剩下一个 bug。修复它留作练习。

### 15.3.3 其他命令和特性

让我们简要提及一些我们尚未涵盖的有用的 `GDB` 特性。

- 1. 可以使用命令 `help` 来查找其他有用命令的名称。
- 2. 命令 `step` 可用于跟踪代码进入其他函数的执行过程。相比之下，`next` 始终在单个函数内移动。
- 3. 你可以在主目录中创建一个名为 `.gdbinit` 的文件，其中包含在 `gdb` 启动时应始终执行的命令。下面显示了一个简单的示例文件，该文件可确保 `gdb` 在调用 `abort` 和 `throw` 语句时始终暂停：

```
set breakpoint pending on
break abort
catch throw
```
