

Redmon, Nigel.. 包络发生器.. 访问于2014年6月, http://www.earlevel.com/main/2013/06/02/envelope-generators-adrs-part-2

```cpp
m_LF01.setSampleRate((double)processSetup.sampleRate);
```

Sound on Sound 杂志。
"合成器秘密。"
访问
2014年6月，

```cpp
m_EG1.setSampleRate((double)processSetup.sampleRate);
m_EG1.m_bOutputEG = true;
```

```cpp
update();
}
netc;
```

```cpp
void Processor::update(){
{
<SNIP SNIP SNIP>

// --- EG 控制
m_EG1.setAttackTime_mSec(m_dAttackTime_mSec);
m_EG1.setDecayTime_mSec(m_dDecayTime_mSec);
m_EG1.setSustainlevel(m_dSustainLevel);
m_EG1.setReleaseTime_mSec(m_dReleaseTime_mSec);
m_EG1.m_bResetToZero = (bool)m_uResetToZero;
m_EG1.m_bLegatoMode = (bool)m_uLegatoMode;

// --- DCA 控制
m_DCA.setPanControl(m_dPanControl);
m_DCA.setAmplitude_dB(m_dVolume_dB);
m_DCA.update();
}
```

http://www.soundsounds.com/sos/allsynthsecrets.htm

synthtech.com..CEM3310 电压包络发生器数据表.. 访问于2014年6月，
http://www.synthtech.com/cem/c3310pdf.pdf

Yamaha, Inc. 1983. DX7 用户手册。东京：Yamaha, Inc.

Yamaha, Inc. 1998. EX5/EX7 用户手册。东京：Yamaha, Inc.

```cpp
bool _stdcall Processor::process(args...)
{
    <SNIP SNIP SNIP and Indents Removed>
    for(int32 j=0; j<samplesToProcess; j++)
    {
        // --- 清空累加器
        dOutL = 0.0;
        dOutR = 0.0;
        if(m_Osc1.m_bNoteOn)
        {
            << 插入 代码列表 5.1：音频渲染 ** 此处 >>
        }

        // 写入缓冲区
        buffers[0][j] = dOutL; // 左
        buffers[1][j] = dOutR; // 右
    }

    etc...
}
```

```cpp
bool Processor::doProcessEvent(Event& vstEvent)
{
    bool noteEvent = false;

    // --- 在此处处理 Note On 或 Note Off 消息
    switch(vstEvent.type)
    {
        // --- Note ON
        case Event::kNoteEvent:
        {
            <SNIP SNIP SNIP>
            m_LF01.startOscillator();
            m_EG1.startEG();
            break;
        }

        // --- Note OFF
        case Event::kNoteOffEvent:
        {
            <SNIP SNIP SNIP>
            // --- 如果是正确的音符，则关闭
            // (最后一个播放的音符)
            if(uMIDINote == m_Oscl.m_uMIDINoteNumber)
                m_EG1.noteOff();
        }

        break;
    }
    etc...
}
```

```cpp
// --- 合成器对象
#include "QBLimitedOscillator.h"
#include "WTOillator.h"
#include "LFO.h"
#include "EnvelopeGenerator.h"
#include "DCA.h"
```

```cpp
// --- AU 合成器
class AUSynth : public AUInstrumentBase
{
public:
```

```cpp
<SNIP SNIP SNIP>

// 在此处添加你的代码：--------------------
QBLimitedOscillator m_osc1;
QBLimitedOscillator m_osc2;
CLFO m_LFO1;

// --- 一个 EG
CEnvelopeGenerator m_EG1;

// --- 一个 DCA
CDCA m_DCA;

void update();

etc...
```

```cpp
ComponentResult AUSynth::Initialize(
{
    // --- 初始化基类
    AUInstrumentBase::Initialize();

    // --- 初始化
    m_Osc1.setSampleRate(GetOutput(0)->GetStreamFormat().msSampleRate);
    m_Osc2.setSampleRate(GetOutput(0)->GetStreamFormat().msSampleRate);
    m_Osc2.m_nCents = 2.5;

    m_LF01.setSampleRate(GetOutput(0)->GetStreamFormat().msSampleRate);
    m_EG1.setSampleRate(GetOutput(0)->GetStreamFormat().msSampleRate);

    // --- 大更新
    update();

    return noErr;
}
```

```cpp
void AUSynth::update()
{
    <SNIP SNIP SNIP>

    // --- 更新 EG
m_EG1.setAttackTime_msec(Globals())->GetParameter(EG1_ATTACK_MSEC);
m_EG1.setDecayTime_msec(Globals())->GetParameter(EG1_DECAY_MSEC);
m_EG1.setSustainLevel(Globals())->GetParameter(EG1_SUSTAIN_LEVEL);
m_EG1.setReleaseTime_msec(Globals())->GetParameter(EG1_RELEASE_MSEC);
m_EG1.m_bResetToZero = Globals()->GetParameter(RESET_TO_ZERO);
m_EG1.m_bLegatoMode = Globals()->GetParameter(LEGATO_MODE);

    // --- 更新 DCA
m_DCA.setPanControl(Globals())->GetParameter(OUTPUT_PAN);
m_DCA.setAmplitude_dB(Globals())->GetParameter(OUTPUT_AMPLITUDE_DB);
m_DCA.update();
}
```

```cpp
OSStatus ASynth::Render(args...)
{
    // --- 广播 MIDI 事件
    PerformEvents(inTimestamp);

    <SNIP SNIP SNIP>
    // --- 帧处理循环
    for(Uint32 frame=0; frame<inFrames; ++frame)
    {
        // --- 清空累加器
        dOutL = 0.0;
        dOutR = 0.0;
        if(m_Osc1.m_bNoteOn)
        {
            << 插入 代码列表 5.1：音频渲染 ** 此处 >>
        }
        // 写入缓冲区
        buffers[0][frame] = dOutL; // 左
        buffers[1][frame] = dOutR; // 右
    }
    etc...
}
```

