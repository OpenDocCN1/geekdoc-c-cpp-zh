# Synchronization

Post kernel launch, the CPU (host) proceeds without waiting for the kernel to complete unless explicitly synchronized using This function blocks the calling thread until the device has completed all preceding requested tasks.

Output from the GPU is available after the call to cudaDeviceSynchronize().