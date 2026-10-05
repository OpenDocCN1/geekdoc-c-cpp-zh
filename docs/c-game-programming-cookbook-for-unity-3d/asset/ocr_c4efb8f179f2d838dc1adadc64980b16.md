```
public void StartTimer() 
{
    // set up initial variables to start the timer
    isTimerRunning=true;
    lastTime=Time.realtimeSinceStartup;
}
```

```
public void StopTimer() 
{
    // stop the timer
    isTimerRunning=false;
}
```

```
public void ResetTimer() 
{
    // resetTimer will set the timer back to zero
    timeElapsed=0.0f;
    currentTime=0.0f;
    lastTime=Time.realtimeSinceStartup;
}
```

```
public string GetFormattedTime() 
{
    // carry out an update to the timer so it is 'up to date'
    UpdateTimer();
```

```
// grab seconds
aSecond=(int)currentTime%60;
```

```
// grab milliseconds
Millis=(int)(currentTime*100)%100;
```

```
// format strings for individual mm/ss/millis
tmp=(int)aSecond;
seconds=tmp.ToString();
if (seconds.Length<2)
    seconds="0"+seconds;
```

```
tmp=(int)aMinute;
minutes=tmp.ToString();
if (minutes.Length<2)
    minutes="0"+minutes;
```

```
tmp=(int)aMillis;
mills=tmp.ToString();
if (millis.Length<2)
    millis="0"+millis;
```