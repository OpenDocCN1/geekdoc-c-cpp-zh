

# ** 代码列表 10.2: 加载样本 >>

```cpp
bool CDIGisynth::loadSamples()           //RAFX
bool Processor::loadSamples()            //VST3
bool ASynth::loadSamples()               //AU
(
    // -- RackAFX
    char* pPath0 = addStrings(getMyDLLDirectory(),"\\MultiSamples\\n\\Heaver");
    char* pPath1 = addStrings(getMyDLLDirectory(),"\\MultiSamples\\n\\OldFlatty");

    // -- VST3
    char* pDLLPath = getMyDLLDirectory(strstr("Digisynth.vst3"));

    char* pPath0 = addStrings(pPath0,"\\MultiSamples\\Heaver");
    char* pPath1 = addStrings(pPath1,"\\MultiSamples\\OldFlatty");

    // -- AU
    char* componentFolder = getMyComponentDirectory(
        CFSTR("developer.audiounit.yourname.digisynth"));

    char* pPath0 = addStrings(componentFolder,"\\MultiSamples\\Heaver");
    char* pPath1 = addStrings(componentFolder,"\\MultiSamples\\OldFlatty");
)

// // 为了加速样本加载。在此处初始化第一个样本
// -- 初始化为 false, false - 不是单样本，不是无音调样本
if(Im_pVoiceArray[0]->InitWithFolderPath(0, pPath0, false, false)) {
    return false;
}
if(Im_pVoiceArray[0]->InitWithFolderPath(1, pPath1, false, false)) {
    return false;
}

// 然后使用另一个函数拷贝样本指针
// 这样它们共享相同的数据缓冲区指针
for(int i=1; i<MAX_VOICES; i++) {
    // -- 初始化为 false, false = 不是单样本，
    // 不是无音调样本
    m_pVoiceArray[i]->initA110ScWithDigiSynthVoice(m_pVoiceArray[0], false, false);
}

// // 始终删除 addStrings() 返回的内存
delete [] pPath0;
delete [] pPath1;

// --- 仅限 VST3
delete [] pDLLPath;

// --- 仅限 AU
delete [] componentFolder;

return true;

<< END ** 代码列表 10.2: 加载样本 ** END >>

class CDigiSynth : public CPlugin
{
public:
    <SNIP SNIP SNIP>

    // 在此处添加你的代码：--------------------------------------
    << 插入 ** 代码列表 10.1: 声明 ** 在 >>

    etc...
bool _stdcall CDigiSynth::initialize()
{
    // --- 加载样本
    return loadSamples();
}
```

```cpp
void CDigiSynth::update() // RAFX
{
    // --- 更新全局参数
    // --- 振荡器：
    double d0scAmplitude = m_d0sc1Amplitude_dB == -96.0 ? 0.0 :
        pow(10.0, m_d0sc1Amplitude_dB/20.0);
    m_GlobalSynthParams.osc1Params.dAmplitude = d0scAmplitude;

    d0scAmplitude = m_d0sc2Amplitude_dB == -96.0 ? 0.0 :
        pow(10.0, m_d0sc2Amplitude_dB/20.0);
    m_GlobalSynthParams.osc2Params.dAmplitude = d0scAmplitude;

    // --- 循环模式
    m_GlobalSynthParams.osc1Params.uLoopMode = m_uLoopMode;
    m_GlobalSynthParams.osc2Params.uLoopMode = m_uLoopMode;

    // --- 滤波器：
    m_GlobalSynthParams.filter1Params.dFcControl = m_dfcControl;
    m_GlobalSynthParams.filter1Params.dQControl = m_dQControl;
    m_GlobalSynthParams.filter2Params.dFcControl = m_dfcControl;
    m_GlobalSynthParams.filter2Params.dQControl = m_dQControl;
}
```

```cpp
class Processor : public AudioEffect
{
    public:
        <SNIP SNIP SNIP>

        // 在此处添加你的代码：--
        << 插入 ** 代码列表 10.1: 声明 ** 在 >>

        etc...

        Processor::Processor()
        (
            // --- 定义我们的控制器 FUID
            setControllerClass(Controller::cid);

            // --- 初始化
            m_d0sc1Amplitude_dB = DEFAULT_OUTPUT_AMPLITUDE_DB;
            m_d0sc2Amplitude_dB = DEFAULT_OUTPUT_AMPLITUDE_DB;
            m_dEG10scIntensity = DEFAULT_BIPOLAR;

        etc... 其余部分与 MiniSynth 相同
}
```

```cpp
result PLUGIN_API Processor::setActive(TBool state)
{
    if(state)
    {
        <SNIP SNIP SNIP>

        // --- 保持分开是因为它们在 RAFX/AU 中是分开的
        for(int i=0; i<kMAX_VOICES; i++)
        {
            CDigiSynthVoice* pVoice = m_pVoiceArray[i];
            pVoice->setSampleRate((double)processup.samplerRate);
            pVoice->prepareForPlay();
        }

        // --- 现在加载样本
        loadSamples();

        // --- 批量更新
        update();
    }
    etc...
}
```

