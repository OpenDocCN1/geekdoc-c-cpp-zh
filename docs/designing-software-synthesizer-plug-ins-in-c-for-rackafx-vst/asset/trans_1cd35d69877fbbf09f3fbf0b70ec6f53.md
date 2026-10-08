

```cpp
CMiniSynthVoice* pVoice = m_pVoiceArray[i];
m_pVoice->setSampleRate((double)m_nSampleRate);
pVoice->prepareForPlay();
```

```cpp
// mass update
update();
```

```cpp
// clear
m_dLastNoteFrequency = -1.0;
```

<< END ** 代码列表 9.4: 一次初始化 ** END >>

# VSTSynthProcessor.cpp

# 构造函数

- 初始化所有为 GUI 控制声明的变量；默认值在项目的 SynthParamLimits.h 中

# setActive()

- 激活状态：
    - 创建并初始化音器（voices）
    - 同步所有调制矩阵（mod matrix）核心
    - 设置采样率并在音器上调用 preparePlay()
    - 批量更新

- 去激活状态：
    - 销毁全局调制矩阵
    - 销毁音器

注意：可以随意合并音器的 for() 循环（列表 9.2 和 9.4）；在这里将它们分开仅是为了与 RackAFX 和 AU 保持一致。

# update()

插入此函数，该函数在上方完整列出。

# process()

- 插入渲染代码以执行渲染循环
- 输出累积值。

# incrementVoiceTimestamps();

```cpp
void CMiniSynth::update() // RAFX
void Processor::update() // VST3
{
  // -- 更新全局参数
  //
  // -- 音器:
  m_GlobalSynthParams.voiceParams.uVoiceMode = m_uVoiceMode;
  m_GlobalSynthParams.voiceParams.dPortamentoTime_mSec = -
      m_dPortamentoTime_mSec;

  // -- 范围
  m_GlobalSynthParams.voiceParams.doscFoPitchModRange = -
      m_nPBendRange;

  // -- 强度
  m_GlobalSynthParams.voiceParams.dFilterKeyIntensity = -
      m_dFilterKeyIntensity;
  m_GlobalSynthParams.voiceParams.dLF01FilterIntensity = -
      m_dLF01FcIntensity;
  m_GlobalSynthParams.voiceParams.dLF01scModIntensity = -
      m_dLF01scPitchIntensity;
  m_GlobalSynthParams.voiceParams.dLF01DCAmpIntensity = -
      m_dLF01AmpIntensity;
  m_GlobalSynthParams.voiceParams.dLF01DCAPanModIntensity = -
      m_dLF01PanIntensity;

  m_GlobalSynthParams.voiceParams.dEG10scModIntensity = -
      m_dEG10scIntensity;
  m_GlobalSynthParams.voiceParams.dEG1FilterModIntensity = -
      m_dEG1FilterIntensity;
  m_GlobalSynthParams.voiceParams.dEG1DCAmpIntensity = -
      m_dEG1DCAIntensity;

  // -- 振荡器:
  double dNoiseAmplitude = m_dNoiseOsc_dB == -96.0 ? 0.0 :
      pow(10.0, m_dNoiseOsc_dB/20.0);
```

