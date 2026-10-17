
```
    osMessageQueueGet();

    function_1();

    osDelay(10);

    function_2();

  }

}
```

线程（Thread）首先进入阻塞状态，等待消息到达。当消息数据到达时，线程将唤醒并调用 `function_1()`，然后它将再次进入阻塞状态，直到调用 `osDelay()` 函数。如果延迟超时，线程将恢复执行并调用 `function_2()`，然后进入阻塞状态，直到下一条消息到达。该线程有两个进入阻塞状态的点。如果所有其他线程也处于阻塞状态，将导致 `osIdleThread()` 运行。对于 RTOS 调度器来说，这两个 OS 调用之间没有本质区别，但对于电源管理而言，存在着重要的区别。当线程被 `os_message_wait()` 调用阻塞时，它是 true处于空闲状态，除非系统其他部分向它提供数据进行处理，否则它将无法继续。当线程为了电源管理之目的被 `osDelay()` 函数阻塞时，它在某种意义上仍然是唤醒的，因为它将在不需要从系统其他部分输入的情况下恢复处理。我们需要构建应用程序线程，使它们等待由系统其他部分触发的“事件”，执行其功能，然后等待下一次事件发生。这意味着每个线程现在都有一个关键阻塞点（图 11.11）。

![](img/950c01277f34327c3481ea2732620dca_459_0.png)

**图 11.11**
在阻塞点，线程已完成当前任务，并正在等待下一个事件以恢复处理。

如果我们这样构建所有系统线程，就可以识别出所有在关键阻塞点等待的线程。此时，应用程序真正处于空闲状态，我们可以将其放入更深层的低功耗状态。

## 电源管理策略

为了构建电源管理策略，我们首先需要一个全局变量，为系统上运行的每个线程持有两个标志（图 11.12）。

`uint32_t powerFlags`

| 任务挂起标志 | 任务运行标志 |
| :--- | :--- |

图 11.12

电源管理标志存储在全局变量中，并在空闲线程中进行监控。

每个线程有一个“线程运行”位和一个“线程挂起”位。接下来，我们需要编写一些简单的函数来控制这些位。当线程唤醒并开始执行代码时，我们需要设置线程运行位。由于多个线程正在访问电源标志，因此应该用互斥锁（mutex）对其保护。

```
void ThreadIsRunning(uint16_t Thread) {

    osWait(mutex,osWaitForever);

    powerFlags |= Thread;

    osRelease(mutex);

}
```

当它完成任务并准备返回等待状态时，我们需要清空线程运行位。

```
void ThreadIsSuspended(uint16_t Thread) {

    osWait(mutex,osWaitForever);

    powerFlags &= ~Thread;

    osRelease(mutex);

}
```

现在应用程序线程看起来如下：

```
@define APPLICATION_THREAD 1

Application_thread(void) {

    while(1) {

        ThreadIsSuspended(APPLICATION_THREAD);

        osWait(0x0001,osFlagsWaitAny,osWaitForever);

        ThreadIsRunning(APPLICATION_THREAD);

        function_1();

        osDelay(10);

        function_2();

    }

}
```

当系统的其他部分准备触发线程时（在本例中，通过发送消息），我们可以设置线程的挂起位。这确保了我们避免了调度器的任何问题。

```
void ThreadIsPending(uint16_t Thread) {

    osWait(mutex,osWaitForever);

    powerFlags |= (Thread << 8); //设置挂起位

    osRelease(mutex);

}
```

现在向我们的应用程序线程发送消息看起来如下：

```
ThreadIsPending(p_phaseA);

osThreadFlagsSet(tid_phaseA, 0x0001);
```

我们必须修改 `ThreadIsRunning` 例程，在应用程序线程恢复执行时清除此位。

```
void ThreadIsRunning(uint16_t Thread) {

    osMutexWait(powerMutex,osWaitForever);

    powerFlags |= Thread;

}
```

## Watch门

## RTOS 技术

## 集成中断例程

# 440 第 11 章

打开 `peripheral\General Purpose IO\GPOIB` 调试窗口。

使用 `debug\run` 开始运行代码。

在初始几秒后，你应该能看到应用程序线程正在切换 GPIO B 引脚的高字节。

打开 `View\Analysis\Performance analyzer`（视图\性能分析器）。

在这里，我们可以看到在这个简单的程序中，大部分运行时间都消耗在 `osRtxIdleThread()` 中（图 11.13）。

![](img/950c01277f34327c3481ea2732620dca_464_0.png)

图 11.13

在这个简单的程序中，处理器将所有时间都花在了空闲任务上。

选择 `RTX_Conf_CM.c` 文件并找到 `osRtxIdleThread()`，退出调试器。

取消 `__wfi();` 的注释并使用 `project\build` 重新编译并绑定代码。

使用 `debugstart` 重启仿真器并开始运行代码。

如果我们重新在性能分析器中查看项目，可以发现 `osRtxIdleThread()` 消耗的周期数大幅减少（图 11.14）。

![](img/950c01277f34327c3481ea2732620dca_464_1.png)

