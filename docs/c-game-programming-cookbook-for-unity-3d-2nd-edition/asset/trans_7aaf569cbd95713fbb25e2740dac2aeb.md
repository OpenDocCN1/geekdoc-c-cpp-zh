
FixedUpdate() 函数将计算物体滑动多少——为此，它会找出物体做了多少侧向移动（相对于 Transform 旋转的右侧）——以确定发生了多少滑移。

## 5.10.7 TimerClass

我们的计时器系统命名为 TimerClass.cs：

```
using UnityEngine;
using System.Collections;

namespace GPC
{
    [AddComponentMenu("CSharpBookCode/Common/Timer class")]
    public class TimerClass : ScriptableObject
    {
        public bool isTimerRunning = false;
        private float timeElapsed = 0.0f;
        private float currentTime = 0.0f;
        private float lastTime = 0.0f;
        private float timeScaleFactor = 1.0f; // <-- If you need to scale time, change this!
        private string timeString;
        private string hour;
        private string minutes;
        private string seconds;
        private string millis;
        private int aHour;
        private int aMinute;
        private int aSecond;
        private int aMillis;
        private int tmp;
        private int aTime;
        private GameObject callback;
        public void UpdateTimer()
        {
```

在这个脚本中，我们只在请求时间时更新时间。虽然有些情况下计时器需要持续更新，但对于本书中的游戏，我们只需要按需更新。对于示例游戏，我们不让类派生自 MonoBehaviour，而是从另一个脚本（Game Manager）调用 UpdateTimer()。如果你希望此脚本自动更新，我们将在本节末尾概述一种修改脚本以实现该行为的方法。

计时器的工作方式是有一个名为 currentTime 的变量，它存储自计时器启动以来经过的时间。currentTime 从零开始，然后 UpdateTimer() 计算两次更新之间经过了多少时间，并将其加到 currentTime 上。然后，currentTime 的值可以在 TimerClass 类的 GetFormattedTime() 函数中解析为分钟、秒和毫秒，并作为整洁美观的格式化字符串返回。

UpdateTimer() 将是唯一更新时间系统的函数：

```
public void UpdateTimer()
{
    // calculate the time elapsed since the last Update()
    timeElapsed = Mathf.Abs(Time.realtimeSinceStartup - lastTime);
```

```
// if the timer is running, we add the time elapsed to the current time (advancing the timer)
if (isTimerRunning)
{
    currentTime += timeElapsed * timeScaleFactor;
}
// store the current time so that we can use it on the next update
    lastTime = Time.realtimeSinceStartup;
```

上面，该函数的工作方式如下：

- 1. 我们通过取当前时间（Time.realtimeSinceStartup）并从中减去 lastTime 的值来计算 timeElapsed——lastTime 在此函数末尾被设置为 Time.realtimeSinceStartup 的值，这意味着 lastTime 会一直保留其值，直到下次 UpdateTimer 运行。由于它保留其值，它充当 Unity 上次到达该函数末尾时的时间戳。通过从当前时间中减去此时间戳，我们就能确切知道自 UpdateTimer() 上次运行以来经过了多少时间。
- 2. 如果计时器正在运行（即布尔变量 isTimerRunning 设置为 true），那么我们将 timeElapsed 加到 currentTime 变量上。currentTime 是自计时器启动以来经过的总时间。当我们将 timeElapsed 加到 currentTime 时，还将其乘以 timeScaleFactor。这允许你缩放时间系统，当你的游戏更新被设置为以与 Time.timeScale 不同的时间缩放运行时，这很有用。

使用 realtimeSinceStartup 是有充分理由的。通过使用 realtimeSinceStartup，游戏可以对 Time.timeScale 值做任何它想做的事（加快或减慢 Unity 物理更新），而 realtimeSinceStartup 仍会提供未缩放的时间值。如果使用 Time.time，它会受 timeScale 影响，并且如果物理计时（Time.timeScale）被设置为 1 以外的任何值，就无法提供实时值。

> 注意：暂停 Unity 游戏的一种常用方法是将 Time.timeScale 设置为 0，这会停止未使用 Time.realtimeSinceStartup 的计时器。如果你使用 Time.timeScale 暂停游戏，你还需要启动和停止计时器，因为它不受 Time.timeScale 影响。

接下来，StartTimer() 函数用于启动计时器：

