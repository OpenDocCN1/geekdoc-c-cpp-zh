# # False Dependencies

Although Fermi GPUs support 16-way concurrency — that is, up to 16 grids executing at once — all streams are multiplexed into a single hardware work queue. When selecting a grid to execute, the task at the front of the queue is scheduled by the CUDA runtime. The runtime checks for task dependencies, and waits for any tasks that this task depends on to complete if they are executing. Finally, when all dependencies are satisfied the new task is dispatched to available SMs. This single pipeline may result in a false dependency. As illustrated in Figure 6-2, only the circled task pairs will eventually be executed concurrently because the runtime will block launching every other grid. A blocked operation in the queue blocks all subsequent operations in the queue, even when they belong to different streams.

![](bbox=[0.095, 0.303, 0.695, 0.448])

FIGURE 6-2

# # Hyper-Q

False dependencies are reduced in the family of GPUs using multiple hardware work queues, a technology called Hyper-Q. Hyper-Q allows multiple CPU threads or processes to launch on a single GPU simultaneously by maintaining multiple hardware-managed connections between the host and the device. Existing applications that were limited by Fermi's false dependencies can see a dramatic performance increase without changing any existing code. Kepler GPUs use 32 hardware work queues and allocate one queue per stream. If there are more than 32 streams are created, multiple streams will share a single hardware work queue. The result is full stream-level concurrency with minimal inter-stream dependencies. Figure 6-3 illustrates a simple case with three streams on three hardware work queues.

![](bbox=[0.095, 0.723, 0.655, 0.868])

FIGURE 6-3