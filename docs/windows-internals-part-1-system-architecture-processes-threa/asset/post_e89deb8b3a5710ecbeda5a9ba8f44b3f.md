
## TABLE 4-6 DFSS registry configuration parameters

| Registry Value Name | Kernel Variable Name | Default Value |
|---|---|---|---|
| DssShortTermSharingMS | PsDfShortTermSharingMS | The time takes for the group rank to increase within a generation cycle | 30 ms |
| DssLongTermSharingMS | PsDfLongTermSharingMS | The time takes to jump from rank 0 to a non-zero rank when the threads exceed their quota within the generation cycle | 15 ms |
| DssGenerationLengthMS | PsDfGenerationLengthMS | The generation time over which to CPU usage averages | 600 ms |
| DssLongTermFraction1024 | PsDfLongTermFraction1024 | The value used in a formula for exponential averaging used for long-term complex cycles | 512 |

After DFSS is enabled, whenever a new session is created (other than session 0), MiSessionObjectCreate a scheduling group associated with the session with the default weight of 5, which is the middle between the minimum of 1 and the maximum of 9. A scheduling group manages either DFSS or CPU rate (see the next section) information based on a policy structure (SCHEDULING_GROUP_POLICY) which is part of a scheduling group. The type indicates whether it's configured for DFSS (WeightBased=0) or rate control (RateControl=1). MiSessionGetObject calls InsertSchedulingGroup to insert the scheduling group into a global system list (maintained in the global variable KiSchedulingList). The resulting scheduling group is linked to the SESSION_OBJECT structure for the particular session.

## EXPERIMENT: Posted to DFSS in action

In this experiment, you'll configure a system to use DFSS and watch it “do its thing”.

- 1. Add the registry keys and values as described in this section. (You can try this experiment on a VM as well.) Then restart the system for the changes to take effect.
- 2. To make sure DFSS is active, open a live kernel debug session and inspect the value of PscpuFairShareEnabled by issuing the following command. A value of 1 indicates DFSS is active.
- 3. In the debugger, look at the current thread. (It should be that the thread is part of a scheduling group and its KSC is not NULL because the thread was running at the time of display).

```
1kd> db!PscpuFairShareEnabled L1
ffff800!S18372ea 01

1kd> !thread
THREAD fffd28c07231640 Cid 196c.1a60 Teb: 00000f897f4b000 Win32Thread: fff28c0b9b0400 running on processor 1
IRP List:
```

ffffd280c6fac10: (0006,0118) Flags: 00060000 Mdl: 00000000

Not impersonating fffffac0d33668340
DeviceMap Image: windbg.exe
Owning Process fffff28c0710fd80
Attached Process N/A Image: N/A
Wait Wait Start Count 6146 Ticks: 33 (0:00:00.515)
Context Switch Count 877 IdealProcessor: 0
UserTime 00:00:00.468
KernelTime 00:00:00.156
Win32 Start Address 0x00007ff6ac3cb3c0
Stack Init fffff8f1ae85fc9 Current fffff8f1ae85f980
Base fffff8f1ae8600000 Limit fffff8f1ae85a500 Call 0000000000000000
Priority 8 BasePriority 8 PriorityDegree 0 IOPriority 2 PagePriority 5
Scheduling Group: fffff28c0e97a40 KSCB: fffff28c0e97c68

- 4. Enter the dt command to view the scheduling group:

```
ld dt nt_kscheduling_group fffff28c0e97a40
+0000 Policy : _KSCHEDULING_GROUP_POLICY
+0008 RelativeWeight : 0x80
+00c0 ChildMinWeight : 0x2710
+0010 ChildWeight : 0
+0014 ChildTotalWeight : 0
+0038 QueryTimeStamp : Ofed61277
+0020 NotificationCycles : 00
+0030 MaxQuotaCyclesRemaining : 0-7321538269
+0038 SchedulingGrouplist : _LIST_ENTRY [ xffff80085179b110 - fffff28c081b7078 ]
+0038 Sibling : _LIST_ENTRY [ xffff80085179b110 fffff28c081b7078 ]
+0048 NotificationDpc : 0x0002eae8000008e_KDPC
+0050 ChildList : _LIST_ENTRY [ xffff28c062a7ab8 - fffff28c085c08ab ]
+0060 Parent : [null]
+0060 Processor : [1]_KSCB
```

- 5. Create another local user on the machine.
- 6. Run CPU Stress in the current session.
- 7. Make a few threads at maximum activity, but not enough to overwhelm the maximum capacity on. For example, the following image shows two threads running at maximum activity on a three-processor virtual machine:

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_307_0.png)

