

## 设备空闲

设备空闲允许设备在未主动使用时进入低功耗状态。内核提供了一个用于管理设备空闲状态的框架。

```
C
struct dev_pm_ops my_device_pm_ops = {
    .prepare = my_device_prepare,
    .complete = my_device_complete,
    .suspend = my_device_suspend,
    .resume = my_device_resume,
    .idle = my_device_idle,
};
```

- **my_device_prepare:** 在设备进入空闲状态之前调用。
- **my_device_complete:** 在设备退出空闲状态之后调用。
- **my_device_idle:** 实际的空闲函数。

```
C
static int my_device_idle(struct device *dev) {
    struct my_device *my_dev = dev_get_drvdata(dev);

    // Prepare the device for idle state
    prepare_device_for_idle(my_dev);

    // Enter idle state
    device_idle(dev);

    // Restore device state after idle
    restore_device_from_idle(my_dev);

    return 0;
}
```

## 挂起与恢复

挂起和恢复用于更深的省电状态。设备驱动必须实现挂起和恢复函数以保存和恢复设备状态。

```
C
static int my_device_suspend(struct device *dev) {
    struct my_device *my_dev = dev_get_drvdata(dev);

    // Save device state
    save_device_state(my_dev);

    // Disable interrupts
    disable_device_interrupts(my_dev);

    // Put device into low-power state
    put_device_to_sleep(my_dev);

    return 0;
}

static int my_device_resume(struct device *dev) {
    struct my_device *my_dev = dev_get_drvdata(dev);

    // Restore device state
    restore_device_state(my_dev);

    // Enable interrupts
    enable_device_interrupts(my_dev);

    // Bring device back to full operation
    wake_up_device(my_dev);

    return 0;
}
```

为了实现最佳的省电效果，驱动程序可以实现具有不同功耗水平的电源状态。然后驱动程序可以根据设备的负载和系统条件选择适当的电源状态。

```
C
enum my_device_power_state {
    ACTIVE,
    IDLE,
    SUSPEND
};

static int my_device_set_power_state(struct my_device *my_dev, enum my_device_power_state state) {
    switch (state) {
        case ACTIVE:
            // Bring device to full power
            break;
        case IDLE:
            // Enter idle state
            break;
        case SUSPEND:
            // Suspend the device
            break;
        default:
            return -EINVAL;
    }

    return 0;
}
```

## 其他考虑

- **唤醒源：** 一些设备可以使系统从低功耗状态唤醒。驱动程序可以使用
device_set_wakeup_capable 和 device_set_wakeup_enable 注册唤醒源。
- **PM 运行时：** 为频繁访问的设备提供更精细的电源管理。
- **时钟管理：** 将电源管理与时钟频率缩放协调。
- **错误处理：** 为挂起、恢复和空闲操作实现适当的错误处理。

有效的低功耗模式实现可以显著提高电池寿命和整体系统性能。通过理解核心概念并利用可用的电源管理框架，设备驱动程序可以有助于优化功耗。

## Linux 设备驱动程序中的唤醒源

唤醒源是一种可以将系统从低功耗状态唤醒的机制。在设备驱动程序的上下文中，它通常是表示需要恢复正常操作的硬件事件。Linux 内核提供了一个用于管理唤醒源的框架。

### 核心概念

- **唤醒事件：** 表示需要恢复正常操作的硬件生成信号。
- **唤醒源：** 内核中物理唤醒事件的表示。
- **唤醒使能/禁用：** 用于控制唤醒源是否处于活动状态的函数。

### 注册唤醒源

要为设备注册唤醒源，驱动程序使用以下函数： C

```
device_set_wakeup_capable(&pdev->dev, true);
device_set_wakeup_enable(&pdev->dev, true);
```

第一个函数表示设备可以作为唤醒源。第二个函数启用唤醒源。

### 处理唤醒事件

当唤醒事件发生时，内核通过恢复函数通知设备驱动程序。然后驱动程序应处理唤醒事件并使设备恢复到完全运行状态。

