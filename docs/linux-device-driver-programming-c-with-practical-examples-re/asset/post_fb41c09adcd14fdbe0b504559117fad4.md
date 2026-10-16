
## Kernel Log (dmesg)

The kernel log stores messages printed by printk and other kernel components.

Bash
dmesg

- **Advantages:** Provides a record of system events.
- **Disadvantages:** Can be overwhelming, especially in production environments.

## Kernel Panic

A kernel panic indicates a critical system failure. It often provides a stack trace, which can be helpful for debugging.

Kernel panic - not syncing: Attempted to kill init!

- **Advantages:** Provides detailed information about the system state before the crash.
- **Disadvantages:** Can be difficult to reproduce and analyze.

## Advanced Debugging Techniques

### Kernel Debugging with KGDB

KGDB allows you to debug a running kernel using a debugger like GDB.

Bash
gdb vmlinux /dev/kmsg

- **Advantages:** Provides interactive debugging capabilities, including setting breakpoints, examining variables, and stepping through code.
- **Disadvantages:** Requires special hardware or kernel configuration.

### Kernel Trace (Ftrace)

Ftrace is a powerful tool for tracing kernel function calls.

Bash
echo function_graph > /sys/kernel/debug/tracing/events/function_graph/enable

**Advantages:** Provides detailed information about function calls, arguments, and return values.

- **Disadvantages:** Can generate large amounts of data.

## Memory Debugging

- **kmemleak:** Detects memory leaks in the kernel.

Bash
kmemleak

- **slabtop:** Monitors slab allocator usage.

Bash
slabtop

- **valgrind:** (for user-space components) Detects memory errors like leaks and invalid memory accesses.

Bash
valgrind --leak-check=full my_user_space_program

## Other Tools

- **perf:** Measures performance and identifies bottlenecks.
- **strace:** Traces system calls made by a process (for user-space components).
- **gdb:** (for user-space components) Debugs user-space applications.

## Debugging Tips

- **Reproducibility:** Try to create reproducible test cases.
- **Isolation:** Isolate the problem to a specific code section.
- **Logging:** Use printk judiciously to log relevant information.
- **Kernel Configuration:** Enable debugging options in the kernel configuration.
- **Symbol Information:** Ensure proper symbol information is available for debugging tools.
- **Code Review:** Peer review can help identify potential issues early on.

## Example: Debugging a Device Driver Crash

```
C++
static int my_device_open(struct inode inode, struct file file) // device open logic
    if (error)
        printk(KERN_ERR "Error opening device: %d\n", error); return -
ENODEV;
    }
    return 0;
```

If the driver crashes during the my_device_open function, you can:

- 1. **Check the kernel log** for error messages using dmesg.
- 2. **Use printk** to add more debugging information before the crash.
- 3. **Enable kernel debugging** with KGDB for interactive debugging.
- 4. **Analyze the kernel panic** for clues about the crash location.
- 5. **Check for memory leaks** using kmemleak.

Debugging Linux device drivers requires a systematic approach and a combination of tools. By understanding the available techniques and applying them effectively, you can efficiently identify and fix issues, improving driver reliability and performance.

## Chapter 13

## Kernel Debugging with Printk

### Understanding Printk

Printk is the primary debugging tool for kernel developers. It's akin to printf in user space, but with some key differences tailored for the kernel environment. Printk messages are typically directed to the kernel log, accessible through dmesg.

```
Basic Printk Usage
C++
#include <linux/kernel.h>

void my_function(int arg) {
    printk(KERN_INFO "My function called with arg: %d\n", arg);
}
```

- KERN_INFO is a log level. There are several others like KERN_ERR (error), KERN_WARNING, KERN_DEBUG, etc.
- The format string and arguments work similarly to printf.
- \n is used for newline.

### Log Levels

Printk messages are categorised by log levels. The kernel only prints messages at or above the configured log level.

```
```cpp
printk(KERN_EMERG "System unusable");
printk(KERN_ALERT "Immediate action needed");
printk(KERN_CRIT "Critical conditions");
printk(KERN_ERR "Error conditions");
printk(KERN_WARNING "Warning conditions");
printk(KERN_NOTICE "Normal but significant condition");
printk(KERN_INFO "Informational message");
printk(KERN_DEBUG "Debug-level message");
```
```

