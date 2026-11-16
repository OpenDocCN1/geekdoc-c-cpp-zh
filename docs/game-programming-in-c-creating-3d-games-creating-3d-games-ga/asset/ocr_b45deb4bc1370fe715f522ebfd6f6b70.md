```
```cpp
float InputSystem::Filter1D(int input)
{
    // A value < dead zone is interpreted as 0%
    const int deadZone = 250;
    // A value > max value is interpreted as 100%
    const int maxValue = 30000;

    float retVal = 0.0f;

    // Take absolute value of input
    int absValue = input > 0 ? input : -input;
    // Ignore input within dead zone
    if (absValue > deadZone)
    {
        // Compute fractional value between dead zone and max value
        retVal = static_cast<float>(absValue - deadZone) /
                 (maxValue - deadZone);

        // Make sure sign matches original value
        retVal = input > 0 ? retVal : -1.0f * retVal;

        // Clamp between -1.0f and 1.0f
        retVal = Math::Clamp(retVal, -1.0f, 1.0f);
    }

    return retVal;
}
```
```