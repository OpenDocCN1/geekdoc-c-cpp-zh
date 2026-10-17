
```cpp
HedgingSimulator simulator;
simulator.setNSteps(1000);
vector<double> result
        = simulator.runSimulations(1);
ASSERT_APPROX_EQUAL(result[0], 0.0, 0.01);
}
```

我们可以看到，尽管预期对冲模拟的损益（PnL）大约为零，但实际上却是一个荒谬的大数 $-5.90148 \times 10^{300}$。显然，我们 `HedgingSimulator` 类中的 `runSimulations` 函数存在数学错误。在这种情况下，如果你使用调试器在此处中断执行并查看调用栈，你会发现它并没有揭示任何我们此前未能推断出的新信息。

为了进一步取得进展，首先要做的是通读 `runSimulations` 的代码，看看是否存在明显的问题。代码如下：

```cpp
std::vector<double>
HedgingSimulator::runSimulations(int nSimulations)
    const {
    std::vector<double> ret(nSimulations);
    for (int i = 0; i < nSimulations; i++) {
        ret[i] = runSimulation();
    }
    return ret;
}
```

这段代码中没有实际的数学计算，因此问题似乎不太可能出在这里。看起来 `runSimulation` 方法才是问题的根源。你可以在第 265 页的图 15.4 中看到该方法代码。

即使你逐行阅读这段代码，也很难发现其中的错误。调试器可以帮助解决这一问题，因为它允许你在任何位置暂停执行，并打印出你感兴趣的任何变量的值。

为了做到这一点，你应该先退出调试器。在重新运行之前，我们需要插入一个新的“断点”。这只是一个希望调试器暂停程序执行的位置，以便我们可以观察正在发生的事情。

你应该打开文件 `HedgingSimulator.cpp`，并在窗口右侧边缘第 39 行 `HedgingSimulator` 开始的地方点击。你需要点击图 15.3 中边缘显示球体的那个位置。如果你点击了正确的位置，一个代表断点的红色球体会出现。

创建断点后，当你下次通过按 `F5` 运行代码时，调试器将在断点处暂停执行。

现在，你可以通过按 `F10` 逐行跟踪代码中的执行过程。你可以在菜单中找到此命令，即“调试 → 单步过（Step Over）”。

![](img/70e8b6971c8420e92597c05233ce9700_274_0.png)

**图 15.3**：插入断点。断点在源代码边缘显示为一个球体。你可以看到第 40 行的球体。在边缘点击即可添加或移除断点。

每次按 **F10** 时，下一行代码将被执行。通过查看显示屏上标记为 *Locals*（本地变量）的区域，你可以看到这对局部变量值的影响。

如果你逐行单步执行代码，你应该能看到利息计算是不正确的。一旦找到问题，你应该停止调试器并重新测试代码，直到 `testDeltaHedging-MeanPayoff` 通过为止。

完成上述步骤后，代码中仍会留下一个故意设计的错误。修复这个错误将留作练习。

### 15.3 使用 GDB 进行调试

`GDB`（Gnu Debugger）是一个免费的调试器，也是 Unix 系统上使用的标准调试器。如果你在 Windows 上工作，应该跳过本节并阅读第 15.4 节。

`GDB` 拥有命令行界面，其用户友好性并不特别高。实际上，如果你在 Unix 上开发 C++，可能会考虑使用某种“GDB 前端”，以使其更易于使用。例如，你可以将 `GDB` 与流行的文本编辑器（如 `vim` 和 `emacs`）集成。也有可用的集成开发环境，例如 `Eclipse`。然而，我们将只讨论如何从命令行使用 `GDB`。

要使用 `GDB`，你必须做的第一件事是确保使用 `gcc` 的调试选项编译了你的代码。如果你使用的是我们的标准 `Makefile`，这将自动完成。`CFLAGS` 变量在 `Makefile` 中使用了 `-g` 和 `-D_GLIBCXX_DEBUG` 标志，正是出于这个原因。如果你对调试不感兴趣，而是希望代码运行得尽可能快，你应该移除这些选项，并替换为适当的优化选项。

