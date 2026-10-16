# Code example:

```
C
#include <linux/workqueue.h>

static struct workqueue_struct *my_workqueue;
static struct delayed_work my_work;

static void my_work_handler(struct work_struct *work) {
    // Bottom half: perform more complex processing
}

static irqreturn_t my_interrupt_handler(int irq, void *dev_id) {
    // Top half: save critical data
    schedule_delayed_work(&my_work, delay_in_jiffies);
    return IRQ_HANDLED;
}
```

# Softirqs

Softirqs are used for very specific types of bottom half processing, such as network packet handling. They are handled by dedicated kernel threads.

Note: Softirqs are less commonly used in modern kernels and are generally replaced by tasklets or workqueues.

# Choosing the Right Bottom Half Mechanism

The choice of bottom half mechanism depends on the specific requirements of the device driver:

+   - **Tasklets:** Suitable for short, atomic operations.
+   - **Workqueues:** Suitable for longer, non-atomic operations.
+   - **Softirqs:** Used for specific kernel subsystems.