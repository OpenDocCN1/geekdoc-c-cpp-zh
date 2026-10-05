Note The fact that the executive, high-level, graphics-related, Win32k structure is pointed to by KTHREAD instead of the ETHREAD appears to be a layer violation or oversight in the standard kernel's abstraction architecture. The scheduler and other low-level components do not use this field.

Most of the fields illustrated in Figure 4-1 are self-explanatory. The first member of the ETHREAD is called Tcb. This is short for thread control block, which is a structure of type KTHREAD. Following that are the thread identification, the process identification information (including a pointer to the owning process so its environment can be accessed); security information in the form of a pointer to the access token and impersonation information, fields relating to Asynchronous Local Procedure Call (ALPC) messages, pending I/O requests (IRPs) and Windows 10-specific fields relating to power management (described in Chapter 6, "I/O system") and CPU Sets (described later in this chapter). Some of these fields are described in more detail elsewhere in this book. For more details on the internal structure of an ETHREAD structure, you can use the kernel debugger dt to display its format.

Let’s take a closer look at two of key data structures referred to in the preceding text: ETHREAD and KTHREAD. The KTHREAD structure (which is the Tcb member of the ETHREAD) contains information that the Windows kernel needs to perform thread scheduling, synchronization, and timekeeping functions.

# EXPERIMENT: Displaying ETHREAD and KTHREAD structures

You can display the ETHREAD and KTHREAD structures with the dt command in the kernel debugger. The following output shows the format of an ETHREAD on a 64-bit Windows 10 system:

```
1kd> dt ntl_ethread
+0x000 Tcb : _KTHREAD
+0x5d8 CreateTime : _LARGE_INTEGER
+0x5e0 Exit : _LARGE_INTEGER

+0xa70 EnergyValues : Ptr64 _THREAD_ENERGY_VALUES
+0xa78 CmClientReferences : UInt84
+0x7b0 SelectedCpuSets : UInt8b
+0x7b0 SelectedCpuSetsIndirect : Ptr64 UInt8b
+0x7b6 Silo : Ptr64 _EJOB
```

```
1kd> dt ntl_kthread
+0x000 Header : _DISPATCHER_HEADER
+0x018 SlistFaultAddress : Ptr64 Void
+0x020 QuantumTarget : Ptr64 Void
+0x028 InitialState : Ptr64 Void
+0x030 StackLimit : Ptr64 Void
+0x038 StackBase : Ptr64 Void
```