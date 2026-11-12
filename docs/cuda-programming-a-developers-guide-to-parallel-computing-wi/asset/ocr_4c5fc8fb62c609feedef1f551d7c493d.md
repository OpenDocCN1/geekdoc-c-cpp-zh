version users had to upgrade their hardware. Although this might sound like NVIDIA trying to force users to buy more cards, it in fact brings many benefits. When upgrading a compute level, you can often move from an older platform to a newer one, usually doubling the compute capacity of the card for a similar price to the original card. Given that NVIDIA typically brings out a new platform at least every couple of years, we have seen to date a huge increase in available compute power over the few years CUDA has been available.

A full list of the differences between each compute level can be found in the NVIDIA CUDA Programming Guide, Appendix G, which is shipped as part of the CUDA SDK. Therefore, we will only cover the major differences found at each compute level, that is, what you need to know as a developer.

# ## Compute 1.0

Compute level 1.0 is found on the older graphics cards, for example, the original 8800 Ultras and many of the 8000 series cards as well as the Tesla C/D/S870s. The main features lacking in compute 1.0 cards are those for atomic operations. Atomic operations are those where we can guarantee a complete operation without any other thread interrupting. In effect, the hardware implements a barrier point at the entry of the atomic function and guarantees the completion of the operation (add, sub, min, max, logical and, or, xor, etc.) as one operation. Compute 1.0 cards are effectively now obsolete, so this restriction, for all intents and purposes, can be ignored.

# ## Compute 1.1

Compute level 1.1 is found in many of the later shipping 9000 series cards, such as the 9800 GTX, which were extremely popular. These are based on the G92 hardware as opposed to the G80 hardware of compute 1.0 devices.

One major change brought in with compute 1.1 devices was support, on many but not all devices, for overlapped data transfer and kernel execution. The SDK call to `cudaGetDeviceProperties()` returns the `deviceOverlap` property, which defines if this functionality is available. This allows for a very nice and important optimization called double buffering, which works as shown in Figure 3.7.

To use this method we require double the memory space we'd normally use, which may well be an issue if your target market only had a 512 MB card. However, with Tesla cards, used mainly for scientific computing, you can have up to 6 GB of GPU memory, which makes such techniques very useful. Let's look at what happens:

+   - **Cycle 0:** Having allocated two areas of memory in the GPU memory space, the CPU fills the first buffer.

+   - **Cycle 1:** The CPU then invokes a CUDA kernel (a GPU task) on the GPU, which returns immediately to the CPU (a nonblocking call). The CPU then fetches the next data packet, from a disk, the network, or wherever. Meanwhile, the GPU is processing away in the background on the data packet provided. When the CPU is ready, it starts filling the other buffer.

+   - **Cycle 2:** When the CPU is done filling the buffer, it invokes a kernel to process buffer 1. It then checks if the kernel from cycle 1, which was processing buffer 0, has completed. If not, it waits