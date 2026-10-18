```
FLINK      = $(F77)
F_LIB      = (none)
F_INC      = (none)
FFLAGS     = -O3 -openmp -mmic
FLINKFLAGS = -O3 -openmp -mmic
RAND       = randi8
```

Please send all errors/feedbacks to:

NPB Development Team
npb@nas.nasa.gov

# FIGURE 25.6, Cont'd

```
119000000  #Total power for running average Window 0
118000000  #Total power for running average Window 1
121000000  #power for current 5 msec sample (Instantaneous power)
189000000  #Max Instantaneous power over some sampling period
34000000   #PCI-E connector power
33000000   #power delivered by 2x3 power connector
54000000   #power delivered by 2x4 power connector
38000000 0 869000    #Core rail (Power, Current, Voltage)
32000000 0 1000000   #Non-core rail (Power, Current, Voltage)
33000000 0 1501000   #Memory subsystem rail (Power, Current, Voltage)
```

# FIGURE 25.7

Output from a sampling of /sys/class/micras/power on an Intel Xeon Phi coprocessor.

at 1 and 244 threads. These are trivial cases that should have the same thread distribution across the cores no matter the affinity. (You may see a slight difference due to the operating system executing on the last core and, depending upon the OpenMP implementation, the threading policy avoiding allocating threads on that core.)

Look more closely at the plots. Are there any correlations between the notable features and thread distribution across cores? There is a whole host of information that you can obtain from this figure. Notice that some of the features on the “scatter” plot correspond to when all the cores are filled with the same number of executing threads, say 2 cores/thread, and your samples start filling up the next number of threads, say 3 cores/thread. For example, in Figure 25.8, at 61 threads, there is a significant drop in performance per watt. Also, the implication is that for an application (or part of an application) that is CPU bound, using affinity = “scatter” may provide better performance.

Look at the drop in performance at 61 threads. Every added thread increases the application’s performance by increasing the amount of parallelism until each of the cores is filled with a given rank, in this case, one thread per core. After every core is executing one thread, and the next rank of threads start, there is a drop in performance as the first few cores fill with the additional threads and experience