#### 15.3.1 使用 GDB 获取堆栈跟踪

使用 `GDB` 最重要的用途是找到包含错误的代码行。`FMLib15` 包含一些故意的错误。让我们看看如何使用 `GDB` 快速找到这些第一个错误的根本原因。

一旦你编译了 `FMLib15`，你应该在 Unix shell 中输入以下命令，在调试器中运行它。

```bash
gdb FMLib
```

注意，我们假设 `gdb` 在你的路径中，并且当前工作目录包含 `FMLib15`。

`GDB` 将启动并进入一种你可以输入命令来告知 `GDB` 你希望它在本次调试会话中如何操作的状态。例如，你可能想要输入命令来告诉它在程序的特定行暂停执行，或者在特定错误发生时暂停执行。一旦你输入了这些命令，你将输入命令 `run`，你的程序将在调试器中执行。

我建议至少在执行 `run` 命令之前，给调试器输入以下指令：

- (i) 告诉调试器，如果任何代码调用了 `abort` 函数（该函数终止 C++ 程序的执行），则暂停执行。通过输入以下命令完成：

```bash
break abort
```

- (ii) 告诉调试器，如果执行了 `throw` 语句，则暂停执行。通过输入以下命令完成：

```bash
catch throw
```

除了在这些事件发生其中之一时暂停外，当你的代码发生某些错误时，`GDB` 也会暂停。例如，如果你尝试访问程序没有权限访问的内存，将会发生段错误（segmentation fault）。当这种情况发生时，`GDB` 会自动暂停，无需你进一步配置 `GDB`。

输入上述命令后，键入 `run`。这将执行 `FMLib`，直到发现第一个错误为止。随后执行将暂停。

以下是我在我的电脑上使用 `gdb` 运行 `FMLib` 时出现的打印输出的末尾部分：

```
Calling testPutCallParity()
testPutCallParity() passed.
Calling testDeltaHedgingMeanPayoff()
/usr/lib/gcc/x86_64-pc-cygwin/5.3.0/include/c++/debug/vector :406:error:
	 attempt to subscript container with out-of-bounds index 1000, but container only holds 1000 elements.
Objects involved in the operation:
sequence "this" @ 0x0xfffffc7a0 {
    type = NSt7__debug6vectorIsaIdEEE;
}

Breakpoint 1, 0x000000018012c574 in abort () from /usr/bin/cygwin1.dll
(gdb) backtrace
#0  0x000000018012c574 in abort () from /usr/bin/cygwin1.dll
```

前三行是由 `FMLib` 本身打印的。它们告诉我们，函数 `testPutCallParity` 运行正常，但函数 `testDeltaHedgingMeanPayoff` 中发生了问题。要看出这一点，只需注意到我们有一条日志语句表明 `testPutCallParity` 已通过，但没有对应的语句表明 `testDeltaHedgingMeanPayoff` 通过。

下一个错误告诉我们，该错误是在名为 `vector` 的 C++ 文件的第 406 行检测到的。这并不意味着 bug 在 `vector` 文件中，只是它在那里被检测到。由于 `vector` 是标准 C++ 库的一部分，它包含 bug 的可能性极小。我们可以猜测，是我们的代码中使用的 `vector` 出了问题。

接下来的几行非常难以解读，对目前而言也没什么太大用处。让我们忽略它们，转向最后一行。这告诉我们执行停止在了 `Breakpoint 1`。这意味着它是由于我们之前输入的 `break abort` 命令而停止的。有帮助的是，最后一行提到它停止在函数 `abort()` 中。不太有帮助的是，该行还告诉了我们 `abort` 函数所在的库及其内存地址。

要了解正在发生的事情的更多细节，输入命令

```bash
backtrace
```

此命令告诉调试器打印当前堆栈的状态。这只是一个当前正在运行的函数列表。在堆栈底部你会看到程序的 `main` 方法，在顶部你会看到当前正在执行的函数。以下是我在我的电脑上运行 `backtrace` 时的打印输出。

