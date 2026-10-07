
# Virtual Address Physical Address

| Virtual Address | Physical Address |
| :--- | :--- |
| 0 | 16 KB |
| 1 KB | 17 KB |
| 3000 | 19384 |
| 4400 | Fault (out of bounds) |

As you can see from the example, it is easy for you to add the base address to the virtual address (which can be viewed as an offset into the address space) to get the resulting physical address. Only if the virtual address is “too big” or negative the result will be a fault, causing an exception to be raised.

# 15.4 Hardware Support: A Summary

Let us now summarize the what we need from the hardware (also see Figure 15.3, page 159). First, as discussed in the chapter on CPU virtualization, we require two different modes. The OS runs in **privileged mode (or kernel mode)**, where it has access to the entire machine; applications run in **user mode**, where they are limited in what they can do. A single bit, perhaps stored in some other kind of exception or interrupt, indicates which mode the CPU is currently running (**status word**; in certain special occasions (t.g., a system call or some other kind of exception or interrupt), the CPU switches between modes.

The hardware must also provide the **base and bounds registers** themselves; each CPU has an additional memory management unit (MMU) of the CPU. When a user program is running, the hardware will translate each address, by adding the base value to the virtual address by the user program. The hardware must also be able to check whether the address is valid, which is accomplished by using the bounds register and some circuitry within the CPU.

The hardware should provide special instructions to modify the base and bounds registers, allowing the OS to change when different processes run. These instructions are **privileged**; only in kernel (or privileged) mode can the registers be modified. Imagine the havoc a user could wreak¹ if they change the base register while running.

> ¹Is anything other than “havoc” that can be “wreaked?” [W17]

ASIDE: Data Structure — The Free List
The OS must track parts of free memory are not in use, so as to be able to allocate memory to processes. Many different data structures can be used for such a task; the simplest (which we will assume here) is a **free list**, which is simply a list of the physical memory which are not currently in use.

# MECHANISM: ADDRESS TRANSLATION 159

| Hardware Requirements | Notes |
| --- | --- |
| Privileged mode | Needed to prevent user-mode processes from executing privileged operations |
| Base/bounds registers | Need pair of registers per CPU to support address translation and bounds checks |
| Ability to translate virtual addresses and check if within bounds | Circuitry to translations and check limits; in this case, quite simple |
| Privileged instruction(s) to update base/bounds | OS must be able to set these values before letting a user program run OS able to tell hardware code to run if exception occurs |
| Privileged instruction(s) to register exception handlers | When processes try to access privileged instructions or out-of-bounds memory |
| Ability to raise exceptions | |

Figure 15.3: Dynamic Relocation: Hardware Requirements

Imagine it! And then quickly flush dark thoughts from your mind, as the ghostly stuff of nightmares are made. Finally, the CPU must be able to generate exceptions in situations where a user program tries to access memory illegally (with an address that is “out of bounds”); in this case, the CPU should stop executing the user program and arrange for the “out-of-bounds” exception handler the OS can then figure out how to react, in this case likely terminating the process. Similarly, if a user program tries to change the values of the (privileged) base and bounds registers, the CPU should raise an exception and retry the “tried to execute a privileged operation while in user mode” handler. The CPU must also provide a method to inform it of the location of these handlers; a few more privileged instructions are needed.

# 15.5 Operating System Issues

Just as the hardware provides new features to support dynamic relocation, the OS has new issues it must handle; the combination of hardware support and OS management leads to the implementation of a virtual memory. Specifically, there are few critical junctures where the OS must get involved to implement our base-and-bounds version of virtual memory.

First, the OS must take action when a process is created, finding space for its address space. Fortunately, given our assumptions that each address space is (s) smaller than the size of physical memory and (b) the same size, this is quite easy for the OS; it can simply view physical memory as an array of slots, and track whether each is free or in use. When a new process is created, the OS will have to search a data structure (often called a free list) to find room for the new address space and mark it used. With variable-sized address spaces, life is more complicated, but we will leave that for future chapters.

# MECHANISM: ADDRESS TRANSLATION

| OS Requirements | Notes |
|---|---|
| Memory management | Need to allocate memory for new processes; Reclaim memory from terminated processes; Generally manage memory via free list |
| Base/bounds management | Must set base/bounds properly upon context switch |
| Exception handling | Code to run when exceptions arise; likely the action is to terminate offending process |

Figure 15.4: Dynamic Relocation: Operating System Responsibilities

Let's look at example. In Figure 15.2 (page 155), you can see the OS using the first slot of physical memory for itself, and it has relocated the process from above into the slot translating physical address 32 KB. The other slots are free (16 KB-32 KB and 48 KB-64 KB); the free list should consist of these two entries.

Second, the OS must do work when a process is terminated (i.e., when it exits gracefully, or is forcibly killed when it is misbehaving), reclaiming all of its memory for use in other processes or the OS. Upon termination of a process, the OS puts its memory back on the free list, and cleans up any data structures as needed.

Third, the OS must also perform a few additional steps when a context switch occurs. There is only one base and bounds register pair on running CPU, after all their values differ for each running process, as program is loaded at a different physical address in memory. The OS must save and restore the base-and-bounds pair when it switches between processes. Specifically, when the OS decides to stop running a process, it must save the values of the base and bounds registers to, in some process structure such as the process control block (PCB). Similarly, when the OS resumes a running process (or it the first time), it must set the values of the base and bounds on the CPU to the correct values for this process.

We should note that when a process is stopped (i.e., not running), it is possible for the OS to move an address space from one memory to another rather easily. To move a process's address, the OS first schedules the process; then, the OS copies the address space from the current location to the new location; the OS updates the base register (in the process structure) to the new location. When the process is resumed, its (new) base register is restored, and it begins running again, oblivious that its instructions and data are in a completely new memory.

Fourth, the OS must provide exception handlers, or functions to be called, as discussed above; the OS installs these handlers at boot time (with privileged instructions). For example, if a process tries to access memory outside its bounds, the CPU will raise an exception; the OS must be prepared to take action when such an exception arises. The common reaction of the OS will be one of hostility; it will likely terminate the offending process. The OS should be highly protective of the memory it is running, and it does not think kindly to a process trying to access memory or