图 11.14

处理器停止在空闲循环中，而不是消耗能量。

# RTOS 技术 441

`__wfi()` 指令将处理器置于睡眠模式，这在 Cortex-M 处理器中是节省电的。然而，微控制器的外设仍在消耗能量。为了利用芯片制造商提供的更深低功耗模式，需要检测应用程序何时处于空闲状态，然后将设备放入更深的低功耗模式，直到它准备好重新开始处理。

# 现在检查应用程序线程。

```
void phaseA(void *argument) {

    for (::) {

        ThreadIsSuspended(p_phaseA);

        ThreadFlagsWait(0x0001,osFlagsWaitAny,osWaitForWait); // 等待事件标志 0x0001 /

        ThreadIsRunning(p_phaseA);

        LED_On(LED_A);

        signal_func(); // 调用通用信号函数 /

        ThreadIsPending(p_phaseB);

        ThreadFlagsSet(tid_phaseB,0x0001); // 发送到 Thread */

        osDelay(5); // 延迟 5 个时钟周期 /

        LED_Off(LED_A);

    }

}
```

在每个线程中，我们识别了关键阻塞点并用 `ThreadIsSuspended()` 和 `ThreadIsRunning()` 函数将其包裹。如果线程信号另一个线程，我们必须先调用 `ThreadIsPending()` 函数。

现在去 `osRtxIdleThread` 并注释掉 `__wfi()` 指令，同时取消 `enterLowPowerState()` 函数的注释。

`enterLowPowerState()` 函数检查标志位并决定进入哪种电源模式。

```
void enterLowPowerState(void) {

    if (powerFlags == ALL_THREADS_INACTIVE) {

        configureAndEnterDeepSleepMode();

    } else {

        configureAndEnterSleepMode();

    }

}
```

在每个低功耗配置函数中，我们通常会配置微控制器的电源模式并运行 `__wfi()` 指令。然而，为了演示目的，我们将留在函数中并简单地切换一个调试变量。

```
void configureAndEnterDeepSleepMode(void) {

    uint32_t delay;

    SCB->SCR |= (1<<SCB_SCR_SLEEPDEEP_Pos); // 启用深度睡眠模式

```

```
// _wfi();

// 让微控制器进入深度睡眠

//for(delay=0;delay<0x100;delay++);

// 简单延迟

debugSleep ^= 0x01;

// 切换调试变量

}
```

重新生成代码并重启调试器。

通过 `view\analysis window\system analyzer` 打开逻辑分析器窗口。

开始运行代码。

在代码运行几秒后，按下 `Min/Max Auto` 按钮并不断缩小比例，直到获得与下方相似的视图（**图 11.15**）。

![](img/950c01277f34327c3481ea2732620dca_466_0.png)

图 11.15

上方轨迹显示了睡眠调试变量。实块部分表示我们处于低功耗模式的状态。下方轨迹同样显示了睡眠调试变量。同样，实块显示了我们处于低功耗模式的位置。在这里，我们可以看到代码在待机模式以及应用程序代码运行执行期间是如何节省能量的。

在 `blinky.c` 中，取消第 171 行 `os_tsk_create (Monitor, 10);` 的注释。

这将启用看门狗监控线程，该线程将确保每个应用程序线程都正确运行。

要创建一个错误，取消 `blinky.c` 中 131 到 136 行代码的注释，这将允许应用程序运行几次然后删除线程 A。

构建代码并启动仿真器。

打开 `watchdog.c` 将 `ThreadWatchdogCounters` 数组添加到监视窗口（watch window）中。

在 `ThreadIsStalled = TRUE;` 代码行处添加断点。

# 打开 `debug\os support\RTX Thread and system` 窗口。

开始运行代码。

在代码运行几秒后，在代码运行几次闪烁序列后，它将从系统中删除 A（图 11.16）。

![](img/950c01277f34327c3481ea2732620dca_467_0.png)

图 11.16
任务 A 删除后的剩余线程。

线程将检测到挂起位已设置并增加 `ThreadWatchdogCounters`。

在监视窗口中观察 `ThreadWatchdog`（图 11.17）。

![](img/950c01277f34327c3481ea2732620dca_467_1.png)

图 11.17
看门狗计数器。

# 444 第 11 章

计数器 0 开始增加。当达到 `MAX_THREAD_COUNT` 时，我们将命中断点。

启动代码，`ThreadIsStalled` 变量将被设置。这种 RTOS 中的看门狗管理方法简单且可以复用。

# 启动屏障

如果你正在使用新的微控制器，良好的做法是在代码中添加一个“启动屏障”（startup barrier）。在开发早期，可能会导致微控制器进入难以通过调试端口连接的状态。如果发生这种情况，我们可以重新给板电源，修改源码并再次尝试。启动屏障就是一个简单的函数：

```
volatile uint32_t debuggerAttached__attribute__((at(0x2000FFFC)));

void startupBarrier(void)

{

if(debuggerAttached!=0x55555555)BKPT(0);

}
```
