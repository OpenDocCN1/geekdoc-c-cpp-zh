```
this.InitializeComponent();
_timer.Tick += OnTick;
_timer.Interval = TimeSpan.FromSeconds(1);
}
private void OnTimer()
{
_timer.Start();
}
private void OnTick(object sender, object e)
{
double newAngle = rotate.Angle + 6;
if (newAngle >= 360) newAngle = 0;
rotate.Angle = newAngle;
}
private void OnStopTimer()
{
_timer.Stop();
}
```

When you run the application, the clock hand is shown (see Figure 22.2).

![](bbox=[0.05, 0.48, 0.95, 0.75])

Figure 22.2

# Summary

Chapter 21 describes how to parallelize applications using tasks. This chapter covered the issues you can have using multiple tasks, such as race conditions and deadlocks.

You’ve seen several synchronization objects that are available with .NET, and with which scenario what synchronization object has its advantage. An easy synchronization can be done using the lock