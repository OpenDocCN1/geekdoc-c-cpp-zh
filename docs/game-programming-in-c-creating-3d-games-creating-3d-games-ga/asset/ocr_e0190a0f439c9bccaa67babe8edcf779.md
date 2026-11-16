```
result = mSystem->initialize(
    512, // Max number of concurrent sounds
    FMOD_STUDIO_INIT_NORMAL, // Use default settings
    FMOD_INIT_CHANNEL_LOWPASS, // Initialize low-pass filter
    nullptr // Usually null
);
```