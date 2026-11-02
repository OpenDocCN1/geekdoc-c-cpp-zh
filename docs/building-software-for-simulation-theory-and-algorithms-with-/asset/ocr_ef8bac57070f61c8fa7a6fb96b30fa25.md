power experiment run at half throttle with a signal frequency of 7000 Hz. The *Hybrid* class now shows up clearly as a performance problem, consuming almost half of the execution time in its *trial_step* method.

The *trial_step* method is called only when an event occurs in the *Hybrid* class. Looking a little further into the profile, the *delta_ext* method of the *Hybrid* class appears at the ninth spot in the list. This suggests that a large number of trial steps are being executed in response to input events received by the *TankPhysics*, which is the only *Hybrid* object in our simulation. The call graph for the *delta_ext* method seems to confirm this. The relevant portions of the profile are shown in the tables.

The cumulative time spent in the *delta_ext* method and its children amounts to 85.7% of the total execution time. Of the methods that it calls, the most time consuming is the *integrate* method, using up 82% of the total execution time, which in turn calls the culprit at the top of Table A.1: *trial_step*. Each input to the *Hybrid* model causes the integration step to be performed, and this is degrading the performance of the simulation.

From here, it is easy to deduce that frequent voltage events arriving from the *InterruptHandler* are the root of the problem. Fortunately, most of these events do not actually change the voltage value, and so there is a simple remedy for the performance problem. The modified output function is shown below. It produces an event only when the voltage actually changes. This cuts the execution time by roughly 1/3, and now the model works admirably as part of the interactive tank simulation. Such a substantial performance improvement with so simple a change is unusual, but the ease with which the problematic section of code was identified shows the tremendous benefits of using a profiler.

# Optimized Output Method for the InterruptHandler

```
```cpp
void InterruptHandler::output_func(Bag<SimEvent>& yb)
{
    // If this is the start of an interrupt, send the motor voltage
    // and an interrupt indicator
    if (phase == OUTPUT) {
        // If the voltage changed, then send the new values
        if (last_left_v != left_v || last_right_v != right_v) {
            SimMotorVoltage vol;
            volts.el = left_v;
            volts.er = right_v;
            yb.insert(SimEvent(volts));
        }
        // Send the interrupt indicator
        yb.insert(SimEvent(SIM_INTERRUPT));
    }
    // If this is the start of an interrupt, then send an indicator for it
    else if (phase == WAIT) {
        yb.insert(SimEvent(SIM_INTERRUPT));
    }
}
```
```