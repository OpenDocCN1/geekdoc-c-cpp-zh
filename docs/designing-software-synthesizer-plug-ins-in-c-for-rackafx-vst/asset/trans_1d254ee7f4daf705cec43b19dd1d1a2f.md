
此方法在不同的合成器上略有不同。宿主程序调用此方法来开启和关闭合成器。Steinberg 建议在激活时进行动态内存分配，在停用时销毁或释放资源。书中的每个合成器都会在此创建并销毁它的音器数组。基于采样的合成器项目将在此初始化动态创建采样数组。当宿主程序调用此方法时，项目的采样率已经设置（或更改）。我们所有的合成器在正常运行都需要采样率，因此我们在这里初始化它。细节将在后续章节中介绍。`Processor` 对象继承自基类 `AudioEffect`，该类声明了一个名为 `processSetup` 的成员变量：

`ProcessSetup` 是一个遵循以下定义的结构：

protected:

我们将使用 `sampleRate` 变量（类型为 `double`）在音器对象添加到栈中后为它们设置采样率：

`ProcessSetup processSetup;`

```cpp
int32 processMode;                //< ProcessModes
int32 symbolicSampleSize;        //< SymbolicSampleSizes
int32 maxSamplesPerBlock;       //< 每个音频块的最大采样数
SampleRate sampleRate;            //< 采样率
```

示例中，我们展示了 `MiniSynth` 的方法。如果 `state` 参数为 `true`，我们向数组中加载我们的音器对象，为音器对象设置采样率，调用 `update()` 方法初始化合成器参数并重置上一个音符频率变量。然后，我们创建日志参数对象。`prepareForPlay()` 方法将在第 8 章中讨论。在下面的代码中，功能被分为两个 `for()` 循环，它们可以很容易地合并为一个。保留两个循环的原因是为了与其他 API 进行比较，在那些 API 中这两个操作是分开的，不在同一个函数中。

如果 `setActive()` 的参数为 `false`，我们将卸载音器栈并删除指针。`MAX_VOICES` 定义了该合成器的最大复声数。最后，调用基类执行其设置工作。

```cpp
result PLUGIN_API Processor::setActive(TBool state)
{
  if(state)
  {
    // 加载音器
    for(int i=0; i<MAX_VOICES; i++)
    {
      CMiniSynthVoice* pVoice = new CMiniSynthVoice;
      if(!pVoice)
        return kInvalidArgument;

      m_pVoiceArray[i] = pVoice;
    }
    for(int i=0; i<MAX_VOICES; i++)
    {
      m_pVoiceArray[i]->setSampleRate((double)processSetup.sampleRate);
      pVoice->prepareForPlay();
    }

    // 批量更新
    update();

    // 清空
    m_dLastNoteFrequency = -1.0;

    // 辅助函数
  }
  else
  {
    // --- 删除音器
    for(int i=0; i<MAX_VOICES; i++)
    {
      delete m_pVoiceArray[i];
    }
    if(m_pFilterLogParam)
      delete m_pFilterLogParam;
  }
  return kSuccess;
}
```

# 2.28 VST3 序列化

序列化通过 `getState()` 和 `setState()` 方法处理。

# getState()

此方法在不同的合成器上略有不同。用户保存项目或预设时，宿主会调用此方法。宿主传递一个文件流指针，你可以用它写入合成器参数变量。`Controller` 的 `createComponent()`（通过读取文件设置 GUI）遵循我们在此方法中设置的顺序，必须非常仔细确保操作顺序完全一致。这里是 `MiniSynth` 方法的部分代码。与之前会话中的 `Controller` 示例一样，我们创建了一个 `IBStreamer` 接口并使用其方法写入我们的变量：

此方法在不同的合成器上略有不同。宿主程序调用此方法从预设文件设置合成器。这与你在 `Controller` 的 `setComponent()` 方法中看到的非常相似。区别在于，在该函数中，你直接从文件加载变量，而不需要将其转换为归一化值。读取操作的顺序必须与 `getState()` 方法中的完全匹配。这里是 `MiniSynth` 方法的部分，你可以看到在 `Controller` 示例中读取 `UINT` 和数据时所需的 `udata` 和 `data` 哑变量的用法。你还可以看到在产品发布和修订后添加额外参数时的版本控制。

```cpp
result PLUGIN_API Processor::getState(IBStream* fileStream)
{
  // 获取流接口
  IBStreamer s(fileStream, kLittleEndian);

  // --- MiniSynthVersion - 将此置于顶部以便在读取操作期间使用版本
  if(is.writeInt64u(MiniSynthVersion)) return kResultFalse;
  // --- 这些顺序与枚举的顺序一致
  if(is.writeDouble(m_dNoiseOsc_db)) return kResultFalse;
  if(is.writeDouble(m_dPulseWidth_Pct)) return kResultFalse;
  if(is.writeDouble(m_dEG10scIntensity)) return kResultFalse;
  // 等...
  return kResultTrue;
}
```

# update()

```cpp
tresult PLUGIN_API Processor::setState(IBStream* fileStream)
{
    IBStreamer s(fileStream, kLittleEndian);
    // 数据块
    uint64 version = 0;
    // 转换为 UINT
    uint32 udata = 0;
    int32 data = 0;

    // 读取版本
    if(is.read64u(version)) return kResultFalse;
    // 读取相同的顺序
    if(is.readDouble(m_dNoiseOsc_db)) return kResultFalse;
    if(is.readDouble(m_dPulseWidth_Pct)) return kResultFalse;
    if(is.readDouble(m_dEG10scIntensity)) return kResultFalse;
    // 等...

    if(version >= 1)
    {
        // // 在此处添加内容
    }
    return kSuccess;
}
```

（注：后续文本内容为上述内容的重复，已按要求要求未进行重复翻译。）
