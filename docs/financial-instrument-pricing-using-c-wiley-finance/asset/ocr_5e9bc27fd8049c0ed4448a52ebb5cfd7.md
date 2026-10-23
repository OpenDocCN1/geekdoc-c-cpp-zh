```
public:
    StopWatch() :isStart(false), isEnd(false) {}
    StopWatch(const StopWatch<TickType, UnitType>& src) = delete;
    StopWatch<TickType, UnitType>& operator
        = (const StopWatch<TickType, UnitType>& src) = delete;

    void Start();
    void Stop();
    void Reset();  // Reset the time to NOW

    // Duration between start and stop in seconds; reset
    TickType GetTime();
};
```

The code body is:

```
template <typename TickType,typename UnitType>
    void StopWatch<TickType,UnitType>::Start()
{
    start = std::chrono::system_clock::now();
    isStart = true;
}

template <typename TickType,typename UnitType>
    void StopWatch<TickType,UnitType>::Stop()
{
    end = std::chrono::system_clock::now();
    isEnd = true;
}

template <typename TickType,typename UnitType>
    void StopWatch<TickType,UnitType>::Reset()
{
    start = std::chrono::system_clock::now();
    isStart = false;
    end = std::chrono::system_clock::now();
    isEnd = false;
}

template <typename TickType,typename UnitType>
    TickType StopWatch<TickType,UnitType>::GetTime()
{
    TickType count;
    if (isStart && isEnd)
    {
        // Seconds as unit type (default)
        std::chrono::duration<TickType, UnitType> D = end - start;
        count = D.count();
    }
    else
```