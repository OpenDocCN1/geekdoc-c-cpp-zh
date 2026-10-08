```
void CStereoDelayFX::reset() {
    // --- flush buffers and reset index values

    m_LeftDelay.resetDelay();
    m_RightDelay.resetDelay();
}
```

# prepareForPlay()

This is the one-time-initialization function for the object. The plug-in calls it during its own one-time-initialization function and passes the current sample rate. This function passes that sample rate to the member objects and then calls the init() function to request the allocation of two seconds worth of buffers.

```
// --- one time init
void CStereoDelayFX::prepareForPlay(double dSampleRate) {
    // --- set sample rate first
    m_LeftDelay.setSampleRate((int)dSampleRate);
    m_RightDelay.setSampleRate((int)dSampleRate);

    // --- initialize to 2 sec max delay
    m_LeftDelay.init(2.0*dSampleRate);
    m_RightDelay.init(2.0*dSampleRate);

    // --- do the flush
    reset();
}
```

# update()

update() function takes the delay ratio and calculates the individual delay times on the left and right delay lines using the logic at the beginning of the section. For negative ratios, notice the negation operation, which is the equivalent of calling an absolute value function here.