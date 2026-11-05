The FixedUpdate() function will calculate how much an object is sliding – to do this, it finds how much sideways movement the object is making (to the right relative to the Transform's rotation) – to find out how much slip is happening.

# 5.10.7 TimerClass

Our timer system is named TimerClass.cs:

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

In this script, we will only update time whenever the time is requested. Although there may be cases where the timer would need to be updated constantly, we only need to do this on demand for the games in this book. For the example games, we do not derive the class from MonoBehaviour and we call UpdateTimer() from another script; the Game Manager. If you want this script to update automatically, we will outline a method to modify the script to work like that at the end of this section.

The timer works by having a variable called currentTime that stores the amount of time since the timer was started. currentTime starts at zero, then UpdateTimer() calculates out how much time goes by between updates and adds it to currentTime. The value of currentTime can then be parsed into minutes, seconds, and milliseconds and returned as a nice, tidy formatted string in the GetFormattedTime() function of the TimerClass class.

UpdateTimer() will be the only function that updates the time system:

```
public void updateTimer()
{
    // calculate the time elapsed since the last Update()
    timeElapsed = Mathf.Abs(Time.realtimeSinceStartup - lastTime);
```