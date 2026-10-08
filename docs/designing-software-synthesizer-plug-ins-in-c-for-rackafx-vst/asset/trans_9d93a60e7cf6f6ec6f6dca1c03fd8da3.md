

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

- 使用 note off 代码来完成该函数

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

- 遍历 voice并在调制矩阵中设置合适的源值

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
- 遍历 voice并在调制矩阵中设置合适的源值：

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

```cpp
// --- event occurred
noteEvent = true;

// fix noteID per SDK
if(vstEvent.noteOff == -1)
    vstEvent.noteOff = uMIDiNote;
```

<< INSERT ** Code Listing 9.8: Note Off >>
break;
```

etc..

- Pan
- Expression
- All Notes Off
- Sustain Pedal

注意：此函数在合成器的其余部分将是相同的，因此不再显示

构建并测试 MiniSynth；尝试不同的 voice 模式并运行调制程序。

# 911 Challenges

# Bronze

修改 EG 控制并将共享的 decay/release 控制拆分为两个控制，这样你就有完整的 attack、decay、sustain 和 release 控制。

图914：MiniSynth（等等，mkII）具有第二个 EG 和开关。

图915：MiniSynth 增加了另一个 LFO。

# Silver

将滤波器升级为多滤波器对象，允许用户选择第7章中的任何滤波器。这将通过订阅 CFilter 并使用指针来选择和操作各种滤波器。如果你实现了 Moog 半阶滤波器，合成器中将会有16个不同的滤波器。

# Gold

实现图914所示的 MiniSynth。此版本增加了连接到滤波器的第二个 EG，使其

```cpp
bool Processor::doControlUpdate(ProcessData& data)
{
bool paramChange = false;

<SNIP SNIP>

switch(pid) // same as RAFX uControlID
(
    <SNIP SNIP SNIP Indents Removed>

    // --- MIDI messages
    case MIDI_PITCHEND: // want -1 to +1
    (
        m_dMIDIPitchBend = unipolarToBipolar(value);
        for(int i=0; i<MAX_VOICES; i++)
        {
            // --- sendArray to matrix
            m_pVoiceArray[i]->m_ModulationMatrix;
            m_dSources[SOURCE_PITCHEND] = m_dMIDIPitchBend;
        }
        break;
    )
case MIDI_MODWHEEL: // want 0 to 127
    (
    m_uMIDIDModWheel = unipolarToMIDI(value);
    for(int i=0; i<MAX_VOICES; i++)
    {
        m_pVoiceArray[i]->m_ModulationMatrix;
        m_dSources[SOURCE_MODWHEEL] = m_uMIDIDModWheel;
    }
    break;
    )
case MIDI_VOLUME_CC7: // want 0 to 127
    (
    m_uMIDIVolumeCC7 = unipolarToMIDI(value);
    for(int i=0; i<MAX_VOICES; i++)
```

```cpp
{
  m_voiceArray[i]->m_ModulationMatrix;
  m_dSources[SOURCE_MIDI_VOLUME_CC07] = m_uMIDIVolumeCC7;
}
break;
case MIDI_PAN_CC10: // want 0 to 127
    {
  m_uMIDIPanCC10 = unipolarToMIDI(value);
  for (int i=0; i<MAX_VOICES; i++) {
    m_voiceArray[i]->m_ModulationMatrix;
    m_dSources[SOURCE_MIDI_PAN_CC10] = m_uMIDIPanCC10;
  }
}
break;
case MIDI_EXPRESSION_CC11: // want 0 to 127
    {
  m_uMIDIExpressionCC11 = unipolarToMIDI(value);
  for (int i=0; i<MAX_VOICES; i++) {
    m_voiceArray[i]->m_ModulationMatrix;
    m_dSources[SOURCE_MIDI_EXPRESSION_CC11] = m_uMIDIExpressionCC11;
  }
}
break;
case MIDI_SUSTAIN_PEDAL: // want 0 to 1
    {
  UINT uMIDI = value > 0.5 ? 127 : 0;
  for (int i=0; i<MAX_VOICES; i++) {
    m_voiceArray[i]->m_ModulationMatrix;
    m_dSources[SOURCE_SUSTAIN_PEDAL] = uMIDI;
  }
}
break;
    }
}
```

