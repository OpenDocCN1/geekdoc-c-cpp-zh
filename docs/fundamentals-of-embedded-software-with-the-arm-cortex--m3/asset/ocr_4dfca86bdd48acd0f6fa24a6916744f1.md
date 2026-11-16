![](bbox=[0.25, 0.08, 0.82, 0.29])

situation diminishes rapidly. Fortunately, development tools do exist that can analyze software and detect such situations automatically, but it is still the programmer who has to find a solution to the problem.

It is important to realize that deadlock simply is not possible when critical sections are protected by turning off task switching or by disabling interrupts. Unfortunately, these techniques are only appropriate for short critical sections. A mutex is the only reasonable way to protect long critical sections without affecting the response time of other tasks.

There are several different strategies for dealing with deadlocks. A common approach is to require all threads to acquire resources in the same order. However, even though the specific order chosen is arbitrary, it often causes resources to be locked for longer than necessary. Occasionally there is no order that can be found that is convenient for all threads. When this happens, an alternative strategy is to require a thread to release all its acquired resources and start over if any one resource cannot be acquired. There are even algorithms for detecting when a deadlock has occurred, but breaking a deadlock once it has been detected is not practical in most real-time systems.

# 10.8 WATCHDOG TIMERS

Priority inversion and deadlock can cause a real-time system to fail. Although strategies exist to avoid such problems, they sometimes are not implemented due to expense, complexity, or oversight. Even when they are, the system may still fail because of programming errors, hardware failure, or unanticipated situations.

If continuous operation of the embedded application is critical, and if the failure is only temporary, then a watchdog timer can be used to provide a primitive recovery mechanism. A watchdog timer is simply a hardware counter that counts down toward zero at a fixed rate. The software is expected to periodically restart the counter so that it never actually reaches zero. If the counter does reach zero, a failure is assumed to have occurred. The watchdog hardware then sends a reset signal to the CPU, causing