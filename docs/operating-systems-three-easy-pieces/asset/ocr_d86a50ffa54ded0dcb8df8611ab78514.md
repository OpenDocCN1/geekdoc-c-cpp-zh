# 19.5 TLB Issue: Context Switches

With TLBs, some new issues arise when switching between processes (and address spaces). Specifically, the TLB contains virtual-to-physical translations that are only valid for the currently running process; these translations are not meaningful for other processes. As a result, when switching from one process to another, the hardware OS (or both) must be careful that the about-to-be-run process does not accidentally use translations from some previous run.

To understand this situation better, let's look at an example. When one process (P1) is running, it assumes the TLB might caching translations that are valid for it, i.e., that from its 10th page P1 is mapped to physical frame 100.

In the example, assume another process (P2), and the OS might decide to perform a context switch and run it. Assume that the 10th virtual page of P2 is mapped to physical frame 170. If entries for both processes were in the TLB, the contents of the TLB would be:

| VPN | PFN | prot |
| --- | --- | --- |
| 10 | 100 | 1 |
| 10 | 170 | 1 | rwx |

In the TLB above, we clearly have a problem: VPN 10 translates to either PFN 100 (P1) or PFN 170 (P2), but the hardware cannot distinguish which entry is for which process. Thus, we need to do some work in order for the TLB to correctly and efficiently support virtualization across multiple processes. And thus, a crux:

> THE CRUX:
To Manage TLB Contents On A Context Switch
When context-switching between processes, the translations in the TLB for the last process are not meaningful to the about-to-be-run process. What should the hardware or OS do to solve this problem?

There are a number of possible solutions to this problem. One approach is to flush the TLB on context switch, emptying it before the new process runs. On a software-based system, this can be accomplished with an explicit (and privileged) hardware instruction; with hardware-managed TLB, the flush could be enacted when the page-table base register is changed (the OS must change on a context switch anyway). In either case, the flush operation sets all valid bits to 0, essentially clearing the contents of the TLB.

By flushing the TLB on each context switch, we now have a working solution, as a process will never accidentally encounter the wrong trans-