```cpp
void Processor::update()
{
    // --- 更新全局参数
    // --- 振荡器：
    double d0scAmplitude = m_d0sc1Amplitude_dB == -96.0 ? 0.0 :
        pow(10.0, m_d0sc1Amplitude_dB/20.0);
    m_GlobalSynthParams.osc1Params.dAmplitude = d0scAmplitude;

    d0scAmplitude = m_d0sc2Amplitude_dB == -96.0 ? 0.0 :
        pow(10.0, m_d0sc2Amplitude_dB/20.0);
    m_GlobalSynthParams.osc2Params.dAmplitude = d0scAmplitude;

    // --- 循环模式
    m_GlobalSynthParams.osc1Params.uLoopMode = m_uLoopMode;
    m_GlobalSynthParams.osc2Params.uLoopMode = m_uLoopMode;

    // --- 滤波器：
    m_GlobalSynthParams.filter1Params.dFcControl = m_dfcControl;
    m_GlobalSynthParams.filter1Params.dQControl = m_dQControl;
    m_GlobalSynthParams.filter2Params.dFcControl = m_dfcControl;
    m_GlobalSynthParams.filter2Params.dQControl = m_dQControl;
}
```

```cpp
bool Processor::doControlUpdate(ProcessData& data)
{
  <SNIP SNIP SNIP>

  switch (pid)
  {
    // cookValue(min, max, currentValue) - 将原始数据转换为有意义的信息
    case OSC1_AMPLITUDE_DB:
    {
      m_d0sc1Amplitude_dB = cookValue(MIN_OUTPUT_AMPLITUDE_DB,
                              MAX_OUTPUT_AMPLITUDE_DB);
      break;
    }

    case OSC2_AMPLITUDE_DB:
    {
      m_d0sc2Amplitude_dB = cookValue(MIN_OUTPUT_AMPLITUDE_DB,
                              MAX_OUTPUT_AMPLITUDE_DB);
      break;
    }

    case LOOP_MODE:
    {
      m_uLoopMode = (UINT)cookValue(MIN_LOOP_MODE,
                              MAX_LOOP_MODE);
      break;
    }
  }
}
```

```cpp
class AUSynth : public AUInstrumentBase
{
public:
    <SNIP SNIP SNIP>

    // 在此处添加你的代码：----------------------
    << 插入 ** 代码列表 10.1: 声明 ** >>

    etc...
ASynth::AUSynth(AudioUnit inComponentInstance)
    : AUInstrumentBase(inComponentInstance, 0, 1)
{
    // --- 创建输入、输出端口和分组
    CreateElements();

    // --- 设置默认工厂预设（示例）
    factoryPreset[OSC1_AMPLITUDE_DB] = 0.0;
    factoryPreset[OSC2_AMPLITUDE_DB] = 0.0;

    <SNIP SNIP SNIP>

    // --- 定义参数数量（控制项）
    Globals()->UseIndexedParameters(NUMBER_OF_SYNTH_PARAMETERS);

    // --- 在此处初始化控制项！
    // --- 这些定义在 SynthParamLimits.h 中
    Globals()->SetParameter(OSC1_AMPLITUDE_DB, DEFAULT_OUTPUT_AMPLITUDE_DB);
    Globals()->SetParameter(OSC2_AMPLITUDE_DB, DEFAULT_OUTPUT_AMPLITUDE_DB);
    Globals()->SetParameter(LOOP_MODE, DEFAULT_LOOP_MODE);

    etc...
}
```

```cpp
ComponentResult USynth::Initialize()
{
    // --- 初始化基类
    AUInstrumentBase::Initialize();

    // 清空
    m_dLastNoteFrequency = -1.0;

    // --- 注意：设置采样率并调用 prepareForPlay 非常重要
    for(int i=0; i<MAX_VOICES; i++) {
        CDigiSynthVoice* pVoice = m_pVoiceArray[i];
        pVoice->setSampleRate(GetOutput(0)->GetStreamFormat().mSampleRate);
        pVoice->prepareForPlay();
    }

    // --- 现在加载样本
    loadSamples();

    // --- 更新合成器
    update();

    return noErr;
}
```

```cpp
void AUSynth::update()
{
    // -- 更新全局参数
    // //
    // -- 振荡器：
    // //
    // -- 振荡器：
    double d0scAmplitude = Globals()->GetParameter(OSC1_AMPLITUDE_DB) ==
    -96.0 ? 0.0 : pow(10.0, Globals()->GetParameter(OSC1_AMPLITUDE_DB)/20.0);
    m_GlobalSynthParams.osc1Params.dAmplitude = d0scAmplitude;
    d0scAmplitude = Globals()->GetParameter(OSC2_AMPLITUDE_DB) ==
    -96.0 ? 0.0 : pow(10.0, Globals()->GetParameter(OSC2_AMPLITUDE_DB)/20.0);
    m_GlobalSynthParams.osc2Params.dAmplitude = d0scAmplitude;
    // -- 循环模式
    m_GlobalSynthParams.osc1Params.uLoopMode = Globals()->GetParameter(LOOP_MODE);
    m_GlobalSynthParams.osc2Params.uLoopMode = Globals()->GetParameter(LOOP_MODE);
    // ...
    // -- 滤波器：
    // // ...
    m_GlobalSynthParams.filter1Params.dFcControl = Globals()->GetParameter(FILTER_FC);
    m_GlobalSynthParams.filter1Params.dQControl = Globals()->GetParameter(FILTER_Q);
    m_GlobalSynthParams.filter2Params.dFcControl = Globals()->GetParameter(FILTER_FC);
    m_GlobalSynthParams.filter2Params.dQControl = Globals()->GetParameter(FILTER_Q);
    // ...
    // ...
    etc...
}
```

