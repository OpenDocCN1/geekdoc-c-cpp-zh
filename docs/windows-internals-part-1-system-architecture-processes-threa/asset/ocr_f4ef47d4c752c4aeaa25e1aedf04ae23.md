# TABLE 6-13 System power-state definitions

| State | Power Consumption | Software Resumption | Hardware Latency |
|---|---|---|--|
| S0 (fully on) | Maximum | Not applicable | None |
| S1 (sleeping) | Less than S0, more than S2 | System resumes where it left off (returns to S2) | Less than 2 seconds |
 S2 (sleeping) | Less than S1, more than S3 | System resumes where it left off (returns to S0) | 2 or more seconds |
| S3 (sleeping) | Less than S2; processor is off | System resumes where it left off (returns to S0) | Same as S2 |
| S4 (hibernating) | Trickle current to power button and wake circuitry | System restarts from saved hibernation file and resumes where it left off hibernation (returns to S0) | Long and undefined |
| S5 (fully off) | Trickle current to power button | System boot | Long and undefined |

As noted in Table 6-13, states S1 through S4 are sleeping states, in which the system appears to be off because of reduced power. However, these systems retain enough information—either in memory or on disk—to move to S0. For states S1 through S3, power is required to preserve the contents of the computer memory so that when the transition is made to S0 (when the user or a device wakes up the computer), the power continues executing where it left off the suspend.

When the system moves to S4, the power manager saves the compressed contents of memory to a hibernation file Hyperfil.sys, which is large enough to hold the uncompressed contents of memory, in the root directory of the system volume (hidden file). (Compression is used to minimize I/O and to improve hibernation and resume-from-hibernation performance.) After it finishes switching, the power manager shuts off the computer. When a user subsequently turns on the computer, a normal boot process occurs, except that the boot manager checks for and detects a valid memory image stored in the hibernation file. If the hibernation file contains the saved state, the boot manager launches %SystemRoot%System32\Windows.exe, which reads the contents of the file, and resumes execution at the point which is recorded in the hibernation file.

On systems with hybrid sleep enabled, an user request to put the computer to sleep will actually be a combination of both the S3 state and the S4 state. While the computer is put to sleep, an emergency hibernation file will also be written to disk. Unlike typical hibernation files, which contain almost all active memory, the emergency hibernation file includes only data that could not be paged in time, making the suspend operation faster than a typical hibernation (because less data is written to disk). Drivers will be notified that an S4 transition is occurring, allowing them to configure themselves and save state just as an actual hibernation request had been initiated. After this point, the system is put in the normal sleep state just like a standard sleep transition. However, if the power goes out, the system is essentially in an S4 state—the user can power on the machine, and Windows will resume from the emergency hibernation file.

> **Note** You can disable hibernation completely and gain some disk space by running power-cfg /h off from an elevated command prompt.