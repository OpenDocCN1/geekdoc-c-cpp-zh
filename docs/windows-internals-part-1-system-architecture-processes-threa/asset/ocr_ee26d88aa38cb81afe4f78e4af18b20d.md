Like any scheduling algorithms, however, these adjustments aren't perfect, and they might benefit all applications.

> Windows never boosts the priority of threads in the real-time range (16 through 31). Therefore, scheduling is always predictable with respect to other threads in this range. Windows assumes that if you're using the real-time thread priorities, you know what you're doing.

Client versions of Windows also include a pseudo-boosting mechanism that occurs during multimedia playback. Unlike the other priority boosts, multimedia-playback boosts are managed by a kernel-mode driver called the Multimedia Class Scheduler Service (mcssss.sys). They are not really boosts, however. The driver merely sets new priorities for the threads as needed. Therefore, none of the rules regarding boosts applies. We'll first cover the typical kernel-managed priority boosts and then talk about MMCSS and the kind of "boosting".

# Boosts due to scheduler/dispatcher events

Whenever a dispatch event occurs, the KiExtdDispatcher routine is called. Its job is to process the deferred list by calling KiProcessThreadWaitList and then call KeCheckForThreadDispatch to check whether any threads on the current processor should be scheduled. Whenever such an event occurs, the caller can specify which type of boost should be applied to the thread, and as what priority increment should be associated with. The following scenarios are considered as AdjustWait dispatch events because they delay a dispatcher (synchronization) object entering a signaled state, which might cause one or more threads to wake up:

+   * An asynchronous procedure (APC), described in Chapter 6 and in more detail in Chapter 8 and Part 2 is queued to a thread.

+   * An event is set or pulsed.

+   * A timer was set, or the system time was changed, and timers had to be reset.

+   * A mutex was released or abandoned.

+   * A process exited.

+   * An entry was inserted in a queue (KQUEUE), or the queue was flushed.

+   * A semaphore was released.

+   * A thread was alerted, suspended, resumed, frozen, or thawed.

+   * A primary UMS thread is waiting to switch to a scheduled UMS thread.

For scheduling events associated with a public API (such as SetEvent), the boost increment is specified by the caller. Windows recommends certain values to be used by developers, who might be described later. For alerts, a boost of 2 is applied (unless the thread is not priority in an alert wait by calling KeAlertThreadById, in which case the case boost is 1), because the alert API does not have a parameter allowing a caller to set a custom increment.