```
public void StartTimer ()
{
    // set up initial variables to start the timer
    isTimerRunning=true;
    lastTime=Time.realtimeSinceStartup;
}
```

上面，当调用 StartTimer() 时，布尔变量 isTimerRunning 被设置为 true。isTimerRunning 用于说明是否要在脚本前面的 UpdateTimer() 函数中更新 currentTime。启动计时器时，lastTime 也需要重置，以防计时器之前一直在运行。如果计时器之前一直在运行，我们这样做是为了确保计时器停止与再次启动之间的任何时间都不被计入。

```
public void StopTimer()
{
    // stop the timer
    isTimerRunning = false;

    // carry out an update to the timer
    UpdateTimer();
}
```

在上面的 StopTimer() 中，isTimerRunning 被设置为 false，这会阻止 UpdateTimer() 向 currentTime 变量添加任何额外时间。为了确保正确计算最后一点时间，在上面的函数末尾快速调用一次 UpdateTimer()。

如果有时需要重置计时器，我们需要将主要变量刷新为默认状态。在 ResetTimer() 函数中，timeElapsed、lastTime 和 currentTime 被重置：

```
public void ResetTimer()
{
    // resetTimer will set the timer back to zero
    timeElapsed = 0.0f;
    currentTime = 0.0f;
    lastTime = Time.realtimeSinceStartup;

    // carry out an update to the timer
    UpdateTimer();
}
```

上面，我们将所有时间变量重置为起始状态，并调用 UpdateTimer() 再次启动计时器过程。

每当我们需要在屏幕上显示时间时，很可能需要将其格式化为类似“分钟:秒:毫秒”的形式。GetFormattedTime 函数接收该值，将其拆分为我们需要的单位，然后组合成格式良好的字符串并返回：

```
public string GetFormattedTime()
{
    // carry out an update to the timer so it is 'up to date'
    UpdateTimer();
}
```

上面，首先调用 GetFormattedTime()。如前所述，计时器不会自行更新——它是一个惰性更新器，只在我们请求时才更新，因此在提供格式化时间之前这样做可确保计算是最新的。

从那时起，我们只是进行数学运算，从 currentTime 中获取分钟、秒和毫秒值：

```
// grab hours
aHour = (int)currentTime / 3600;
aHour = aHour % 24;
// grab minutes
aMinute = (int)currentTime / 60;
```

```csharp
aMinute = aMinute % 60;
// grab seconds
aSecond = (int)currentTime % 60;

// grab milliseconds
aMillis = (int)(currentTime * 100) % 100;
```

在分钟、秒和毫秒值被计算并存储到整数变量 aMinute、aSecond 和 aMillis 中之后，会由它们构建三个新字符串，分别称为 seconds、minutes 和 mills：

```csharp
// format strings for individual mm/ss/mills
tmp = (int)aSecond;
seconds = tmp.ToString("D2"); // ToString()
```

会进行格式化……在本例中，D 后跟数字的位数

```csharp
tmp = (int)aMinute;
minutes = tmp.ToString("D2");

tmp = (int)aHour;
hour = tmp.ToString("D2");

tmp = (int)aMillis;
mills = tmp.ToString("D2");
```

```csharp
// pull together a formatted string to return
timeString = minutes + ":" + seconds + ":" +
mills;
```

在 C# 中，你可以使用 ToString() 函数将数字转换为字符串。ToString() 的一大优点是还可以传入格式字符串。格式字符串的形式为一个字母后跟一个整数。上面，我们使用格式字符串 D2 告诉 ToString() 使用两位数，这会将我们的时间转换为整洁、可显示的格式。请注意，你可以通过更改格式字符串中的数字来设置任意位数。有关格式字符串的更多信息，你可以在线在微软的 .NET 标准数字格式字符串页面找到完整说明和所有可用格式选项的完整列表：https://docs.microsoft.com/en-us/dotnet/standard/base-types/standard-numeric-format-strings

一旦格式化时间字符串的各个部分准备就绪，我们就将它们全部组合成最终的 timeString，并在函数末尾返回它，如下所示：

```csharp
// pull together a formatted string to return
timeString=minutes+":"+seconds+":"+mills;

return timeString;
}
```

在脚本的最后，GetTime() 函数为其他脚本提供了一种处理 currentTime 值的方法：

```csharp
public int GetTime ()
{
    // remember to call UpdateTimer() before trying to
use this function, otherwise the time value will
    // not be up to date
    return (int)currentTime;
}
```
