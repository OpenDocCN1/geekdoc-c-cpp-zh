If the ready thread cannot be run right, it is moved into the ready state on the shared or local queue (as appropriate base on affinity constraints), where it will await its turn to run. As seen in the scheduling scenarios earlier, the thread will be inserted either at the head or the tail of the queue, based on whether it entered the ready state due to preemption.

> Note Regardless of the underlying scenario and various possibilities, threads are mostly put on their ideal processor's per-processor ready queues, guaranteeing the consistency of the algorithms that determine which logical processor picks a thread to run.

# Heterogeneous scheduling (big.LITTLE)

The kernel assumes SMP system, as previously described. However some ARM-based processors contain multiple cores that are not the same. A typical ARM CPU (for example, from Qualcomm) contains some powerful cores, which should run for short periods at a time (and consume more energy); and set of weaker cores, which can run for longer periods (and consume less energy). This is sometimes called big.LITTLE.

Windows 10 introduced to distinguish between these cores and schedule based on the core's size and policy, including the foreground status of the thread, its priority, and its expected runtime. Windows initializes the set of processors when the Power Manager is initialized by calling pInitializeHeteroScheduler (and if processors are not added to the system). The function allows the simulation of hetero systems (for, testing purposes) by adding keys under the registry HKLM\System\CurrentControlSet\SessionManager\Kernel1\KGroups as follows:

+   - A key should use two decimal digits to identify a processor group number. (Recall that each group holds at most 64 processors). For example, if 0 is the first group, 1 is the second, (On most systems, one group suffices).

+   - Each key should contain a DWORD value named SmAllProcessorMask that is a mask of processors that would be considered small. For example, if the value is 3 (the first two bits are on) and the group has six total processors, that would mean 0 and 1 (3 or 2 are small), while the other four processors are big. This is essentially the same as an affinity mask.

The kernel has several policy options that can be tweaked when dealing with hetero systems, stored in global variables. Table 4-5 shows some of these variables and their meaning.

TABLE 4-5 Heter kernel variables

| Variable Name | Meaning | Default Value |
|---|---|---|
| KiHeteroSystem | Is the system heterogeneous? | False |
| PopHeteroSystem | System hetero type: None (0) Simulated (1) EfficiencyClass (2) FavoredCore (3) | None (0) |