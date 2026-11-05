|  |  |
|---|---|
| 12. | public static LocalDataStoreSlot GetNamedDataSlot(string name) |
|  | Looks up a named data slot. For better performance, use fields that are marked with the ThreadStaticAttribute attribute instead. |
| 13. | public void Interrupt() |
|  | Interrupts a thread that is in the WaitSleepJoin thread state. |
| 14. | public void Join() |
|  | Blocks the calling thread until a thread terminates, while continuing to perform standard COM and SendMessage pumping. This method has different overloaded forms. |
| 15. | public static void MemoryBarrier() |
|  | Synchronizes memory access as follows: The processor executing the current thread cannot reorder instructions in such a way that memory accesses prior to the call to MemoryBarrier execute after memory accesses that follow the call to MemoryBarrier. |
| 16. | public static void ResetAbort() |
|  | Cancels an Abort requested for the current thread. |
| 17. | public static void SetData(LocalDataStoreSlot slot, Object data) |
|  | Sets the data in the specified slot on the currently running thread, for that thread's current domain. For better performance, use fields marked with the ThreadStaticAttribute attribute instead. |
| 18. | public void Start() |
|  | Starts a thread. |
| 19. | public static void Sleep(int millisecondsTimeout) |
|  | Makes the thread pause for a period of time. |
| 20. | public static void SpinWait(int iterations) |
|  | Causes a thread to wait the number of times defined by the iterations parameter |
| 21. | public static byte VolatileRead(ref byte address) |
|  | public static double VolatileRead(ref double address) |
|  | public static int VolatileRead(ref int address) |