```
C
static int my_device_resume(struct device *dev) {
struct my_device *my_dev = dev_get_drvdata(dev);

// Check if the device was woken up by a hardware event
if (device_may_wakeup(dev)) {
    // Handle the wakeup event
    handle_wakeup_event(my_dev);
}

// Restore device state
restore_device_state(my_dev);

// Enable interrupts
enable_device_interrupts(my_dev);

// Bring device back to full operation
wake_up_device(my_dev);

return 0;
}
```

### 其他考虑

- **延迟：** 系统从低功耗状态唤醒所需的时间应最小化。
- **功耗：** 唤醒机制本身应消耗最少的功率。
- **误唤醒：** 驱动程序应能够优雅地处理误唤醒事件。

### 示例

C

```
#include <linux/module.h>
#include <linux/kernel.h>
#include <linux/init.h>
#include <linux/platform_device.h>
#include <linux/pm_runtime.h>

// device-specific headers

struct my_device
    // device-specific data
    bool wakeup_enabled;

// device driver functions

static int my_device_probe(struct platform_device pdev) // device
initialization

    device_set_wakeup_capable(&pdev->dev, true);

    return 0;
}
static int my_device_suspend(struct device dev)
    struct my_device *my_dev = dev_get_drvdata(dev);

    my_dev->wakeup_enabled = device_may_wakeup(dev);
    if (my_dev->wakeup_enabled)
        // Configure hardware for wakeup
    }
    // other suspended operations

    return 0;
}
```

```
static int my_device_resume(struct device dev)
    struct my_device my_dev = dev_get_drvdata(dev);

    if (my_dev->wakeup_enabled)
        // Handle wakeup event
        handle_wakeup_event(my_dev);
    }
    // other resume operations

    return 0;
```

正确实现唤醒源对于高效的电源管理至关重要。通过仔细考虑设备的能力和系统的要求，驱动程序可以优化唤醒过程以实现最小的功耗和快速的响应时间。

## 第 16 章

## 设备驱动程序中的安全威胁

设备驱动程序是连接硬件和操作系统的关键软件组件，通常成为被忽视的安全堡垒。它们接近系统资源以及操作的复杂性使其成为恶意攻击的主要目标。本文深入探讨了 Linux 设备驱动程序中的常见安全威胁，并附带代码示例来说明漏洞和缓解策略。

### 常见安全威胁

### 1. 缓冲区溢出

缓冲区溢出发生在程序尝试向缓冲区写入比其容量更多的数据时。这可能会覆盖相邻的内存位置，可能导致代码执行。

```
```c
void my_device_read(struct file *filp, char __user *buf, size_t count, loff_t *f_pos)
{
    // Vulnerable code: no size check
    copy_to_user(buf, my_device_data, count);
}
```
```

缓解措施：

- 始终验证输入数据的大小。
- 使用适当的边界检查使用有界内存复制函数，如 `copy_to_user`。
- 采用内核地址空间布局随机化 KASLR 以阻碍攻击可预测性。

### 2. 使用后释放

### 3. 竞态条件

```
C
static int device_open_count = 0;

int my_device_open(struct inode *inode, struct file *filp) {
    if (device_open_count)
        return -EBUSY;
    device_open_count++;
    // ...
}
```

缓解措施：

- 使用适当的同步原语，如互斥锁或信号量。
- 仔细设计数据访问和修改例程以防止竞态条件。
- 在可行时采用无锁数据结构。

### 4. 权限提升

权限提升利用漏洞获得比最初授予更高的权限。

```
C
// Vulnerable code: granting root access without proper checks
int my_device_ioctl(struct file *filp, unsigned int cmd, unsigned long arg) {
    if (cmd == MY_MAGIC_CMD) {
        capable(CAP_SYS_ADMIN); // Insufficient privilege check
        // Grant root access
    }
    // ...
}
```

缓解措施：

- 基于用户权限强制严格的访问控制。