### Conditional Printk

To avoid excessive logging, you can use conditional printk based on compile-time or runtime conditions.

```
```cpp
#ifdef DEBUG
printk(KERN_DEBUG "Debug message: %d\n", value); #endif
```
```

### Printk and Device Drivers

Printk is invaluable in device driver development. It can help diagnose issues related to device initialization, data transfer, and error handling.

```
```cpp
static int my_device_open(struct inode *inode, struct file *file) {
    printk(KERN_INFO "my_device_open called\n");
    // ... device open logic ...
    return 0;
}

static int my_device_read(struct file *file, char *buf, size_t count, loff_t *offset) {
    printk(KERN_INFO "my_device_read called, count: %zu\n", count);
    // ... device read logic ...
    return bytes_read;
}
```
```

## Example: Debugging a Device Driver Issue

Consider a device driver that's experiencing random hangs.

- 1. **Increase log verbosity:** Add printk statements at key points in the driver's execution, especially around potential hang areas.
- 2. **Analyze log messages:** Look for patterns or inconsistencies in the log.
- 3. **Use conditional printk:** If the issue is intermittent, use conditional printk based on specific conditions.
- 4. **Experiment with log levels:** Adjust the log level to balance debugging information with system performance.

By following these steps and effectively using printk, you can gain valuable insights into the behavior of your device driver and identify the root cause of issues.

**Remember:** While printk is an essential tool, it's often used in conjunction with other debugging techniques for a comprehensive approach.

## Using Kernel Debuggers (kgdb, kdb)

Kernel debugging is an indispensable skill for Linux device driver developers. While printk is invaluable, it often falls short when dealing with complex issues. Kernel debuggers like kgdb and kdb provide deeper insights into the kernel's behavior, enabling effective troubleshooting.

### Understanding kgdb and kdb

- **kgdb:** A user-space debugger that interacts with a kernel-resident debugging stub. It provides source-level debugging capabilities, allowing you to set breakpoints, inspect variables, and step through code.
- **kdb:** A simpler, text-based command-line interface embedded within the kernel. It offers basic debugging functionalities like inspecting memory, registers, and process information.

## Setting Up a Debugging Environment

To use kgdb or kdb, you'll need:

- A target machine with the kernel configured for debugging.
- A host machine with the necessary debugging tools installed.
- A serial console or network connection between the target and host.

### Kernel Configuration:

```
CONFIG_DEBUG_KERNEL=y
CONFIG_KGDB=y
```

### Host Machine Setup:

Bash

```
sudo apt install gdb
```

## Using kgdb

kgdb leverages the power of GDB for kernel debugging.

### Attaching to the Kernel:

Bash

```
gdb vmlinux /dev/ttyS0 # Replace /dev/ttyS0 with your serial port
```

Basic Commands:

```
break my_device_open # Set a breakpoint at the function
continue # Resume kernel execution
step # Step into the next function
print variable # Print the value of a variable
backtrace # Print the call stack
```

## Example:

```
C++
static int my_device_open(struct inode *inode, struct file *file) {
    printk(KERN_INFO "my_device_open called\n");
    /* ... device open logic ... */
    return 0;
}
```

To debug `my_device_open`:

- 1. Set a breakpoint in GDB: `break my_device_open`
- 2. Continue kernel execution: `continue`
- 3. When the breakpoint is hit, inspect variables and step through code.

## Using kdb

kdb offers a more limited but often sufficient debugging experience directly on the target machine.

**Accessing kdb:** Typically, you'll need to trigger a kernel panic or use a specific key combination to enter kdb. The exact method depends on your system configuration.

### Basic Commands:

```
pc # Print program counter
backtrace # Print call stack
examine /x $sp # Examine memory at the stack pointer
```

## Advanced Debugging Techniques

- **Core Dumps:** Generate core dumps for post-mortem analysis.
- **Watchpoints:** Set breakpoints on memory locations.
- **Single Stepping:** Execute code one instruction at a time.
- **Disassembly:** View the assembly code of a function.

## Challenges and Considerations
