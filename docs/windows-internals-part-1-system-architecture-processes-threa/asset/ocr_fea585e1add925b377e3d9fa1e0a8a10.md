# TABLE 4-4 Scheduling categories

| Category | Priority | Description |
| --- | --- | --- |
| High | 23–26 | Audio threads running at a higher priority than any other thread on the system except for critical system threads |
| Medium | 16–22 | The threads of a foreground application such as Windows Media Player |
| Low | 8–15 | All other threads that are not part of the previous categories |
| Exhausted | 4–6 | Threads that have exhausted their share of the CPU and continue running if no lower-priority threads are ready to run |

The main mechanism MMCS boosts the priority of threads inside a registered process to the priority level matching its scheduling category and relative priority within this category for a guaranteed period. It lowers then threads to the exhausted category so that other, non-multimedia threads on the system can also get to execute.

By default, multimedia receives 80 percent of the CPU time available, while other threads receive 20 percent. (Based on a sample of 10 ms, that would be 8 ms and 2 ms, respectively.) You can change this percentage by modifying the SystemResponsiveness value under the HKLM\SOFTWARE\Microsoft\Windows\Multimedia\SystemProfile key. The value can range from 10 to 100 percent (20 is the default; setting a value lower than 10 evaluates to 0), which changes the CPU percentage guaranteed to the system (not the registered audio apps). MMCS scheduling thread runs around priority 27 because they cannot prevent any Pro Audio threads to lower their priority to the exhausted category.

As discussed, changing the relative priority within a Process does not usually make sense, and no tools allow this because only developers understand the importance of the various threads in their programs. On the other hand, because applications must manually register with MMCS and provide it with information about what kind of thread this is, MMCS has the necessary data to change these relative priorities—and developers are well aware that this will happen.

# EXPERIMENT: MMCS priority boosting

In this experiment, you will see the effects of MMCS priority boosting.

+   1. Run Windows Media Player (wmplayer.exe). (Other playback programs might not take advantage of the API calls required to register with MMCS).
2. Play some audio content.
3. Using Task Manager or Process Explorer, the affinity of the Wplayer.exe process so that it runs on only one CPU.
4. Start the Performance Monitor tool.
5. Using Task Manager, change Performance Monitor’s priority class to Realtime so it will have a better chance of recording activity.