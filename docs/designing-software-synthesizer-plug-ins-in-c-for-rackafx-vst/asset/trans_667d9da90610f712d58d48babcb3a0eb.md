

![](img/b42d0dca53f4a889d8162d55f7c8c05d_679_0.png)
图 10.6：每个圆角框代表单个样本，覆盖了一个八度的音高范围和一个由高度决定的速度范围。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_679_1.png)
图 10.7：四个区域；区域 2 和 4 经过影处理以便观察。

## 10.5 CWaveData 对象

让我们来看 CWaveData 对象。记住，它的作用是打开 .wav 文件并将音频提取到浮点缓冲区中。该对象可以处理具有任意通道数的文件，尽管解码交错样本取决于你。对于交错文件，通道的编码方式为 L、R、L、R、L、R 等。CWaveData 可以在 Windows 和 MacOS 上打开并读取以下 .wav 文件类型：

- 16 位有符号整数
- 封装在三个或四个字节中的 24 位有符号整数
- 32 位有符号整数
- 32 位浮点
- 64 位双精度浮点

它不读取 8 位文件（尽管你可以很轻松地做到），并且只读取 PCM 或未压缩文件。一段时间以来，样本文件的行业标准是 24 位整数，尽管这可能会发生。合成器文件都是 24 位的。使用用于 .wav 文件的字符串初始化 CWaveData 对象。它打开文件并将音频提取到新创建的浮点缓冲区。一旦成功，你就可以访问其成员变量来获取样本信息，例如 MIDI 单位音符、MIDI 音高分数、长度、通道数等。该对象可以重用以打开多个文件，但缓冲区将被销毁并根据新内容重建。我们将在荡器中使用一个 .wav 文件。如果你是经验丰富的 RackFX 用户，这个对象一直都在，尽管没有文档说明。表 10.1 显示了 CWaveData 的成员变量。

### SMPTE 格式

- 0 无 SMPTE 偏移
- 24 每秒 24 帧
- 25 每秒 25 帧
- 29 每秒 30 帧，带丢帧 (30 drop)
- 30 每秒 30 帧

### SMPTE 偏移

表 10.1：CWaveData 的成员变量为你提供了关于 .wav 文件所需的所有信息。

| 类型 | 变量名 | 描述 |
|---|---|---|
| float* | m_pWaveBuffer | 从 .wav 文件中提取的音频的缓冲区 |
| bool | m_bWaveLoaded | 如果对象成功打开并解析音频数据，则为 true |
| HANDLE | m_file | 文件句柄（仅限 Windows）——你可以安全地忽略它 |
| UINT | m_uNumChannels | 通道数 |
| UINT | m_usampleRate | 文件采样率 |
| UINT | m_usampleCount | 文件中的样本总数 |
| UINT | m_uLoopCount | 文件中的循环次数 |
| UINT | m_uLoopStartIndex | 第一次循环的起始索引 |
| UINT | m_uLoopEndIndex | 第一次循环的结束索引 |
| UINT | m_uLoopType | 循环类型值 |
| | 0 | 正向循环（正常） |
| | 1 | 交替循环（来回循环） |
| | 2 | 反向循环（倒序） |
| | 3-31 | 厂商特定 |
| UINT | m_uMIDINote | MIDI 单位音符数 |
| UINT | m_uPitchFraction | MIDI 音高分数 |
| UINT | m_uSMPTEFormat | SMPTE 格式 |
| UINT | m_uSMPTEOffset | SMPTE 偏移 |

SMPTE 偏移值指定了用于波形第一个样本同步/校准的时间。该值使用 0hhhhmmssff 格式，其中 hh 是小时的有符号值（-23 到 23），mm 是分钟的无符号值（0 到 59），ss 是秒的无符号值（0 到 59），ff 是帧的无符号值（0 到 79）。

CWaveData 对象只有两个成员函数，都涉及音频数据的提取。构造函数为：

```cpp
CWaveData(char* pFilePath = NULL);
```

如果你在构造时传递有效路径，它将用于一次性加载并初始化对象。如果你传递 NULL 指针，则不会分配对象的音频数据数组。

```cpp
bool initWithUserWAVEFile(char* pInitDir = NULL);
```

initWithWAVEFile() 仅适用于 Windows 版本。当你调用此函数时，会打开 Windows 文件对话框，用户浏览查找 .wav 文件；你可以提供初始目录作为参数，或者留空以使用当前目录。我们不会在合成器中使用此函数，但你可能会想出有趣的用法。

使用此对象可以更简单。只需构造它并将文件路径作为参数传递，然后检查 m_bWaveLoaded 以确定是成功还是失败。

遍历音频缓冲区需要你检查...

