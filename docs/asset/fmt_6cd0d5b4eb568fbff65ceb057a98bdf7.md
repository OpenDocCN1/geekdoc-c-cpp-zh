
赋值语句的右成员是一个条件表达式，它评估圆括号内的表达式。如果结果为真，我们赋值问号后面的值；否则，我们赋值冒号后面的值。此类表达式在 C 语言中经常被使用。

## 处理音频流

如果用户没有提供 `-d` 选项标记，`endpoint` 被赋值为文件的总长度，`dur` 被设置为相应的秒数。注意，此除法的两个成员之前已分别转换为 `double` 以产生可靠的结果。

与上一个示例一样，如果打开的文件通道数大于二，程序将结束，因为它只支持单声道和立体声文件。`psf` 库函数

```c
psf_andSeek(sfd, counter, PSF_SEEK_SET);
```

将当前文件指针移动到第二个输入参数（`counter` 变量）的位置。`PSF_SEEK_SET` 参数是一个宏，表示文件指针已从文件开始移动。（其他选项还有 `PSF_SEEK_CUR`，它从当前位置移动，以及 `PSF_SEEK_END`，它从文件末尾向后计数。）

如果用户没有提供音频文件名，则显示错误信息（命令行语法）并终止程序。初始化 `postfix` 库并像在 `player.c` 中一样打开文件。完成后，程序向控制台提供有关打开文件的的一些信息，例如其名称和采样率。

### 3.4.1 FIFO 缓冲区

如果之前的示例用于实时流，且如果样本块被完全播放，将会出现一个延迟，在此期间程序将计算新块。如果这个延迟超过了采样周期，音频接口将保持片刻不向输出。这将导致声音断断。为了避免断断，解决方案是使用多个样本块。在这种情况下，传递给 `outBlock()` 函数的块在被 DAC 播放之前复制到另一个内部块，程序可以自由计算另一个块。这种技术通常被称为“双缓冲”。如有必要，可以在转换器阶段填充多个块。这时，我们可以拥有“三缓冲”、“四缓冲”等。

缓冲是实时流的一项重要技术，用于流的缓冲方案被称为 FIFO（先进先出）队列或循环缓冲区。实时缓冲区可以是同步或异步的。当项目的速率恒定时同时（例如音频或视频流），我们处理的是同步流；如果速率不恒定（例如 MIDI），我们处理的是异步流。缓冲区有两种：输入缓冲区和输出缓冲区。输入缓冲区接收来自输入设备的数据并为程序提供数据。数据经过程序处理后最终发送到输出缓冲区，后者将数据发送到输出设备。输入 FIFO 缓冲区由一个内存块和一个将来自输入源的项目插入到缓冲区头的路径（此操作通常称为“推”）组成，持续操作直到没有可用空间。如果程序的平均处理速度不足以提取和处理数据，则可能发生输入缓冲区满的情况。事实上，每个项目在缓冲区中停留的时间应该是有限的，然后必须由程序本身从缓冲区尾提取并移除以便进行处理（此操作通常称为“弹出”）。如果输入缓冲区为空，程序将暂时停止处理并等待更多数据可用。

# 与音频流交互

在输出缓冲区的情况下，数据项由程序生成并推送到缓冲区的头部。输出设备从缓冲区的尾部接收数据项，并在需要时将其发送到输出端。处理后的数据由输出设备从缓冲区中弹出。如果缓冲区完全满（这是一种正常情况），程序将等待缓冲区能够接收更多数据。请注意，在输出缓冲区的情况下，如果程序提供处理后数据的速度慢于它们发送到输出端的速度，输出缓冲区可能会变为空。在同步实时处理中，输出缓冲区为空是一种不正常的、病理性的状态，在这种情况下，传输的项（例如，音频 DAC 中的样本，或者在你的 CD 刻录机中录制 CD 的情况）在传输时必须保持严格的周期性。这种情况也被称为“缓冲区欠载（buffer undererr）”。

简而言之，FIFO 有两种类型：输入缓冲区和输出缓冲区。对于输入缓冲区，数据项从外部接收，并由输入设备推入缓冲区。程序的任务是从缓冲区中推出此类数据项以进行处理。在实时处理中，程序必须保持缓冲区为空，或者至少不满。如果程序弹出数据的速度不够快，缓冲区可能会变满，导致传入的数据丢失。对于输出缓冲区，数据项由程序生成并推入输出缓冲区。在实时同步流传输中，输出设备以严格恒定的速率从缓冲区中弹出此类数据项。程序的职责是保持缓冲区满，或者至少不空。如果程序推入数据的速度不够快，缓冲区可能会变空并发生断音（drop-outs），从而破坏流操作的规律性。

缓冲区越大，避免“缓冲区欠载”的安全性就越高。永远无法绝对确定这种病理状态是否会发生；你可以相信，在合理的缓冲区大小下，正常情况下不会发生缓冲区欠载。

为什么我们不在实时音频流传输中使用巨大的缓冲区来获得完全的安全保障呢？在实时处理中使用大缓冲区有一个缺点，而且这个缺点与缓冲区的大小成正比：这就是所谓的延迟（latency）。理论延迟是在 FIFO 缓冲区中推入数据项与随后的弹出该数据项的动作之间经过的平均时间。在音频流的情况下，这种延迟与缓冲区的大小成正比，与采样率成反比。通常延迟以毫秒为单位，因此最大延迟通过以下公式计算：

```
maxlatency = 1000 * blockSize / sampleRate
```

其中 `blockSize` 是 FIFO 缓冲区的大小（例如，在三帧缓冲的情况下为 3），`blockSize` 是每个块的采样帧数（例如 512 个立体声帧），而 `sampleRate` 是采样率（例如 44,100 Hz）。在这种情况下，最大延迟为：

$latency = 1,000 \times 3 \times \frac{512}{44,100} \approx 34.83\text{ ms}$

即 34.83 ms（最大延迟时间）。现在我们必须使用以下公式计算最小延迟：

$minlatency = 1,000 \times (\text{bufferSize} - 1) \times \frac{\text{blockSize}}{\text{sampleRate}}$

即：

$minlatency = 1,000 \times 2 \times \frac{512}{44,100} \approx 23.22\text{ ms}$。

理论平均延迟通过最大和最小延迟之间的平均值获得：

$\text{averageLatency} = \frac{\text{minlatency} + \text{maxlatency}}{2}$

即：

$\text{averageLatency} = \frac{34.83 + 23.22}{2} = 29.02\text{ ms}$。

记住，这是一个理论值，实际延迟总是比理论延迟大。此外，在输入和输出数据同步传输（全双工，某些数字效果如吉他失真单块板可能需要）的情况下，理论延迟是输入缓冲区和输出缓冲区以及块大小的延迟之和。

选择合适的缓冲区大小和块大小是在延迟和防止欠载的安全性之间的权衡。因此，大多数商业音频程序留给用户来自定制最佳缓冲区大小，这只能通过试错测试来实现。

总结：与其直接将数据项发送到输出端，使用 FIFO 缓冲区至少有三个原因：

- 在同步流操作中，物理输出（或输入）设备必须保证完全恒定的速率和精确的时间控制，但计算机倾向于以不规则的速度处理数据；通过用一定数量的数据项填充缓冲区，始终会有至少有一个项要发送。
- 在同步和异步流操作中，数据项的速度可能快于输出设备能够处理的速度，因此某些项可能会丢失。通过在缓冲区中存储“过载”的项，我们保证所有项都能被输出设备依次识别。
- 处理和传输数据块通常比逐个处理单个数据元素要快。

## 3.4.2 主机驱动和回调机制

由于设备驱动程序通常向用户隐藏缓冲机制，因此实现很少是一个问题。尽管如此，使用这些技术仍然需要基础知识。例如，当我们在 `player.c`、`player2.c`、`playerIMP.cpp` 和 `playerGUI.cpp` 程序中使用 `outInterleaved()` 和 `outMono()` 时，这些函数（属于库）实际上隐藏了缓冲，程序员必须提供一个生成每个块并分配数组的例程。

