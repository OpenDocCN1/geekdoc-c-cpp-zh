+   - The callbacks registered with the events associated with this queue.

+   - The power management state for the queue. KMDF supports power-managed and non-managed queues. For the former, the I/O handler wakes up the device when required (and when possible), the idle timer when the device has no I/Os queued, and calls the driver's I/O cancellation routines when the system is switching away from a working state.

+   - The dispatch method for the queue. KMDF can deliver I/Os from a queue in sequential, parallel, or manual mode. Sequential I/Os are delivered one at a time (KMDF waits for the driver to complete the request), while parallel I/Os are delivered to the driver as soon as possible. In manual mode, the driver must manually retrieve I/Os from the queue.

+   - Whether the queue can accept zero-length buffers, such as incoming requests that don't contain any data.

> Note The dispatch method only affects the number of requests that can be active inside a driver at once. It does not determine whether the event callbacks will be called concurrently or serially. That behavior is determined through the synchronization object described earlier. Therefore, it is possible for a parallel queue to have concurrency disabled but still have multiple incoming requests.

By the mechanism of queues, the KMDF I/O handler can perform various tasks upon receiving a create, close, cleanup, write, read, or device control (IOCTL) request:

+   - For create requests, the driver can request to be immediately notified through the EvtFileCreate callback event, or it can create a non-manual queue to receive requests. It must then register an EvtIoDefault to receive the notifications. Finally, if none of these methods are used, KMDF will simply complete the request with a success code, meaning that by default, applications will be able to open handles to KMDF drivers that don't supply their own code.

+   - For cleanup and close requests, the driver will be immediately notified through EvtFileCleanup and EvtFileClose callbacks, if registered. Otherwise, the framework will simply complete with a success code.

+   - For write, read, and IOCTL requests, the flow shown in Figure 6-46 applies.