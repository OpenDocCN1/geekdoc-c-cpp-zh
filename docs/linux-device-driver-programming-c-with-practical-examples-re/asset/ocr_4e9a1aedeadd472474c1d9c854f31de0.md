+   - `irqreturn_t`: Return type indicating whether the interrupt was handled.
+   - `irq`: The interrupt number.
+   - `dev_id`: Optional device-specific data.

# Interrupt Sharing

Multiple device drivers can share the same interrupt line. In such cases, the `IRQF_SHARED` flag is used when registering the interrupt handler. The kernel ensures that only one ISR runs at a time for a shared interrupt.

# Bottom Halves

For tasks that cannot be completed within the ISR, use bottom halves (tasklets or workqueues) to defer processing to a process context. This helps prevent interrupt latency and allows for more complex operations.

# Freeing an Interrupt Handler

When the device is no longer used, free the interrupt handler using `free_irq`: