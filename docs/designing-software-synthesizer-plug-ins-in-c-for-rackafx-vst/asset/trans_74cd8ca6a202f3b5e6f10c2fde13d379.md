

```cpp
// 从我们的 AU buddy 获取 AudioUnitParameter
AudioUnitParameter parameter = (buddyAU, 0, kAudioUnitScope_Global, 0);

// -- 参数 0 -> NUMBER_OF_SYNTH_PARAMETERS-1
// 注意使用 mParameterID 添加额外参数的方式
for(int i=0; i<NUMBER_OF_SYNTH_PARAMETERS; i++)
{
    // --- 更改后续控件的参数  ID
    parameter.mParameterID = i;

    if(AudioUnitGetParameter(buddyAU, i, kAudioUnitScope_Global, 0,
        &paramValue) != noErr) {
        return;
    }

    // -- 更新控件
    id control = [self getControlWithIndex:i];
    if(control && [control respondsToSelector(
        @selector(setControlValue:))]) {
        [control controlValue:paramValue];
    }
}
```

回调函数 `eventListener` 设置了 `controlValue`，进而通知控件更新自身，包括任何可能需要的重绘。

我们设计这些控件不仅仅是为了在 AU 中使用，因此它们拥有方法可以在不使用事件监听器方案的情况下自动更新控件。换句话说，当你移动控件时，它会重绘并更新自己，而不需要 AU 插件允许它这样做。有几行代码你可以取消注释来启用此功能。你现在可以无任何问题地取消代码注释，此时控件会被重绘两次。

## 2.46 视图接口与初始化

现在我们可以通过查看视图接口（.h 文件）和初始化来找到拼图的最后碎片。我们已经涵盖了 view 中的所有函数。打开 `MiniSynth.h` 文件并查看接口定义。首先是每个控件的 `IOutlets`。它们按列排列，因为最终的 MiniSynth GUI 也是这样排列的。其之后是两个数组；一个用于存储图像，另一个用于存储视图上所有的控件。为了效率考虑，我们只创建了一个旋钮图像数组，所有旋钮控件共享该数组。

数组之后，你可以看到事件监听器对象——buddy AU、`AUEEventListener` 以及背景图像对象。最后，`getControlWithMethod` 在控件中搜索具有特定控件索引（全局参数索引）的对象。

打开 `MiniSearchView.m` 文件并查看初始化器 `awakeFromNib`。在第一部分，你创建了旋钮数组并加载了图像。之后是旋钮和选项菜单组的初始化器，它们设置了名称、索引值、最小、最大和默认值。控件限制和默认值定义在 `SynthParamLimits.h` 中。对于选项，你还传递了枚举字符串。设置控件后，它们被添加到控件数组中。你设置了

```objc
(void)event:(void*)hObject
    event:(const AudioUnitEvent*)inEvent
    value:(Float32)inValue
```

```objc
switch (inEvent->mEventType) {
    // 对于预设，每个参数都会被调用一次
    case kAudioUnitEvent_ParameterChange: {
        // --- 从我们的数组中获取控件
        id control = [self getControlWithIndex:
            inEvent->mArgument.mparameter.mparameterID];

        // --- 所有的 MY (WP) 控件都使用相同的方法，
        // setControlValue: 所以没有其他需要做的
        if(control && [control respondsToSelector:@selector(setControlValue:)])
            [control setValue:inValue];
    }
}
```

```objc
(IBAction)WPRotaryKnobChanged:(id)sender {
    if(![sender respondsTo:@selector(controlID)] ||
        ![sender respondsTo:@selector(controlValue)])
        return;

    // controlID 是参数的索引
    if([sender controlID] >= 0) {
        // -- 获取旋钮的用户值
        Float32 floatValue = [sender controlValue];

        // -- 在我们的 AU buddy 中设置 AudioUnitParameter
        AudioUnitParameter* param = (buddyAU, [sender controlID],
            kAudioUnitScope_Global, 0);

        // -- 设置 AU 参数；这会调用 au 中的 SetParameter()
        AUParameterSet(AUEventListener, sender, &param,
            (Float32)floatValue, 0);
    }
}

(IBAction)WPOptionMenuItemChanged:(id)sender

if([sender respondsToSelector:@selector(controlID)] ||
    [sender respondsToSelector:@selector(getSelectedIndex)])
    return;

if([sender controlID] >= 0) {
    // -- 获取选择索引
    Float32 floatValue = [sender getSelectedIndex];

    // -- 在我们的 AU buddy 中设置 AudioUnitParameter
    AudioUnitParameter param = (buddyAU, sender, controlID,
        kAudioUnitScope_Global, 0);

    // -- 设置 AU 参数；这会调用 au 中的 SetParameter()
    AUParameterSet(AUEventListener, sender, &param,
            (Float32)floatValue, 0);
}
```

