
注意：函数的这部分在其他合成器项目中是相同的，因此将不再显示。

```cpp
// 循环并累加声音
for(int i=0; i<MAX_VOICES; i++)
{
    // --- 渲染合成器
    m_pVoiceArray[i]->doVoice(dLeft, dRight);

    // --- 累加并缩放
    dLeftAccum += fMix*dLeft;
    dRightAccum += fMix*dRight;
}
```

<< END ** 代码列表 9.5: 渲染 ** END >>

# 9.10 MiniSynth: AU

创建一个名为 `MiniSynth` 的新项目并使用表 9.5 设置 GUI。

# AUSynth.h

为 `voice` 数组、辅助函数以及上一次音和 MIDI 接收变量添加声明：

# << ** 代码列表 9.6: Note On ** >>

```cpp
bool bStealNote = true;
for(int i=0; i<MAX_VOICES; i++)
{
    // 循环寻找空闲 voice
    CMiniSynthVoice* pVoice = m_pVoiceArray[i];

    // 如果有空闲 voice，则开启
    if(!pVoice->m_bNoteOn)
    {
        // 先执行这个
        incrementVoiceTimestamps();

        // 然后触发 note on
        pVoice->noteOn(uMIDINote, uVelocity, midiFreqTable[uMIDINote], m_dLastNoteFrequency);
    }

    // 记录 MIDI 事件

    // 保存
    m_dLastNoteFrequency = midiFreqTable[uMIDINote];
}

bStealNote = false;
break;
}
// --- 需要抢占音
if(bStealNote)
{
    // --- 抢占最旧的音
    CMiniSynthVoice* pVoice = getOldestVoice();
    if(pVoice)
    {
        // --- 先执行这个
        incrementVoiceTimestamps();
        // --- 然后触发 note on
        pVoice->noteOn(uMIDINote, uVelocity, midiFreqTable[uMIDINote], m_dLastNoteFrequency);
        // 记录 MIDI 事件
    }
    // --- 保存
    m_dLastNoteFrequency = midiFreqTable[uMIDINote];
}
```

<< END ** 代码列表 9.6: Note On ** END >>

# AUSynth.cpp

## 构造函数

- 初始化为 GUI 控制声明的所有变量；默认值位于项目的 `SynthParamLimits.h` 中
- 创建并初始化 `voices`
- 同步所有调制矩阵核心

## 析构函数

- 销毁全局矩阵
- 销毁 `voices`

## Reset()

## Initialize()

- 这些函数的代码完全相同；先调用基类，然后：
- 设置采样率并在 `voices` 上调用 `prepareFor()`
- 批量更新
- 初始化上一次音频率

## update()

插入此函数，该函数已完整列出。

# << ** 代码列表 9.7: All Notes Off ** >>

```cpp
// 强制全部关闭
for(int i=0; i<MAX_VOICES; i++)
{
    m_pVoiceArray[i]->m_uoteNumber);
}
```

<< END ** 代码列表 9.7: All Notes Off ** END >>

# << ** 代码列表 9.8: Note Off ** >>

// 寻找并关闭

// 可能有多个持续音；这确保

// 从栈顶开始

```cpp
for(int i=0; i<MAX_VOICES; i++)
{
    CMiniSynth* pVoice = getOldestVoiceWithNote(uMIDINote);

    if(pVoice)
    {
        pVoice->noteOff(uMIDINote);
        // 记录 MIDI
        break;
    }
}
```

<< END ** 代码列表 9.8: Note Off ** END >>

| DCA.h | MoogLadderFilter.h |
| DCA.cpp | MoogLadderFilter.cpp |
| EnvelopeGenerator.h | Oscillator.h |
| EnvelopeGenerator.cpp | Oscillator.h |
| Filter.h | QBlitedOsc.h |
| Filter.cpp | QBlitedOsc.cpp |
| LFO.h | synth.h |
| LFO.cpp | VAoneFilter.h |
| MiniSynthVoice.h | VAoneFilter.cpp |
| MiniSynthVoice.cpp | Voice.h |
| ModulationMatrix.h | Voice.cpp |

## Render()

```cpp
class CMiniSynth : CPlugin
{
public:
  * 插入渲染代码来渲染循环
  * 输出累加值
```

```cpp
incrementVoiceTimestamps();
// 在此处添加你的代码：------------------------------------
```

<< INSERT ** 代码列表 9.1: Declarations ** >>

```cpp
CMiniSynth::CMiniSynth()
{
  m_bOutputOnlyPlugin = true;
  // 设置所有消息标记
  m_bWantAllIMessages = true;
}
```

<< INSERT ** 代码列表 9.2: Init Voices ** >>

```cpp
CMiniSynth::~CMiniSynth(void)
{
}
```

<< INSERT ** 代码列表 9.3: Destruction ** >>

```cpp
bool __stdcall CMiniSynth::prepareForPlay()
{
  return true;
}
```

<< INSERT ** 代码列表 9.4: One Time Init ** >>

```cpp
return false;
switch(cStatus)
{
    <SNIP SNIP SNIP>
    case CONTROL_CHANGE:
    {
        switch(cData)
        {
            case VOLUME_CC07:
            {
                // --- send to matrix
                for(int i=0; i<MAX_VOICES; i++)
                {
                    m_VoiceArray[i]->mModulationMatrix.m_dSources[SOURCE_MIDI_VOLUME_CC07] = (UINT)cdata2;
                }
            }
            break;
    }}
    case PAN_CC10:
    {
        // --- send to matrix
        for(int i=0; i<MAX_VOICES; i++)
        {
            m_VoiceArray[i]->mModulationMatrix.m_dSources[SOURCE_MIDI_PAN_CC10] = (UINT)cdata2;
        }
    }
    break; SOURCE_MIDI_EXPRESSION_CC11
    case EXPRESSION_CC11:
    {
        // --- send to matrix
        for(int i=0; i<MAX_VOICES; i++)
        {
        }
    }
}
```

