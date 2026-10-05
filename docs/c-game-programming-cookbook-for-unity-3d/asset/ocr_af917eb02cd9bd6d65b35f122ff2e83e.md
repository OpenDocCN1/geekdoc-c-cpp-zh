```
// pull together a formatted string to return
timeString=minutes+":"+seconds+":"+millis;

return timeString;

public int GetTime () {
    // remember to call UpdateTimer() before trying to use this
    // function, otherwise the time value will not be up to date
    return (int) (currentTime);
}
```

# 4.2.1 Script Breakdown

we will only update time whenever the time is requested. Although there may be cases where the timer would need to be updated constantly, in the projects for this book we only need to do it on demand. So, after the variable declarations, the TimerClass sc scripts begin with an update function called UpdateTimer(). Note that if you wanted the timer to update constantly, you would derive the class from MonoBehavior (instead of ScriptableObject it currently does) and add a call to UpdateTimer in your main function.

The timer works by having a variable currentTime that stores the amount of time elapsed since the timer started. currentTime starts at zero, UpdateTimer() calculates how much time goes by updates and adds it to currentTime. The value of currentTime is then parsed into minutes, seconds, and milliseconds, and returned as a nice, tidy formatted string in the GetFormattedTimer() function of the same class. UpdateTimer will be the only function that updates the timer's time system:

```
public void UpdateTimer () {
    // calculate the time elapsed since the last Update()
    timeElapsed=Math.Abs(Time.realtimeSinceStart-lastTime);
```

A variable calledElapsed tracks how much time has gone by between updates. realtimeSinceStart is used for good reason. By using realtimeSinceStart, the game can do whatever it likes to the Time.timeScale value (speeding up or slowing down Unity physics updates), and realtimeSinceStart will still provide usable values. If time were used, it would be affected by the timeScale and fail to provide real-time values if its value were set to anything other than 1.

```
// if the timer is running, we add the time elapsed to the
    // current time (advancing the timer)
    if (isTimerRunning) {
        currentTime+=timeElapsed*timeScaleFactor;
}
```