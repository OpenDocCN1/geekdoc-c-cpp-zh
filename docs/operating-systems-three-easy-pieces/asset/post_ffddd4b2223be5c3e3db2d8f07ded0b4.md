
## Why No Memory Is Leaked Once Your Process Exits 697

- Why No Valid Bit, 203
- Why Null Pointer Accesses Cause Seg Faults, 279
- Why Servers Crash, 651
- Why System Calls Look Like Procedure Calls, 57

## Tips

- Always Hold The Lock While Signaling, 373
- Amortization Can Reduce Costs, 78
- Avoid Premature Optimization (Knuth's Law), 366
- Avoid Voooo Constants (Ousterhout's Law), 93
- Be Careful Setting The Timeout Value, 638
- Be Careful With Generalization, 406
- Be Careful With Terminology, 590
- Be Lazy, 282
- Be Wary Of Complexity, 238
- Be Wary Of Locks And Control Flow, 362
- Be Wary Of Commands, 506
- Be Wary Of User Inputs In Systems, 560
- Communication Is Inherently Unreliable, 632
- Comparing Against Optimal 259
- Consider Extent-based Approaches, 525
- Consider Incremental, 286
- Dealing With Application Misbehavior, 62
- Do Work In The Background, 252
- Don't Always Do It Perfectly (West's Law), 421
- Don't Block In Event-based Servers, 429
- Enforce Lock Ordering By Address, 416
- Getting It Right (Lamps' Law), 460
- Hardware-based Dynamic Relocation, 157
- Idempotency Is Powerful, 657
- If 1000 Solutions Exist, No Great Does, 175
- Interposition Is Powerful, 153
- Interrupts Not Always Better Than PIO, 448
- It Depends (Livny's Law), 469
- It Compiled Or Is Correct, 143
- Know And Use Your Tools, 310
- Learn From History, 86
- Less Code Is Better (Lauer's Law), 343
- Make The System Usable, 548
- Measure Then Build (Patterson's Law), 669
- More Concurrency Isn't Necessarily Faster, 359
- Overlap Enables Higher Utilization, 79
- Perfect Is The Enemy Of The Good (Voltaire's Law), 699
- RAM't Always RAM (Culler's Law), 224
- Reboot Is Useful, 64
- Scheduling Must Be Secure From Attack, 90
- Separate Policy And Mechanism, 29
- Setting The Value Of Semaphore, 395
- Simple And Dumb Can Be Better (Hill's Law), 651
- The Importance Of Backwards Compatibility, 594
- The Principle Of Isolation, 134
- The Principle Of SJF, 74
- There's No Free Lunch, 617
- Think About Concurrency As A Malicious, 339
- Think Carefully About Naming, 493
- Transparency Enables Deployment, 474
- Turn Flaws Into Virtues, 585
- Understand Vs. Dynamic Partitioning, 533
- Understand The Durability/Performance Trade-off, 693
- Use Time-Space Trade-offs, 235
- Use strace (And Similar Tools), 495
- A Level Of Indirection, 578
- Use Atomic Operations, 313
- Use Caching When Possible, 481
- Use Checksums For Integrity, 635
- Use Disks Sequentially, 464
- Use Efficient Data Structures When Appropriate, 108
- USE HYBRIDS 701
- Use Hybrids, 233
- Use Protected Control Transfer, 58
- Use Randomness, 98 The Timer Interrupt To Regain Control, 63
- Use Tickets To Represent Shares, 99
- Use Time Sharing (and Space Sharing), 28
- Use While (Not If) For Conditions, 382
- When In Doubt, Try It Out, 141

## THREE EASY PIECES

## Courses

- To Account For Disk Rotation Costs, 468
- To Add Locks To Data Structures, 353
- To Allocate And Manage Memory, 139
- To Avoid Spinning, 344
- To Avoid The Costs Of Polling, 447
- To Build A Complete VM System, 275
- To Build A Device-neutral OS, 450
- To Build A Distributed File System, 650
- To Build A Flash-based SSD, 589
- To Build A Lock, 333
- To Build Concurrent Servers Without Threads, 642
- To Build Correct Programs, 631
- To Build Systems That Work When Components Fail, 631
- To Communicate With Devices, 449
- To Create And Control Processes, 41
- To Create And Control Threads, 319
- To Deal With Deadlock, 414
- To Deal With Load Imbalance, 119
- To Decide Which Page To Evict, 257
- To Define A Stateless File Protocol, 653
- To Design A Scalable File Protocol, 670
- To Design TL Replacement Policy, 223
- To Develop Scheduling Policy, 71
- To Efficiently And Flexibly Virtualize Memory, 151
- To Efficiently Virtualize The CPU With Control, 55
- To Ensure Data Integrity, 613
- To Gain Control Without Cooperation, 62
- To Go Beyond Physical Memory, 245
- To Handle Common Concurrency Bugs, 409
- To Handle Disk Starvation, 467
- To Handle Latent Sector Errors, 615
- To Handle Lost Writes, 621
- To Handle Misdirected Writes, 620
- To Implement A Simple File System, 519
- To Implement An LRU Replacement Policy, 268
- To Integrate I/O Into Systems, 443
- To Manage PIO Overheads, 449
- To Make A Large, Fast, Reliable Disk, 473
- To Make All Writes Sequential, 574
- To Make Tables Smaller, 229
- To Manage A Persistent Device, 491
- To Manage Free Space, 180
- To Manage TLB Contents On Context Switch, 221
- To Organize On-Disk Data To Improve Performance, 538
- To Perform Restricted Operations, 56
- To Preserve Data Integrity Despite Corruption, 616
- To Provide The Illusion Of Many CPUs, 27
- To Reduce File System I/O Costs, 532
- To Regain Control Of The CPU, 661
- To Schedule Jobs On Multiple CPUs, 112
- To Share The CPU Proportionally, 97
- To Schedule Without Perfect Knowledge, 85
- To Speed Up Address Translation, 213
- To Store Data On Disk, 45
- To Support A Large Address Space, 167
- To Update The Disk Crashes, 551
- To Use Semaphores, 389
- To Virtualize Memory, 133
- To Virtualize Memory With Pages, 197
- To Virtualize Resources, 4
- To Wait For A Condition, 370

This book was typeset using the amazing LaTeX typesetting system and the wonderful memoir book-making package. A heartfelt thank you to the legions of programmers who have contributed to this powerful tool over the many years of its development.

All of the graphs and figures in the book were generated using a Python-based version of zplot, a simple and useful tool developed by R. Arpac-Dusseau to generate graphs in PostScript. The zplot arose after many years of frustration with existing graphing tools such as gnuplot (which was limited) and ploticus (which was overly complex though admitted quite awesome). As a result, R. A-D finally put his years of study of PostScript to good use and developed zplot.