- 8. Press Ctrl+Alt+Del and select Switch User. Then select and log in to the account for the other user you created.
- 9. Run CPU Stress again, making the same number of threads run with maximum activity.
- 10. For the CPUStress process, open the Process menu, choose Priority Class, and select High to change the process priority class. Without DFSS, higher-priority process should consume most of the CPU because there are four threads competing for three processors. One of these will lose out, and it should be from the lower-priority process.
- 11. Open Process Explorer, double-click both CPUStress processes, and select Performance Graph.
- 12. Place both windows side by side. You should see CPU consumed roughly between the processes even though their priorities are not the same:

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_308_0.png)

- 13. Disable DFSS by removing the registry keys. Then restart the system.
- 14. Run the experiment. You should clearly see the difference with the higher-priority process receiving the most CPU.

## CPU rate limits

DFSS works by automatically placing new threads inside a scheduling group which is fine for terminal scenario, but not good enough as general mechanism to limit the CPU time of threads. The infrastructure can be used in more granular fashion by using job object. Recall from Chapter 3 that job can manage one or more processes. One of the limitations you place on job is CPU rate, which you can do by calling SetInformationJobObjectRateInformation as type of JOBJECT_CPU_RATE_INFORMATION containing the actual control data. You may apply one of three settings to limit CPU time:

- CPU rate value can be between 0 and 100 and represents percent multiplied by 100 (for example, for 40 percent).
- Weight-based value can be between 1 and 9, relative to the weight of other jobs.
- Minimum and maximum rates are specified similarly to the first option (600 ms by default), they cannot get any CPU time until the next interval. You can use control flag to enforce the limit even if there is spare time available. The result of setting these limits is to place all threads from a new scheduling group.

## EXPERIMENT: CPU rate limit

In this experiment, you'll look at CPU rate using job object. It's best to perform this experiment on a virtual machine rather than using the local kernel because of debugger writing.

- 1. Run CPU Stress on the test VM and activate four threads on eight-processor system to consume over 50 percent of CPU time.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_309_0.png)

- 2. Open Process Explorer, find CPUStress instance, open its properties, and select Performance Graph. The CPU usage should be roughly 50 percent.
- 3. Download the CPU LIMIT tool from resources. This is a simple tool that limits the CPU usage of a single process through hard capping.
- 4. Run the command to limit the CPU usage to 20 percent for the CPUStress process (Replace the number 6324 with your process ID). CpuLimit.exe 6324.
- 5. Look at the Process Explorer window. You should see the drop to around 20 percent:

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_309_1.png)

- 6. Open Winbg on the host system.
- 7. Attach to the kernel of the test system and break into it.
- 8. Enter the following command to locate the CPUStress process:
0: kd: !process 0 cpustres.exe
PROCESS fffff9e062928080
SessionId: 1 Cid: 1b Peb: 009e4000 ParentId: 1c4
DiBase: 23080300 ObjectTable: fffff78d1afc540 HandleCount: <Data
NotAccessible>
Image: CPUST.exe

- 9. Type the following command to list basic information for the process:
0: kd: !process fffff9e062952800 1
PROCESS fffff9e06295280
SessionId: 1 Cid: 1b Peb: 009e4000 ParentId: 1c4
DiBase: 23080300 ObjectTable: fffff78d1afc540 HandleCount: <Data
NotAccessible>
Image: CPUST.exe
VadRoot fffff9e0626582010 Vads 88 Clone 0 Private 450 Modified 4 Locked 0.
DeviceMap fffff78dc8cd941640 fffff78cfe3db050
Token
ElapsedTime 00:08:38.438
UserTime 00:00:00.00
KernelTime 00:00:00.00
QuotaUsage[PagedPool] 209912
QuotaUsage[NonPagedPool] 11880
Working Set Sizes (now,min,max) (C50, 345) (13184KB, 200KB, 13880KB)
PeakWorkingSetSize 3325
VirtualSize 108 Mb
PeakVirtualCount 128 Mb
PageFaultCount 3670
MemoryPriority BACKGROUND
BasePriority 8
CommitCharge 568
Job fffff9e06286539a0

- 10. Notice there is a non-NULL job object. Show its properties with the !job command. The tool creates a job (CreateJobObject), adds the process to the job (AssignProcessToJobObject), and calls SetInformationJobObject with the CPU rate information and rate value of 2000 (20 percent).

```
0: kd: !job fffff9e06286539a0
Job at fffff9e06286539a0
Basic Accounting Information
TotalUserTime: 0x0
TotalKernelTime: 0x0
TotalCycleTime: 0x0
ThisPeriodTotalUserTime: 0x0
ThisPeriodKernelTime: 0x0
```
