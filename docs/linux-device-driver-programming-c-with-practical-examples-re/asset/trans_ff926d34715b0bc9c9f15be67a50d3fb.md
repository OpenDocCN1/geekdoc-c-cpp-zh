

## 内核日志（dmesg）

内核日志存储由 printk 和其他内核组件打印的消息。

Bash
dmesg

- **优点：** 提供系统事件的记录。
- **缺点：** 可能信息量过大，尤其是在生产环境中。

## 内核崩溃（Kernel Panic）

内核崩溃表示严重的系统故障。它通常会提供堆栈跟踪，这有助于调试。

内核崩溃 - 不同步：尝试终止 init！

- **优点：** 提供崩溃前系统状态的详细信息。
- **缺点：** 难以重现和分析。

## 高级调试技术

### 使用 KGDB 进行内核调试

KGDB 允许你使用 GDB 等调试器调试正在运行的内核。

Bash
gdb vmlinux /dev/kmsg

- **优点：** 提供交互式调试功能，包括设置断点、检查变量和单步执行代码。
- **缺点：** 需要特殊的硬件或内核配置。

### 内核跟踪（Ftrace）

Ftrace 是一个用于跟踪内核函数调用的强大工具。

Bash
echo function_graph > /sys/kernel/debug/tracing/events/function_graph/enable

**优点：** 提供有关函数调用、参数和返回值的详细信息。

- **缺点：** 可能生成大量数据。

## 内存调试

- **kmemleak：** 检测内核中的内存泄漏。

Bash
kmemleak

- **slabtop：** 监视 slab 分配器的使用情况。

Bash
slabtop

- **valgrind：**（用于用户空间组件）检测内存错误，如泄漏和无效内存访问。

Bash
valgrind --leak-check=full my_user_space_program

## 其他工具

- **perf：** 测量性能并识别瓶颈。
- **strace：** 跟踪进程发出的系统调用（用于用户空间组件）。
- **gdb：**（用于用户空间组件）调试用户空间应用程序。

## 调试技巧

- **可重现性：** 尝试创建可重现的测试用例。
- **隔离：** 将问题隔离到特定代码段。
- **日志记录：** 明智地使用 printk 记录相关信息。
- **内核配置：** 在内核配置中启用调试选项。
- **符号信息：** 确保调试工具可以获得正确的符号信息。
- **代码审查：** 同行评审有助于及早发现潜在问题。

## 示例：调试设备驱动程序崩溃

```
C++
static int my_device_open(struct inode inode, struct file file) // 设备打开逻辑
    if (error)
        printk(KERN_ERR "Error opening device: %d\n", error); return -
ENODEV;
    }
    return 0;
```

如果驱动程序在 my_device_open 函数期间崩溃，你可以：

- 1. 使用 dmesg **检查内核日志**中的错误消息。
- 2. 在崩溃前**使用 printk** 添加更多调试信息。
- 3. 使用 **KGDB 启用内核调试** 以进行交互式调试。
- 4. **分析内核崩溃**，寻找崩溃位置的线索。
- 5. 使用 **kmemleak 检查内存泄漏**。

调试 Linux 设备驱动程序需要系统化的方法和工具的组合。通过理解可用的技术并有效应用它们，你可以高效地识别和修复问题，提高驱动程序的可靠性和性能。

## 第 13 章

## 使用 Printk 进行内核调试

### 理解 Printk

Printk 是内核开发人员的主要调试工具。它类似于用户空间中的 printf，但针对内核环境有一些关键区别。Printk 消息通常指向内核日志，可通过 dmesg 访问。

```
Basic Printk Usage
C++
#include <linux/kernel.h>

void my_function(int arg) {
    printk(KERN_INFO "My function called with arg: %d\n", arg);
}
```

- KERN_INFO 是一个日志级别。还有其他几个级别，如 KERN_ERR（错误）、KERN_WARNING（警告）、KERN_DEBUG（调试）等。
- 格式字符串和参数的工作方式与 printf 类似。
- \n 用于换行。

