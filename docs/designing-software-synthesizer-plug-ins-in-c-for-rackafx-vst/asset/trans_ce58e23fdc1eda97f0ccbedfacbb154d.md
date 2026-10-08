

![](img/b42d0dca53f4a889d8162d55f7c8c05d_602_0.png)

图 9.5：Sequential Circuits Prophet VS 语音架构——这是第 11 章 VectorSynth 的基础，将在该中讨论其独特的矢量混合包络生成器（Vector Mix Envelope Generator）。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_602_1.png)

图 9.6：来自 Triton 和 Karma 的 Korg H.I. 语音架构；在这里 Korg 将一个子音色称为“OSC”，它由振荡器、滤波器、LFO、EG 和 DCA 组成——两个 OSC 组成一个音色。

## CVoice 子组件

![](img/b42d0dca53f4a889d8162d55f7c8c05d_603_0.png)

图 9.7：CVoice 是合成器对象的集合，你通过连接它们来创建一个音色；补丁编程通过调制矩阵完成，对象使用全局参数来调整组件属性。

```cpp
class CVoice {
public:
    CVoice(void);
    virtual ~CVoice(void);

    // 注意：public;此由源和终点共享
    CModulationMatrix m_ModulationMatrix;

protected:
    // --- 4 个振荡器
    COscillator* m_p0sc1;
    COscillator* m_p0sc2;
    COscillator* m_p0sc3;
    COscillator* m_p0sc4;

    // --- 2 个滤波器；2 个单声道或 1 个立体声
    CFilter* m_pFilter1;
    CFilter* m_pFilter2;

    // --- 4 个 EG
    CEnvelopeGenerator m_EG1;
    CEnvelopeGenerator m_EG2;
    CEnvelopeGenerator m_EG3;
    CEnvelopeGenerator m_EG4;

    // --- 2 个 LFO
    CLFO m_LF01;
    CLFO m_LF02;

    // --- 1 个 DCA (可以是单声道或立体声)
    CDCA m_DCA;
};
```

LFO、EG 和 DCA 仅仅是静态声明，因为它们不会变化。在构造函数中，所有指针（振荡器、滤波器和全局参数）都被置为空，这禁用了它们。派生新类并设置它们的组件取决于你。

// --- 全局参数
```cpp
globalVoiceParams* m_pGlobalVoiceParams;
globalSynthParams* m_pGlobalSynthParams;
```

声明特定于新音色的振荡器和滤波器，并在派生类的构造函数中初始化这些指针。由于 MiniSynth [是] 模拟建模，我们使用以下组件：

- 振荡器：准带限幅 (COBLimitedOscillator)
- 滤波器：四阶低通滤波器配置的 Moog 梯形滤波器 (CMoodLadderFilter)

因此，MiniSynthVoice 对象的声明如下：

对象在构造函数中连接到指针：

```cpp
class MiniSynthVoice : public CVoice {
    public:
        CMiniSynthVoice(void);
        ~CMiniSynthVoice(void);
```

CVoice 对象在使用振荡器和滤波器之前会对其进行测试，因此将第二个滤波器指针设置为 NULL 将会禁用它。如果你以后决定将振荡器更改为 CWaveTable并将滤波器更改为 CDiodelFilter，你只需更改 .h 文件中的声明，其他所有工作将自动完成。注意滤波器被命名为 m_LadderFilter 是为了提醒其类型，但你也可以选择使用 m_Filter1 或在设计中让切换对象变得更容易。

