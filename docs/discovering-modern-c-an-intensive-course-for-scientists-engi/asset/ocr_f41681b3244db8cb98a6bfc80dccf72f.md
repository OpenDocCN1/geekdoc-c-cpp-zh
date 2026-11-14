For not polluting our benchmarks with the clock overhead, we run multiple computations and scale down our time interval accordingly:

```
cout << "my_root(3.0) = " << r3 << ", the calculation took " << ((end - start) / rep).count() << " ticks\n";
```

yielding on the test machine:

my_root(3.0) = 1.73205, the calculation took 54 ticks

Thus, we should know how long a tick is. We will figure this out later. First, we convert the duration into something more tangible like microseconds:

```
duration_cast<microseconds>((end - start) / rep).count()
```

Our new output is

my_root(3.0) = 1.73205, the calculation took 0 µs

count returns an integer value and our computation took apparently less than a microsecond. For printing the duration with three decimal places, we convert it to nanoseconds and divide this by the double value 1000.0:

```
duration_cast<nanoseconds>((end - start) / rep).count() / 1000.
```

Note the dot at the end; if we divided by an int, we would cut off the fractional part:

my_root(3.0) = 1.73205, the calculation took 0.054 micros

The resolution of a clock is given by a ratio of a second in the clock's internal typedef period:

```
using P = steady_clock::period; // type of time' unit
cout << "Resolution is: " << double(P::num) / P::den << " s.\n";
```

The output on the test machine was

Resolution is 1e-09s.

Thus, the resolution of the clock is one nanosecond. The library distinguishes three clocks:

+   The system_clock represents the native wall clock on the system. It is compatible with <ctime> as needed in our first example.

+   The high_resolution_clock has the maximal resolution possible on the underlying system.

+   steady_clock is a clock with guaranteed increasing time points. The other two clocks might be adjusted (e.g., at midnight) on some platforms so that later time points might have lower values. This can lead to negative durations and other nonsense. Therefore, steady_clock is the most convenient for a timer (when the resolution is sufficient).

People knowing <ctime> might find <chrono> somewhat complicated at the beginning, but we don't need to deal with seconds, milliseconds, microseconds, and nanoseconds in different interfaces. The C++ library offers a uniform interface, and many errors can be detected at the type level—making the programs much safer.