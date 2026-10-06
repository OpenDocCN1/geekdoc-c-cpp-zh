In the constructor, we create two QTimer objects: updateTimer is used to refresh the appearance of the widget every five seconds, finishTimer emits the widget's timeout() signal when the oven timer reaches 0. The finishTimer needs to time out only, so we call setSingleShot(true); by default, timers fire repeatedly until they are stopped or destroyed. The last connect() call is an optimization to stop updating the widget when the timer is inactive.

At the end of the constructor, we set the point size of the font used for drawing the widget to 9 points. At the end, this is done to ensure that the numbers displayed on the widget have approximately the same size everywhere.

```
void OvenTimer::setDuration(int secs)
{
    secs = qBound(0, secs, MaxSeconds);

    finishTime = QDateTime::currentDateTime().addSecs(secs);

    if (secs > 0)
        updateTimer->start(UpdateInterval 1000);
        finishTimer->start(secs 1000);
    } else {
        updateTimer->stop();
        finishTimer->stop();
    }
    update();
}
```

The setDuration() function sets the duration of the oven timer to the given number of seconds. Using Qt's qBound() function means that we can avoid writing code such as this:

```
if (secs < 0) {
    secs = 0;
} else if (secs > MaxSeconds) {
    secs = MaxSeconds;
}
```

We compute the finish time by adding the duration to the current time (obtained from QDateTime::currentDateTime()) and store it in the finishTime private variable. At the end, we call update() to redraw the widget with the new duration.

The finishTime variable is of type QDateTime. Since the variable holds both a date