```cpp
// --- OSC3 是子振荡器
m_GlobalSynthParams.osc3Params.Amplitude = dSubAmplitude;

// --- OSC4 是噪声振荡器
m_GlobalSynthParams.osc4Params.dAmplitude = dNoiseAmplitude;

// --- 脉宽
m_GlobalSynthParams.osc1Params.dPulseWidthControl = m_dPulseWidth_Pct;
m_GlobalSynthParams.osc2Params.dPulseWidthControl = m_dPulseWidth_Pct;
m_GlobalSynthParams.osc3Params.dPulseWidthControl = m_dPulseWidth_Pct;

// --- 八度
m_GlobalSynthParams.osc1Params.noctave = m_noctave;
m_GlobalSynthParams.osc2Params.noctave = m_noctave;
m_GlobalSynthParams.osc3Params.noctave = m_noctave;

// --- MiniSynth 的调音
m_GlobalSynthParams.osc1Params.nCents = m_dDetune_cents;
m_GlobalSynthParams.osc2Params.nCents = m_dDetune_cents;

// --- 滤波器:
m_GlobalSynthParams.filter1Params.dFcControl = m_dFcControl;
m_GlobalSynthParams.filter1Params.dQControl = m_dQControl;

// --- LF01:
m_GlobalSynthParams.lf01Params.uWaveform = m_uLF01Waveform;
m_GlobalSynthParams.lf01Params.dAmplitude = m_dLF01Amplitude;
m_GlobalSynthParams.lf01Params.dOSfo = m_dLF01Rate;

// --- EG1:
m_GlobalSynthParams.eg1Params.dAttackTime_mSec = m_dAttackTime_mSec;
m_GlobalSynthParams.eg1Params.dDecayTime_mSec = m_dDecayTime_mSec;
m_GlobalSynthParams.eg1Params.dSustainLevel = m_dSustainLevel;
m_GlobalSynthParams.eg1Params.dReleaseTime_mSec = m_dReleaseTime_mSec;
m_GlobalSynthParams.eg1Params.bResetToZero = (bool)m_ResetToZero;

m_GlobalSynthParams.egParams.bLegato = (bool)m_uLegato;

// --- DCA:
m_GlobalSynthParams.caParams.dAmplitude_dB = m_dVolume_dB;

// --- 启用/禁用调制矩阵
if(m_uVelocityToAttack == 1)
  m_GlobalModMatrix.enableRow(SOURCE_VELOCITY, DEST_ALL_EG_ATTACK, true); // 启用
else
  m_GlobalModMatrix.enableRow(SOURCE_VELOCITY, DEST_ALL_EG_ATTACK, false);

if(m_uNumberToDecay == 1)
  m_GlobalModMatrix.enableRow(SOURCE_MIDI_NUM, DEST_ALL_EG_DECAY, true); // 启用
else
  m_GlobalModMatrix.enableRow(SOURCE_MIDI_NUM, DEST_ALL_EG_DECAY, false);

if(m_uFilterKey == 1)
  m_GlobalModMatrix.enableRow(SOURCE_MIDI_NUM, DEST_ALL_FILTER_KEYTRACK, true); // 启用
else
  m_GlobalModMatrix.enableRow(SOURCE_MIDI_NUM, DEST_ALL_FILTER_KEYTRACK, false);
```cpp
void ASynth::update() {
  // --- 音器:
  m_GlobalSynthParams.voiceParams.uVoiceMode = Globals()->GetParameter(VOICE_MODE);
  m_GlobalSynthParams.voiceParams.dPortamentoTime_mSec = Globals()->GetParameter(PORTAMENTO_TIME_MSEC);

  // --- 范围
  m_GlobalSynthParams.voiceParams.doscFoPitchModRange = Globals()->GetParameter(PITCH_END_RANGE);

  // --- 强度
  m_GlobalSynthParams.voiceParams.dFilterKeyIntensity = Globals()->GetParameter(FILTER_TRACK_INTENSITY);
  m_GlobalSynthParams.voiceParams.dLF01FilterIntensity = Globals()->GetParameter(LF01_TO_FILTER);
  m_GlobalSynthParams.voiceParams.dLF01ScModIntensity = Globals()->GetParameter(LF01_TO_OSC);
  m_GlobalSynthParams.voiceParams.dLF01CAmpIntensity = Globals()->GetParameter(LF01_TO_CA);
  m_GlobalSynthParams.voiceParams.dLF01DCANModIntensity = Globals()->GetParameter(LF01_TO_PAN);
  m_GlobalSynthParams.voiceParams.dEGI0OscIntensity = Globals()->GetParameter(EGI1_TO_OSC);
  m_GlobalSynthParams.voiceParams.dEGI1FilterIntensity = Globals()->GetParameter(EGI1_TO_FILTER);
  m_GlobalSynthParams.voiceParams.dEGI1CAmpIntensity = Globals()->GetParameter(EGI1_TO_CA);

  // --- 振荡器:
  double dNoiseAmplitude = Globals()->GetParameter(NOISE_OSC_AMP_DB) == -96.0 ? 0.0 : pow(10.0, Globals()->GetParameter(NOISE_OSC_AMP_DB) / 20.0);
  double dSubAmplitude = Globals()->GetParameter(SUB_OSC_AMP_DB) == -96.0 ? 0.0 : pow(10.0, Globals()->GetParameter(SUB_OSC_AMP_DB) / 20.0);

  // --- OSC3 是子振荡器
  m_GlobalSynthParams.osc3Params.Amplitude = dSubAmplitude;

  // --- OSC4 是噪声振荡器
  m_GlobalSynthParams.osc4Params.dAmplitude = dNoiseAmplitude;

  // --- 脉宽
  m_GlobalSynthParams.osc1Params.dPulseWidthControl = Globals()->GetParameter(PULSE_PCT);
  m_GlobalSynthParams.osc2Params.dPulseWidthControl = Globals()->GetParameter(PULSE_PCT);
  m_GlobalSynthParams.osc3Params.dPulseWidthControl = Globals()->GetParameter(PULSE_PCT);

  // --- 八度
  m_GlobalSynthParams.osc1Params.noctave = Globals()->GetParameter(OCTAVE);
  m_GlobalSynthParams.osc2Params.noctave = Globals()->GetParameter(OCTAVE);
  m_GlobalSynthParams.osc3Params.noctave = Globals()->GetParameter(OCTAVE) - 1;

  // --- MiniSynth 的调音
  m_GlobalSynthParams.osc1Params.nCents = Globals()->GetParameter(DETUNE_CENTS);
  m_GlobalSynthParams.osc2Params.nCents = Globals()->GetParameter(DETUNE_CENTS);

  // --- 滤波器:
  m_GlobalSynthParams.filter1Params.dFcControl = Globals()->GetParameter(FILTER_FC);
  m_GlobalSynthParams.filter1Params.dQControl = Globals()->GetParameter(FILTER_Q);

  // --- LF01:
  m_GlobalSynthParams.lf01Params.uWaveform = Globals()->GetParameter(LF01_WAVEFORM);
  m_GlobalSynthParams.lf01Params.dAmplitude = Globals()->GetParameter(LF01_AMPLITUDE);
  m_GlobalSynthParams.lf01Params.dOSfo = Globals()->GetParameter(LFO1_RATE);

  // --- EG1:
  m_GlobalSynthParams.eg1Params.dAttackTime_mSec = Globals()->GetParameter(EG1_ATTACK_MSE);
  m_GlobalSynthParams.eg1Params.dDecayTime_mSec = Globals()->GetParameter(EG1_DECAY_RELEASE_MSE);
  m_GlobalSynthParams.eg1Params.dSustainLevel = Globals()->GetParameter(EG1_SUSTAIN_LEVEL);
  m_GlobalSynthParams.eg1Params.dReleaseTime_mSec = Globals()->GetParameter(EG1_RELEASE_MSE);
  m_GlobalSynthParams.eg1Params.bResetToZero = (bool)Globals()->GetParameter(RESET_TO_ZERO);

  m_GlobalSynthParams.egParams.bLegato = (bool)Globals()->GetParameter(LEGATO_MODE);

  // --- DCA:
  m_GlobalSynthParams.caParams.dAmplitude_dB = Globals()->GetParameter(VOLUME_DB);

  // --- 启用/禁用调制矩阵
  if(m_uVelocityToAttack == 1)
    m_GlobalModMatrix.enableRow(SOURCE_VELOCITY, DEST_ALL_EG_ATTACK, true); // 启用
  else
    m_GlobalModMatrix.enableRow(SOURCE_VELOCITY, DEST_ALL_EG_ATTACK, false);

  if(m_uNumberToDecay == 1)
    m_GlobalModMatrix.enableRow(SOURCE_MIDI_NUM, DEST_ALL_EG_DECAY, true); // 启用
  else
    m_GlobalModMatrix.enableRow(SOURCE_MIDI_NUM, DEST_ALL_EG_DECAY, false);

  if(m_uFilterKey == 1)
    m_GlobalModMatrix.enableRow(SOURCE_MIDI_NUM, DEST_ALL_FILTER_KEYTRACK, true); // 启用
  else
    m_GlobalModMatrix.enableRow(SOURCE_MIDI_NUM, DEST_ALL_FILTER_KEYTRACK, false);
}
```