`initialize` 方法通过 `setKnob` 调用。创建每个控件并添加到控件中。初始化器的最后部分找到并存储了背景图像。对于这个合成器，它是拉丝金属材质。你可以在这里更改背景图像进行实验。图像将被平铺。`dealloc` 方法释放我们保留的资源；注意它还移除了我们设置的监听器。最后，`drawRect` 方法平铺背景图像并为每一行或每一列设置组帧。图像来自 GUI 库并拉伸以适应。通过简单的图形计算来放置行和列帧，并使用 `drawRect` 放置组图像。

## 2.5 实现 AU 插件：调试

在将插件加载到客户端之前，使用 AU 验证工具对其进行验证至关重要。如果插件验证失败，客户端可能会拒绝再次加载它。

```objc
@interface MiniSynthView : NSView

{
// --- 旋钮组
    // --- 第1列
    @IBOutlet RotaryKnobMS* wRotaryKnob_0;
    @IBOutlet RotaryKnobMS* wRotaryKnob_1;

    // --- 声部行
    @IBOutlet OptionMenuGroupMS* wOPMG_1;
    @IBOutlet OptionMenuGroupMS* wOPOMG_2;
    @IBOutlet RotaryKnobMS* wRotaryKnob_24; // 未使用
    @IBOutlet RotaryKnobMS* wRotaryKnob_25; // 未使用

    // 控件数组
    @property NSMutableArray* controlArray;
    @property NSMutableArray* knobImages;

    // --- AU 成员
    @property AudioUnit buddyAU; // 我们连接的 AU
    @property AUEventListenerRef AUEventListener;

    // --- 背景颜色
    @property NSColor* backgroundColor; // 背景颜色
    @property NSImage* backImage;
}

// --- 在我们的数组中查找控件
-(id)getControlAtIndex:(int)index;

// --- 设置我们的 buddy AU 并初始化
-(void)setAU:(AudioUnit)inAU;

// --- 动作处理器
-(IBAction)WProtaryKnobChanged:(id)sender;
-(IBAction)WOptionMenuItemChanged:(id)sender;

// - 事件监听器相关
-(void)synchronizeUIParameterValues;
-(void)addListeners;
-(void)removeListeners;

-(void)eventListener:(void *)object event:(const AudioUnitEvent*)event value:(Float32)inValue;

@end

@implementation MiniSynthView

存储一个曾经失败过验证的产品代码列表，之后不再验证。通过打开终端并使用 AU 验证来验证你的插件：

```objc
-(void)awakeFromNib {
// --- 初始化旋钮
Bundle* bundle = [CFBundleForClass:[self class]];
// --- 创建图像数组
knobImages = [[NSMutableArray alloc] initWithCapacity:KNOB_COUNT];
for(int i=0; i<KNOB_COUNT; i++) {
    NSImage* image = nil;
    NSString* file = [NSString stringWithFormat:@"knob%04d", i];
    NSString* path = [[bundle pathForResource:file ofType:@"png"] autorelease];

    if(path)
    image = [[NSImage alloc] initWithContentsOfURL:[NSURL fileURLWithPath:path]];

    if(image)
    [knobImages addObject:image];
}
```

auval -v aumu

其中 <PLUG> 是你的 4 位插件代码，<COMP> 是你的 4 位公司名称。对于我的 MiniSynth，它将是：

```objc
// --- 初始化旋钮
controlArray = [[NSMutableArray alloc] init];

// --- 列
[wpRotaryKnob_0 initControlWithName:@"Noise Osc (dB)" controlIndex:NOISE_OSC_AMP_DB
```

auval -v aumu MS03n

如果你的验证没有成功，请回去检查你的代码。一旦成功，你就可以准备好调试合成器了。

调试你的合成器对于你自己的代码和章节挑战至关重要。当你开始尝试自己的代码或想法时，可能会像我们在实现新代码时遇到问题。为了调试和测试插件，你需要一个 AU 宿主（客户端）；我们用 AULab、Logic 9 和 Ableton 9 测试过。有两种调试方法。

简单的方法是编辑项目的 Scheme（在附录中描述）并选择一个执行文件——执行文件就是 AU 宿主。然后，你可以点击三角形按钮重新构建并启动宿主进行调试。这种方法允许你在控制窗口记录字符串。

你还可以在客户端运行时启动调试器（你需要手动启动客户端）。客户端运行时，调试-附加进程 并在进程列表中选择客户端，然后设置断点。当你实例化插件时，断点将激活，你可以像往常一样单步执行。区别在于当你使用附加进程机制时，无法通过 printf 语句向控制窗口记录信息。调试日志非常有用，我们将在下一节中使用它记录 MIDI 事件。Apple, Inc. "The Audio Programming Guide." Accessed June 2014,
://developer.apple.com/library/mac/documentation/MusicAudio/Conceptual/AudioProgrammingGuide/Introduction.html

Pirkle, Will. 2012. Designing Audio Effects Plug-Ins in C++, Chap. 2. Burlington: Focal Press.

Rogerson, Dale. 1997. Inside COM, Chap. 1–7. Redmond: Microsoft Software.

Steinberg GmbH. "VST3 SDK." Accessed June 2014,
http://www.steinberg.net/en/cn/company/developers/sdk_download_portal.html