- 使用 `note off` 代码来完成该函数

```cpp
m_pVoiceArray[i]
  ->mModulationMatrix.m_dS [SOURCE_MIDI_EXPRESSION_CC11] = (UINT)cData2;
  break;
}
case SUSTAIN_PEDAL:
(
  for(int i=0; i<MAX_VOICES; i++)
  {
    m_pVoiceArray[i]
      ->mModulationMatrix.m_dS
      [SOURCE_SUSTAIN_PEDAL] =
      (UINT)cData2;
  }
  break;
}
```

等等 . . .

```cpp
class Processor : public AudioEffect
{
public:
  <SNIP SNIP SNIP>
  // Add your code here:                                               //
  << INSERT ** Code Listing 9.1: Declarations ** HERE >>
  etc. . .
  - 注意：此函数在其余的同步项目中将是相同的，区别在于音器数组中指针的类型，因此它不再再次显示
```

```cpp
Processor::Processor()
{
  // --- we are a Processor
  setController(Controller::cid);
```

```cpp
// --- our inits
m_dNoiseOsc_db = DEFAULT_NOISE_OSC_AMP_DB;
m_dPulseWidth_Pct = DEFAULT_PULSE_WIDTH_PCT;
m_dDHSRatio = DEFAULT_HARD_SYNC_RATIO;
m_dDEGIScIntensity = DEFAULT_BIPOLAR;
```

```cpp
// VST3 specific
m_dMidiIDIPitchBend = DEFAULT_MIDI_PITCHBEND; // -1 to +1
m_uUMidiModWheel = DEFAULT_MIDI_MODWHEEL;
m_uUMidiVolumeCC7 = DEFAULT_MIDI_VOLUME; // note defaults to 127
m_uUMidiPanCC10 = DEFAULT_MIDI_PAN; // 64 = center pan
m_uUMidiExpressionCC11 = DEFAULT_MIDI_EXPRESSION;
```

```cpp
// Finish initializations here
m_dLastNoteFrequency = -1.0;
```

```cpp
// receive on all channels
m_uUMidiRxChannel = MIDI_CH_ALL;
```

```cpp
// this is created/destroyed in SetActive()
m_pFilterLogParam = NULL;
```

# HandlePitchWheel()

- 遍历 `voice` 并在调制矩阵中设置合适的源值

```cpp
result PLUGIN_API Processor::setActive(TBool state)
{
if(state)
{
    << INSERT ** Code Listing 9.2: Init Voices ** HERE >>
    << INSERT ** Code Listing 9.4: One Time Init ** HERE >>
    // mass update
    update();
    // helper
m_pFilterLogParam = newLogScaleParameter<ParamValue>(USTRING("Filter fc"),FILTER_FC,
filterLogScale2, (USTRING("Hz")));
}
else
{
    << INSERT ** Code Listing 9.3: Destruction ** HERE >>
    // base class method is last
    return AudioEffect::setActive(state);
}
```

- 注意：这些函数在合成器的其余部分将是相同的，因此不再再次显示

```cpp
result PLUGIN_API Processor::process(ProcessData& data)
{
<SNIP SNIP SNIP>
float fMix = 0.25; // 12dB headroom
double dLeft = 0.0;
double dRight = 0.0;
double dLeftAccum = 0.0;
double dRightAccum = 0.0;

for(int j=0; j<samplesToProcess; j++) {
    // --- clear accumulators
    dLeftAccum = 0.0;
    dRightAccum = 0.0;

    for (int i=0; i<MAX_VOICES; i++) {
        // --- render left and right
        m_pVoiceArray[i]->doVoice(dLeft, dRight);
        // --- accumulate
        dLeftAccum += fMix*dLeft;
        dRightAccum += fMix*dRight;
    }
    // write out to buffer
    buffers[0][j] = dLeftAccum; // left
    buffers[1][j] = dRightAccum; // right
}
```

etc.. .

# HandleControl()

- 解码消息
- 遍历 `voice` 并在调制矩阵中设置合适的源值：

```cpp
bool Processor ::doProcessEvent(Event& vstEvent)
{
    bool noteEvent = false;
    switch(vstEvent.type)
    {
        // --- NOTE ON
        case Event::*NoteEvent:
        {
            // --- get the channel/note/vel
            UINT uMIDiChannel = (UINT)vstEvent.channel;
            UINT uMIDiNote = (UINT)vstEvent.pitch;
            UINT uVelocity = (UINT)(127.0*vstEvent.velocity);
            // --- test channel/ignore
            if(m_uMIDiRxChannel != MIDI_CH_ALL && uMIDiChannel != m_uMIDxChannel)
                return false;
            // --- event occurred
            noteEvent = true;
            // --- fix noteID per SDK
            if(vstEvent.noteID == -1)
                vstEvent.noteID = uMIDiNote;
            << INSERT ** Code Listing 9.6: Note On >>
            break;
        }
        // --- NOTE OFF
        case Event::*NoteOff:
        {
            // --- get the channel/note/vel
            UINT uMIDiChannel = (UINT)vstEvent.channel;
            UINT uMIDiNote = (UINT)vstEvent.pitch;
            UINT uVelocity = (UINT)(127.0*vstEvent.velocity);
        }
    }
}
```

- Mod Wheel
- Volume

```cpp
// --- test channel/ignore
if(m_uMidiRxChannel != MIDI_CH_ALL && uMIDIChannel != m_uMIDxChannel)
    return false;
```
