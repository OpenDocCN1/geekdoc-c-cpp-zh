

对于大多数简单应用的关键对象是 `uBit.audio.soundExpressions`，最常用的方法是 `play("sound")` 和 `playAsync("sound")`，它们的作用相同，但 `playAsync` 在后台运行。声音字符串可用于详细指定你想要的声音，这里有一些预定义的声音可用：

| 咯咯笑 | 你好 | 悲伤 | 飞翔 | 闪烁 |
| 快乐 | 神秘 | 滑动 | 弹簧 | 打哈哈欠 |

必须说的是，很多音效听起来并不像描述的那样！
产生的声音由一种相当复杂的字符串格式描述，每个音频样本包含 72 个字符：

Start
[0] wave 0 SineTone
1 SawtoothTone
2 TriangleTone
3 SquareWaveTone
4 Noise

```
[1] volume 0000-1023
[5] frequency 0000-9999
[9] duration 0000-9999
[13] shape 00 noInterpolation
01 linearInterpolation
02 curveInterpolation
05 exponentialFallingInterpolation;
06 exponentialFallingInterpolation;
08 aggrioAscending majorScale
09 aggrioDescending majorScale
10 aggrioAscending minorScale
11 aggrioDescending minorScale
12 aggrioAsc diminished
13 aggrioDescending diminished
14 aggrioAscending chromatic
15 aggrioDescending chromatic
16 aggrioAscending wholeTone
17 aggrioDescending wholeTone
18 logarithmicInterpolation;
```

[15] unused XXX
[18] end frequency 0000-9999
[22] unused XXX
[26] end volume 0000-1023
[30] steps 0000-9999
[34] fx choice 00 volumeRampEffect
01 frequencyVibratoEffect
02 volumeVibratoEffect
03 warbleInterpolation

[36] fxParam 0000-9999
[40] fxnSteps 0000-9999

[44] freq. random 0000-9999
[48] end freq 0000-9999
[52] volume random 0000-9999
[56] end vol random 0000-9999
[60] duration random 0000-9999
[64] fxParamRandom 0000-9999
[68] fxnStepsRandom 0000-9999

持续时间近似以毫秒为单位，频率近似以赫兹为单位。基本思想是设置起始和结束频率以及音量，然后选择这些值在持续时间内如何变化。因此，选择线性插值（linear interpolation）会让频率和音量从起始值平滑变化到结束值。还有许多方法可以通过应用效果和随机变化来修改声音，但这超出了本书的范范围。

如果我们写一个可以更改 `ManagedString` 任何部分的短函数，那么构造音频效果就会变得简单：

```
ManagedString setSound(ManagedString audio,
    ManagedString data, int s)
{
    return audio.substring(0, s) + data +
        audio.substring(s + data.length(),
        audio.length() - s data.length());
}
```

使用这，我们可以创建一个播放 500ms 恒正弦波的简单效果：

```
#include "MicroBit.h"
MicroBit uBit;
int main() {
	uBit.initString();
	// 72 characters
	static ManagedString soundData(
		"0000000000000000000000000000000000000000000000000000000000");

soundData = setSound(soundData, "0", 0); // 波形
soundData = setSound(soundData, "1023", 1); // 音量起始
soundData = setSound(soundData, "1023", 26); // 音量结束
soundData = setSound(soundData, "1000", 5); // 频率起始
soundData = setSound(soundData, "1000", 18); // 频率结束
soundData = setSound(soundData, "0", 13); // 形状

soundData = setSound(soundData, "500", 9); // 持续时间
soundData = setSound(soundData, "0128", 30); // 步骤

uBit.audio.soundExpressions.play(soundData);

	return 0;
}
```

这会按预期产生“哔”声。
如果我们将规格改为：

```
soundData = setSound(soundData, "01", 13); // 形状
soundData = setSound(soundData, "9000", 18); // 频率结束
```

你会听到一个上升调。
值得说明的是音效涉及多个帧 72 字符的帧。
如果这对于创建一个简单的哔声来说太复杂了，那么好消息是，microbit 的方法在重定向到扬声器时同样有效：

```
void analogPitch(int frequency, int vol, int ms) {
	uBit.io.speaker.setAnalogValue(vol);
	uBit.io.speaker.setAnalogPeriodUs(1000000/frequency);
	uBit.io.sleep(ms);
	uBit.io.speaker.setAnalogValue(0);
}
```

# 摩斯电发送器

作为一个使用无线电和声音稍微复杂的示例，让我们实现一个摩斯电发送器。摩斯电虽然过时了但很有意义，值得学习。其思想是字母表中的每个字母都编码为短音和长音的序列，通常称为点（dot）和划（dash），例如字母 A 是点划。基本思想是点和划没有固定的长度，除了划的长度应该是点的三倍之外，字母之间用点长度的静音分隔。

创建一个摩斯电传输程序只需要在按下 A 键时开启 LED 并启动声音，在松开时关闭 LED 并停止声音。实现此点的简单方法是利用按钮的按下和释放事件。如果我们使用无线电来调用相应的函数。这使得本地 microbit 上的程序运行。

```
#include "MicroBit.h"
MicroBit uBit;

void beepOn(ManagedString e) {
    // ...
}

void beepOff(ManagedString e) {
    // ...
}
```
