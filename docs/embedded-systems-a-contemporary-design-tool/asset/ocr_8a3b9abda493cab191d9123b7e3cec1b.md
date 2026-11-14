+   - System Protection
+   As discussed earlier, ensuring the protection of data and resources in the context of concurrent processes is an important and essential duty for the operating system. Such a duty is more acute in the context of a von Neumann machine.

+   - Networking
+   In the context of a distributed application, the operating system must also take on the responsibility of managing distributed intra-system communication and the remote scheduling of tasks.

+   - Command Interpretation
+   The operating system in machines such as the familiar desktop computers that directly interact with the user provides the interface to that user’s application. In embedded applications that support provisions for user interaction, the task is implemented via a variety of software drivers supported by the OS that interact with the hardware I/O devices. As commands and directives come into the system, they must be parsed, checked for grammatical accuracy, and directed to the target task.

# 11.9 THE REAL-TIME OPERATING SYSTEM (RTOS)

real-time operating system (RTOS) A RTOS is primarily an operating system. In addition to the responsibilities already enumerated, this special class of operating system ensures (among other things) that (rigid time constraints can be met. The RTOS is commonly found in embedded applications because, as noted, in certain such applications, if such requirements are not met, the performance of the application is inaccurate or compromised in some way. Such systems are often interacting with the physical environment through sensors and various types of measurement devices. RTOS-based applications are frequently used in scientific experiments, control systems, or other applications where missed deadlines cannot be tolerated.

Often, people misuse the term real time to mean that the system responds quickly. Such an interpretation is only partially correct. The key characteristic of an RTOS is deterministic behavior. By this term we mean that given the same state and same set of inputs, the next state (and any associated outputs) will be the same each time the control algorithm utilized by the system is executed.

hard real time, soft real time In earlier discussions, we identified the two extremes in real-time behavior: that which is termed hard real time and that designated soft real time. Behavior that falls into the first category is sufficiently characterized such that system delays are known or, at least, bounded. These systems are said to be operating correctly if they can return results within the specified timing bounds. Behavior classified as soft real time ensures that critical tasks have priority over other tasks and retain that priority until complete. A real-time task cannot be kept waiting indefinitely. We will return to this discussion shortly.

# 11.10 OPERATING SYSTEM ARCHITECTURE

virtual machines Most contemporary operating systems are designed and implemented as a hierarchy of what are called virtual machines, as illustrated in Figure 11.9. Organized like the onion model discussed earlier, the only real machine that the various pieces of functionality within the operating system see is the underlying physical microprocessor; specifically, the OS sees the CPU, the memory, and the concrete I/O devices. The hierarchy is designed such that each layer uses the functions/operations and services of lower layers. The primary advantage of such an approach is increased modularity.