有比阻塞高效得多的机制。其中包括多线程、主机驱动和回调机制。这些方法通常在同一个应用程序中结合。我们已经在 `playerIMP.cpp` 和 `playerGUI.cpp` 中看到了使用多线程的方法。

对 GUI 事件生成的消息进行响应。我们已经在 `playerGUisimple.cpp` 和 `playerGUI.cpp` 程序中见过这种回调函数了。通常，学习新概念的最佳方法是看到它应用于实际示例中。这正是我们现在要做的，为了使用 Portaudio 库提供的回调机制。在下一节中，我们将处理一个基于 Portaudio 的全双工音频流的回调机制示例。

## 3.4.3 使用 Portaudio 库

Portaudio 库¹⁹ 是一个标准的、开源的跨平台库，得益于其集成回调机制，它能够非常高效地支持实时音频流。Portaudio 将大多数依赖硬件的实现代码封装成通用 API，适用于多种操作系统，如 Windows、Linux、Solaris、FreeBSD、Mac OS 和 OS-X。从 v.19 版本开始，Portaudio 在同一个二进制文件中提供了多个 host-API 支持。这意味着，例如在 Windows 下，它可以在应用程序的单一构建中选择 MME、DirectX 和 ASIO。最终应用程序可以在运行时不同的 host-API 之间进行选择。Portaudio 同时提供了阻塞式 API² 和回调机制 API。程序员可以自由选择更适合特定应用程序的一种，但回调机制是目前最高效的（尽管编写起来比阻塞机制难一点）。

到目前为止，我们在程序中一直使用的是阻塞机制；但使用回调机制代替阻塞机制有两个主要优势：

- 它在输出缓冲区满或输入缓冲区为空时释放 CPU，使其脱离死循环，从而提高整体性能，并允许在 i/o 缓冲区填充时主执行线程继续运行（即主线程不会被缓冲区状态阻塞）。
- 它有助于将延迟降低到最低，特别是当使用面向低延迟的 host-API（如 ASIO 或 ALSA）时。

## 3.4.4 实践中的回调机制：HelloRing

本节所示的应用是一个控制程序，实现了一个实时环形调制²¹，用户可以设置调制频率。由于环形调制是一种极其简单的合成技术，这让我们专注于 Portaudio 提供的回调机制。

在本小节中，我们将重点关注以下内容：

- 如何编写一个专门适用于 Portaudio 的全双工音频回调函数（包含音频引擎）
- 如何获取并显示 Portaudio 支持的 host-API 的所有可用音频设备

## 处理音频流

- 如何为输入和输出选择特定设备
- 如何设置音频流的参数（例如通道数、采样率、块大小等）
- 如何初始化 Portaudio 并启动音频回调机制
- 如何停止回调机制并清理 Portaudio。

用户在程序启动时，从可用端口列表中选择音频输入和音频输出端口。从 Portaudio V19 版本开始，程序允许用户从目标机器上的所有 host APIs 中选择。这允许用户在 Windows 下选择 MME、DirectX 或 ASIO，在 Linux 下选择 OSS 或 ALSA 等。

程序 **HelloRing** 将接受立体声输入：两个通道都将通过一个正弦信号进行调制（频率由用户选择），并将两个调制后的通道发送到立体声输出。

以下是程序 `helloRing.c:` 要求的描述性总结：

编写一个控制程序，其中：

- 接受立体声音频信号作为输入，并使用 Portaudio v19 库提供的回调机制将处理后的信号实时流到立体声输出。
- 通过环形调制技术对输入信号进行实时处理，即输入信号的每个通道都与作为调制器的正弦信号相乘。该信号通过标准 C 库 `math.h` 提供的 `sin` 函数计算。
- 允许用户选择 (1) 调制正弦波的频率（赫兹），以及 (2) 在目标机器存在的多个 host-API 中选择输入和音频输出设备。

以下是我们完成该任务将涵盖的步骤大纲：

