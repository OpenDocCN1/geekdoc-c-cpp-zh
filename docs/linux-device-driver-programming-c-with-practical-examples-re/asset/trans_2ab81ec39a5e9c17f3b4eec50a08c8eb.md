

```c
C
long my_ioctl(struct file *filp, unsigned int cmd, unsigned long arg) {
  // Handle different ioctl commands based on cmd
  switch (cmd) {
  case MY_IOCTL_GET_VALUE:
    // Copy value to user space
    break;
  case MY_IOCTL_SET_VALUE:
    // Copy value from user space
    break;
  default:
    return -EINVAL; // Invalid ioctl command
  }
  return 0; // Success
}
```

## 其他注意事项

- **错误处理：** 在设备驱动中，正确的错误处理至关重要。
- 返回适当的错误代码以指示失败。
- **并发性：** 如果多个进程可以同时访问设备，您可能需要实现锁定机制来保护共享数据。
- **性能：** 优化数据传输并避免不必要的系统调用以提高性能。
- **安全性：** 注意安全影响，尤其是在处理敏感数据时。

示例
```c
struct file_operations my_fops = {
    .owner = THIS_MODULE,
    .open = my_open,
    .release = my_release,
    .read = my_read,
    .write = my_write,
    .ioctl = my_ioctl,
};
```

注意：这是一个简化的示例。实际设备驱动程序通常涉及更复杂的逻辑和错误处理。

通过理解和实现这些核心文件操作，您可以创建能够有效与用户空间交互的基本设备驱动程序。

## Linux 设备驱动程序中的设备注册与注销

在用户空间应用程序可以访问设备之前，它需要在内核中注册。此过程涉及在系统设备表中创建设备条目，并将其与设备驱动程序的文件操作相关联。当不再需要该设备时，必须将其注销以释放系统资源。

## 字符设备的注册与注销

字符设备用于以字节流方式传输数据的设备。

### 注册

```c
#include <linux/fs.h>
#include <linux/init.h>
#include <linux/module.h>

static int my_major = 0;
static struct file_operations my_fops = {
    // ... file operations ...
};

static int __init my_device_init(void) {
    int ret;

    // Allocate a major number dynamically
    ret = alloc_chrdev_region(&my_major, 0, 1, "my_device");
    if (ret < 0) {
        printk(KERN_ERR "Failed to register character device\n");
        return ret;
    }

    // Create a cdev structure
    struct cdev *my_cdev = cdev_alloc();
    if (!my_cdev) {
        printk(KERN_ERR "Failed to allocate cdev\n");
        goto unregister_chrdev;
    }

    // Initialize cdev
    cdev_init(my_cdev, &my_fops);
    my_cdev->owner = THIS_MODULE;

    // Add cdev to the system
    ret = cdev_add(my_cdev, MKDEV(my_major, 0), 1);
    if (ret < 0) {
        printk(KERN_ERR "Failed to add cdev\n");
        goto unregister_cdev;
    }

    // ... other initialization ...

    return 0;

unregister_cdev:
    cdev_del(my_cdev);
unregister_chrdev:
    unregister_chrdev_region(my_major, 1);
    return ret;
}
```

- alloc_chrdev_region 为设备分配主设备号并注册设备名称。
- cdev_alloc 分配一个 cdev 结构体。
- cdev_init 使用文件操作初始化 cdev 结构体。
- cdev_add 将 cdev 添加到系统中。

### 注销

```c
static void __exit my_device_exit(void) {
    // Get the cdev structure
    struct cdev *my_cdev = cdev_get(MKDEV(my_major, 0));

    // Delete the cdev
    cdev_del(my_cdev);

    // Unregister the character device
    unregister_chrdev_region(my_major, 1);
}
```

- cdev_get 检索 cdev 结构体。
- cdev_del 删除 cdev。
- unregister_chrdev_region 注销字符设备。

## 块设备的注册与注销

块设备用于以固定大小块传输数据的设备。

### 注册