#### 15.3.2 使用 GDB 进行断点和单步调试

在调试器暂停程序之前，打印输出现在应该如下所示：

```
Calling testDeltaHedgingMeanPayoff()

ASSERTION FAILED

Expected -5.90148e+300

Actual 0

HedgingSimulator.cpp:106:

Catchpoint 2 (exception thrown), 0x00000003f512a787 in cygstdc++-6!
_ZNSt15__exception_ptr9operator()EPSt0
() from /usr/bin/cygstdc++-6.dll
```

除了最后一行以外的所有打印输出都是由我们的测试库生成的。它告诉我们，在 `HedgingSimulator.cpp` 的第 106 行，一个 **ASSERT_APPROX_EQUAL** 语句失败了。

如果我们在文本编辑器中查看该代码，我们会发现运行 **testDeltaHedgingMeanPayoff** 时出现了一个问题。

```cpp
static void testDeltaHedgingMeanPayoff() {
rng("default");
HedgingSimulator simulator;
simulator.setNSteps(1000);
vector<double> result
= simulator.runSimulations(1);
ASSERT_APPROX_EQUAL(result[0], 0.0, 0.01);
}
```

我们可以看到，我们期望对冲模拟的损益（PnL）大约为零，但事实上它却是一个极其大的数值 $-5.90148 \times 10^{300}$。显然，我们 `HedgingSimulator` 类中的 **runSimulations** 函数存在数学错误。不幸的是，在这种情况下，如果在 **gdb** 中运行 **backtrace** 命令，它不会提供太多额外信息。

为了进一步取得进展，首先要做的是通读 **runSimulations** 代码，看看是否有明显的问题。以下是代码：

```cpp
std::vector<double>
HedgingSimulator::runSimulations(int nSimulations)
const {
     std::vector<double> ret(nSimulations);
     for(int i = 0; i < nSimulations; i++) {
         ret[i] = runSimulation();
     }
     return ret;
}
```

这段代码中没有实际的数学计算，因此这似乎不太可能是问题所在。`runSimulation` 方法似乎是一个不错的猜测，它是问题所在。你可以在第 265 页的图 15.4 中看到该方法代码。

你可能会发现很难在这段代码中找出 bug，即使你逐行阅读。调试器可以帮助你，它允许你在任意点暂停执行并打印出你感兴趣的任何变量的值。

为此，你应该退出调试器并重新启动。但这次在执行运行命令之前，请输入命令

```bash
break HedgingSimulator::runSimulation
```

这将在 `runSimulation` 函数的开始处暂停执行。

当程序暂停时，你会看到类似以下的输出。

```
Calling testDeltaHedgingMeanPayoff()
Breakpoint 5, HedgingSimulator::runSimulation (this=0xffffc920)
 at HedgingSimulator.cpp:41
 41     double T = toHedge->getMaturity();
```

这表明执行已暂停在 `HedgingSimulator.cpp` 的第 41 行。给定的代码行尚未执行。要执行它，请输入 `next`。

这应该已经为局部变量 `T` 分配了一个值。要查看分配的值，请输入 `print T`。

现在你可以逐行单步执行 `runSimulation` 函数，检查沿途变量的值。你应该能够确认 `runSimulation` 函数中的利息计算存在问题，然后你应该能够修复它。

代码中仍然有一个 bug 未解决。修复它留作练习。

#### 15.3.3 其他命令和功能

让我们简要介绍一些我们没有涵盖的有用 `GDB` 功能。

1. 可以使用命令 `help` 来查找其他有用命令的名称。
2. 可以使用命令 `step` 来跟踪代码执行进入其他函数。相比之下，`next` 始终在单个函数内部移动。
3. 你可以在主目录中创建一个名为 `.gdbinit` 的文件，其中包含 `gdb` 启动时应始终执行的命令。下面展示了一个简单的示例文件，它确保 `gdb` 总是在调用 `abort` 和 `throw` 语句时暂停：

```
set breakpoint pending on
break abort
catch throw
```
