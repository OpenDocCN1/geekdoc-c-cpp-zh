![](bbox=[0.16, 0.08, 0.59, 0.28])

# Figure 3.5: A small number of background threads continuously process the queue of regions that have been modified and regenerate the surface geometry. The main thread retrieves the results and uploads the geometry to the GPU.

A small number (1–4) of surface extraction threads run in the background and wait for the priority queue to contain task data to process. When a `TaskData` instance is available, a surface extraction thread will remove it from the priority queue and perform the Marching Cubes algorithm on its specified region. If other mesh processing tasks such as normal computation (Section 3.4) or splitting by material (Section 3.5.2) are necessary, then they are also performed by the surface extraction thread. The resulting vertex and index buffer pair is then assigned to the `TaskData` instance, which in turn is added to a queue of completed tasks.

The main thread is the only one that can copy the data to the GPU (at least on current generation hardware), and so this takes responsibility for removing items from the queue of completed tasks and uploading them to the graphics card. Semaphores are used to control access to the queues and to provide thread synchronization.

In order to give an indication of how well our threaded surface extractor performs, we ran each of our three test volumes through the surface extractor using between one and four threads. In each case, we measured the amount of time actually spent performing surface extraction. Time spent performing other tasks such as