### 日志级别

Printk 消息按日志级别分类。内核只打印达到或超过配置日志级别的消息。

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

### 条件 Printk

为避免过度记录日志，你可以基于编译时或运行时条件使用条件 printk。

```
```cpp
#ifdef DEBUG
printk(KERN_DEBUG "Debug message: %d\n", value); #endif
```
```

### Printk 与设备驱动程序

Printk 在设备驱动程序开发中非常有价值。它可以帮助诊断与设备初始化、数据传输和错误处理相关的问题。

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

## 示例：调试设备驱动程序问题

考虑一个设备驱动程序遇到随机挂起的情况。

- 1. **提高日志详细程度：** 在驱动程序执行的关键位置添加 printk 语句，尤其是可能挂起的区域附近。
- 2. **分析日志消息：** 查找日志中的模式或不一致之处。
- 3. **使用条件 printk：** 如果问题是间歇性的，基于特定条件使用条件 printk。
- 4. **尝试不同的日志级别：** 调整日志级别，以在调试信息和系统性能之间取得平衡。

通过遵循这些步骤并有效使用 printk，你可以深入了解设备驱动程序的行为，并找出问题的根本原因。

**请记住：** 虽然 printk 是必不可少的工具，但通常需要与其他调试技术结合使用，才能形成全面的方法。

## 使用内核调试器（kgdb、kdb）

内核调试是 Linux 设备驱动程序开发人员不可或缺的技能。虽然 printk 非常有用，但在处理复杂问题时往往力不从心。kgdb 和 kdb 等内核调试器可以更深入地了解内核行为，从而进行有效的故障排除。

### 理解 kgdb 和 kdb

- **kgdb：** 一种用户空间调试器，与内核驻留的调试桩交互。它提供源代码级调试功能，允许你设置断点、检查变量和单步执行代码。
- **kdb：** 一个嵌入在内核中的、更简单的基于文本的命令行界面。它提供基本调试功能，如检查内存、寄存器和进程信息。

## 设置调试环境

要使用 kgdb 或 kdb，你需要：

- 一台内核已配置为调试的目标机器。
- 一台安装了必要调试工具的主机。
- 目标机与主机之间的串行控制台或网络连接。

### 内核配置：

```
CONFIG_DEBUG_KERNEL=y
CONFIG_KGDB=y
```

### 主机设置：

Bash

```
sudo apt install gdb
```

## 使用 kgdb

kgdb 利用 GDB 的强大功能进行内核调试。

### 连接到内核：

Bash

```
gdb vmlinux /dev/ttyS0 # 将 /dev/ttyS0 替换为你的串行端口
```

基本命令：

```
break my_device_open # 在函数处设置断点
continue # 继续执行内核
step # 单步进入下一个函数
print variable # 打印变量的值
backtrace # 打印调用栈
```

## 示例：

```
C++
static int my_device_open(struct inode *inode, struct file *file) {
    printk(KERN_INFO "my_device_open called\n");
    /* ... device open logic ... */
    return 0;
}
```

调试 `my_device_open`：

- 1. 在 GDB 中设置断点：`break my_device_open`
- 2. 继续执行内核：`continue`
- 3. 当断点命中时，检查变量并单步执行代码。

## 使用 kdb

kdb 直接在目标机器上提供更有限但通常足够的调试体验。

**访问 kdb：** 通常，你需要触发内核崩溃或使用特定的组合键进入 kdb。具体方法取决于你的系统配置。

### 基本命令：

```
pc # 打印程序计数器
backtrace # 打印调用栈
examine /x $sp # 检查栈指针处的内存
```

## 高级调试技术

- **核心转储：** 生成核心转储用于事后分析。
- **监视点：** 在内存位置设置断点。
- **单步执行：** 一次执行一条指令。
- **反汇编：** 查看函数的汇编代码。

## 挑战与注意事项