1. 包含所需的库头文件。
2. 进行外部声明：
    a. 定义帧块长度、采样率和 $2\pi$ 的宏常量（调制频率计算所需）。
    b. 将 portaudio 流指针声明为全局。
    c. 将采样增量声明为全局。
3. 定义包含环形调制引擎的回调函数（即一个将每个通道与正弦波相乘并输出结果的循环）。
4. 在函数内部定义所有初始化内容。初始化函数必须：
    a. 询问用户并获取调制频率
    b. 计算采样增量并将其存储在相应的全局变量中
    c. 初始化 `Portaudio` 以运行
    d. 显示每个 host-API 的所有可用音频输出设备，并要求用户选择其中一个
    e. 填充相应的结构。该结构将包含音频流的信息，如所选设备、通道数、格式等，用于打开音频流。
    f. 显示每个 host-API 的可用音频输入设备，并要求用户选择其中一个
    g. 填充相应的结构
5. 在函数中定义终止工作。终止函数必须：
    a. 停止流
    b. 关闭流
    c. 关闭 Portaudio
6. 定义 `main()` 函数。main 函数需要：
    a. 调用初始化函数
    b. 开始一个在按键时停止的循环
    c. 终止 Portaudio

以下是 `helloRing.c` 的内容：

```c
#include <stdio.h>
#include <math.h>
#include "portaudio.h"
#define FRAME_BLOCK_LEN 256
#define SAMPLING_RATE 44100
#define TWO_PI (3.14159265f * 2.0f)
PaStream *audioStream;
double si = 0;
int audio_callback(const void *inputBuffer, void *outputBuffer,
unsigned long framesPerBuffer,
const PaStreamCallbackInfo *timeInfo,
PaStreamCallbackFlags statusFlags,
void *userData)
{
    float *in = (float*)inputBuffer, *out = (float*)outputBuffer;
    static double phase = 0;
    for(int i=0; i < framesPerBuffer; i++) {
        float sine = sin(phase);
        *out++ = *in++ sine; /* 左通道 */
        *out++ = *in++ sine; /* 右通道 */
    }
    phase += si;
    return paContinue;
}
void init_stuff() {
    float frequency;
    int i,id;
    const PaDeviceInfo *info;
    const PaHostApiInfo *hostapi;
    PaStreamParameters outputParameters, inputParameters;
    printf("Type the modulator frequency in Hertz: ");
    scanf("%f", &frequency); /* 获取调制频率 */
    si = frequency / SAMPLING_RATE; /* 计算采样增量 */
    printf("Initializing Portaudio. Please wait...\n");
    Pa_Initialize(); /* 初始化 portaudio */
    for (i=0; i < Pa_GetDeviceCount(); i++) {
        info = Pa_GetDeviceInfo(i); /* 获取当前设备信息 */
        hostapi = Pa_GetHostApiInfo(info->hostapi); /* 获取 host API 结构 */
        if (info->maxOutputChannels > 0) { /* 设备支持输出 */
            printf("%d: [%s] s (output)\n", i, hostapi->name, info->name);
        }
    }
    printf("Type audio device number: ");
    scanf("%d", &id); /* 从用户获取输出设备 ID */
    info = Pa_GetDeviceInfo(id); /* 获取所选设备结构 */
    hostapi = Pa_GetHostApiInfo(info->hostapi); /* 获取 host API 结构 */
    printf("Opening audio device [%s]\n", hostapi->name, info->name);
    outputParameters.device = id; /* 选择的 ID */
    outputParameters.channelCount = 2; /* 立体声输出 */
    outputParameters.sampleFormat = paFloat32; /* 32位浮点输出 */
    outputParameters.suggestedLatency = info->defaultLowOutLatency; /* 设置默认为 NULL/*无特定信息 */
    outputParameters.hostApiSpecificStreamInfo = NULL;
    // ... 后续实现
}
```

```c
for (i=0; i < Pa_GetDeviceCount(); i++) {
    info = Pa_GetDeviceInfo(i); /* get information from current device */
    hostapi = Pa_GetHostApi(info->hostApi); /* get info from host API */
    if (info->maxInputChannels > 0) /* if curr device supports input */
```
