

Example: Handling a Network Interface Interrupt

```c
#include <linux/interrupt.h>
#include <linux/netdevice.h>
#include <linux/etherdevice.h>
#include <linux/skbuff.h>

static DECLARE_TASKLET(netdev_rx_tasklet, netdev_rx_tasklet_handler);

static irqreturn_t netdev_interrupt(int irq, void *dev_id) {
    struct net_device *dev = (struct net_device *)dev_id;

    // Top half: receive packet and save to buffer
    struct sk_buff *skb = ...; // Allocate skb and fill with packet data
    netif_rx(skb); // Pass packet to network stack

    // Schedule bottom half to process received packet
    tasklet_schedule(&netdev_rx_tasklet);

    return IRQ_HANDLED;
}

static void netdev_rx_tasklet_handler(unsigned long data) {
    // Bottom half: process received packet
    // ...
}
```

通过有效使用上半部和下半部处理程序，设备驱动程序可以提高性能和响应能力。上半部快速确认中断并安排下半部进行更复杂的处理，从而使系统能够高效地处理多个中断。

## Interrupt Sharing and Masking in Linux Device Drivers

在许多嵌入式系统中，多个设备共享同一条中断线是很常见的。这通常是由于硬件限制或设计选择造成的。Linux 提供了处理此类场景的机制。

- Key points:
- • Multiple device drivers can register for the same IRQ.
- • The kernel ensures only one ISR runs at a time for a shared IRQ.
- • The dev_id parameter in request_irq is crucial for identifying the correct handler.

## Code example:

```
C
#include <linux/interrupt.h>

static irqreturn_t dev1_interrupt_handler(int irq, void *dev_id) {
    // Handle interrupt for device 1
    return IRQ_HANDLED;
}

static irqreturn_t dev2_interrupt_handler(int irq, void *dev_id) {
    // Handle interrupt for device 2
    return IRQ_HANDLED;
}

static int __init my_module_init(void) {
    request_irq(IRQ_SHARED_IRQ, dev1_interrupt_handler, IRQF_SHARED,
"dev1", &dev1_data);
    request_irq(IRQ_SHARED_IRQ, dev2_interrupt_handler, IRQF_SHARED,
"dev2", &dev2_data);
    return 0;
}
```

## Important considerations:

- - Use unique dev_id values for each driver to differentiate between handlers.
- - Properly handle the case where multiple devices generate interrupts simultaneously.
- - Consider using bottom halves for complex interrupt handling to avoid blocking the ISR.

## Interrupt Masking

中断屏蔽允许驱动程序暂时禁用中断，通常是为了防止重入或与其他操作同步。

## Key points:

- - Use `disable_irq` to disable an interrupt.
- - Use `enable_irq` to re-enable an interrupt.
- - Be careful when disabling interrupts to avoid deadlocks.

```
```c
#include <linux/interrupt.h>

static irqreturn_t my_interrupt_handler(int irq, void *dev_id) {
    // Disable interrupt to prevent re-entry
    disable_irq(irq);

    // Critical section
    // ...

    // Re-enable interrupt
    enable_irq(irq);

    return IRQ_HANDLED;
}
```
```

## Important considerations:

- - Disable interrupts for the shortest possible time.
- - Use nested disabling with care.
- - Consider alternative synchronization mechanisms if possible.

## Interrupt Masking and Sharing Together

中断共享和屏蔽可以结合使用。例如，驱动程序在访问共享资源时可能会禁用中断以防止竞争条件。

## Code example:

```
```c
static irqreturn_t my_interrupt_handler(int irq, void *dev_id) {
	// Disable the shared interrupt to protect shared resources
disable_irq(IRQ_SHARED_IRQ);

	// Access shared resources
	// ...

	// Re-enable the shared interrupt
	enable_irq(IRQ_SHARED_IRQ);

	return IRQ_HANDLED;
}
```

## Additional Considerations

- - Interrupt Priorities: Linux allows assigning priorities to interrupts, which can be useful for handling critical interrupts first.
- - Interrupt Affinity: Bind interrupts to specific CPUs for performance optimization.
- - Interrupt Handling Efficiency: Keep ISRs as short as possible to minimize interrupt latency.
- - Error Handling: Implement proper error handling in interrupt handlers to prevent system crashes.

中断共享和屏蔽是管理 Linux 设备驱动程序中断的重要技术。通过理解这些概念并遵循最佳实践，您可以创建健壮且高效的驱动程序，有效地处理硬件交互。

## Chapter 6

## Character Device Driver API

## Understanding the Limitations: C++ in Linux Kernel Development

在深入代码之前，必须解决一个常见的误解。虽然 C++ 是一种强大的语言，但其在 Linux 内核开发中的使用是有限的。内核主要用 C 编写，原因在于效率、可移植性和稳定性。C++ 的特性如异常、虚函数和模板会引入内核环境中不希望出现的复杂性。

然而，我们仍然可以在内核中使用类似 C 的语法，这就是本回复的重点。

## Character Device Driver API: A Brief Overview

字符设备是内核与用户空间之间基本接口的一种。它们通常用于处理数据顺序的设备，例如串口、键盘和鼠标。Linux 中字符设备的核心 API 围绕内核提供的一组函数展开：

- - **register_chrdev:** 向内核注册字符设备，为其分配主设备号和次设备号。
- - **unregister_chrdev:** 注销字符设备。
- - **alloc_chrdev_region:** 为字符设备分配一组次设备号。
- - **release_chrdev_region:** 释放一组次设备号。
- - **cdev_init:** 初始化字符设备的 cdev 结构。
- - **cdev_add:** 将 cdev 结构添加到内核的字符设备列表中。
- - **cdev_del:** 从内核的字符设备列表中移除 cdev 结构。

## Basic Character Device Driver Structure

```
C

static int my_device_open(struct inode *inode, struct file *filp) {
    // Device open logic
    return 0; // Success
}

static ssize_t my_device_read(struct file *filp, char __user *buf, size_t count, loff_t *offset) {
    // Device read logic
    return 0; // Number of bytes read
}

static ssize_t my_device_write(struct file *filp, const char __user *buf, size_t count, loff_t *offset) {
    // Device write logic
    return 0; // Number of bytes written
}

static int my_device_release(struct inode *inode, struct file *filp) {
    // Device close logic
    return 0;
}
```

Define file operations structure:

```
C

static const struct file_operations my_device_fops = {
    .owner = THIS_MODULE,
    .open = my_device_open,
    .read = my_device_read,
    .write = my_device_write,
    .release = my_device_release,
    // ... other file operations
};
```

● Register the character device:

```
C

static int __init my_device_init(void) {
    // Allocate major and minor numbers
    alloc_chrdev_region(&dev_num, 0, 1, "my_device");

    // Initialize cdev structure
    cdev_init(&my_cdev, &my_device_fops);

    // Add cdev to the kernel's list
    cdev_add(&my_cdev, dev_num, 1);

    // Create device node
    device_create(my_class, NULL, MKDEV(MAJOR(dev_num), 0), NULL, "my_device");

    return 0;
}
```

● Unregister the character device:

```
static void __exit my_device_exit(void) {
	// Remove device node
	device_destroy(my_class, MKDEV(MAJOR(dev_num), 0));
	// Remove cdev from the kernel's list
	cdev_del(&my_cdev);
	// Release major and minor numbers
	unregister_chrdev_region(dev_num, 1);
}
```

## Module initialization and cleanup:

```
module_init(my_device_init);
module_exit(my_device_exit);
MODULE_LICENSE("GPL ");
```

## Key Points and Considerations

- - Replace placeholders like my_device with appropriate names for your device.
- - Implement the device-specific logic within the open, read, write, and close functions.
- - Handle error conditions gracefully, returning appropriate error codes.
- - Consider using other file operations like ioctl for device control.
- - For complex devices, you might need to create additional file operations or use character device classes.
- - Always follow kernel coding style guidelines.