```c
#include <linux/blkdev.h>

static int my_major = 0;
static struct block_device_operations my_bdev_ops = {
	// ... block device operations ...
};

static int __init my_device_init(void) {
	int ret;

	// Allocate a major number dynamically
	ret = register_blkdev(my_major, "my_block_device");
	if (ret < 0) {
		printk(KERN_ERR "Failed to register block device\n");
		return ret;
	}

	// ... other initialization ...
	return 0;
}
```

register_blkdev 使用指定的主设备号和设备名称注册块设备。

### 注销

```c
static void __exit my_device_exit(void) {
	unregister_blkdev(my_major, "my_block_device");
}
```

unregister_blkdev 注销块设备。

## 重要注意事项

- **错误处理：** 始终检查注册和注销函数的返回值以发现错误。
- **模块生命周期：** 确保设备注册和注销发生在模块的初始化和清理函数（__init 和 __exit）中。
- **设备命名：** 选择适当的设备名称以便于识别。
- **主设备号分配：** 谨慎管理主设备号分配以避免冲突。
- **设备结构：** 创建适当的数据结构来存储设备特定信息。
- **清理：** 在注销期间释放所有已分配的资源。

## 补充说明

- 对于更复杂的设备，您可能需要使用平台驱动程序或其他设备模型。
- 某些设备可能需要额外的注册步骤，例如设备树绑定或特定于总线的注册机制。
- 正确的错误处理和资源管理对于可靠的设备驱动程序至关重要。

通过理解这些概念并遵循最佳实践，您可以在 Linux 设备驱动程序中有效地注册和注销设备。

## 第 7 章

## Linux 设备驱动程序编程中的 Poll 与 Fasync 机制

在 Linux 设备驱动程序编程中，高效处理异步事件至关重要。实现这一目标的两种主要机制是 poll 和 fasync。这些系统调用允许用户空间进程高效地等待文件描述符上的事件，而不会消耗过多的 CPU 资源。

## Poll

poll 系统调用提供了一种用于多路复用输入/输出操作的机制。它允许进程监视多个文件描述符上的事件，如可读、可写或异常。驱动程序负责实现 poll 操作，以通知用户空间数据的可用性或写入数据的可能性。

### 实现

要在设备驱动程序中实现 poll 操作，您需要在文件操作结构中定义一个 poll 函数指针。以下是一个基本示例：

```c
static unsigned int my_device_poll(struct file *file, poll_table *wait) {
    unsigned int mask = 0;

    /* Check device state to determine available events */
    if (device_has_data_to_read()) {
        mask |= POLLIN | POLLRDNORM;
    }
    if (device_can_accept_write()) {
        mask |= POLLOUT | POLLWRNORM;
    }

    /* Add the current process to the wait queue */
    poll_wait(file, &my_device_wait_queue, wait);

    return mask;
}
```

在此示例中，my_device_wait_queue 是与设备关联的等待队列。poll_wait 函数将当前进程添加到等待队列，并返回可用事件掩码。

## Fasync

fasync 机制用于异步通知用户空间进程有关文件描述符上的事件。驱动程序注册一个回调函数，以便在事件发生时调用。

### 实现

要实现 fasync 支持，您需要在文件操作结构中定义一个 fasync 函数指针。以下是一个基本示例：

```c
static int my_device_fasync(int fd, struct file *file, int mode) {
    struct my_device *dev = file->private_data;

    return fasync_helper(fd, file, mode, &dev->async_queue);
}
```

fasync_helper 函数是内核提供的辅助函数，用于管理 fasync 队列。async_queue 是一个 struct fasync_struct 指针，用于跟踪异步通知。

要向用户空间发送通知，可以使用 kill_fasync 函数：
```c
kill_fasync(&dev->async_queue, SIGIO, POLL_IN);
```
这将向所有在文件描述符上注册了异步通知的进程发送 SIGIO 信号。

## 结合 Poll 与 Fasync

在许多情况下，将 poll 和 fasync 结合起来对于高效事件处理非常有用。poll 操作可用于初步检查事件，如果没有待处理事件，则可以将进程添加到等待队列。当事件发生时，驱动程序可以使用 fasync 通知等待的进程。

## 示例

以下是一个更完整的示例，演示了如何在设备驱动程序中同时使用 poll 和 fasync：

