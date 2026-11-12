Note that although `printf` is an easy way to display information at the host end, be aware that it’s creating a 1 MB buffer in GPU memory and transferring that buffer back to the host upon certain events.

Thus, the `printf` output will be seen only under the following conditions:

+   1. At the start of a subsequent kernel launch.
+   2. At the end of a kernel execution if the environment variable `CUDA_LAUNCH_BLOCKING` is set (not recommended if using multiple GPUs or streams).
+   3. As the result of a host side-initiated synchronization point such as synchronizing the device, stream, or an event.
+   4. Blocking operations of `cudaMemcpy`.
+   5. Programmer-initiated device reset (`cudaDeviceReset` or driver `cuCtxDestroy` API calls).

Thus, in most cases you will see the output printed. If you do not, simply call `cudaDeviceReset` prior to exiting the host program or `cudaStreamSynchronize` at the end of the set of work from a stream and the missing output should appear.

Should you need a larger buffer, this can be set using the `cudaDeviceSetLimit (cudaLimitPrintfFifoSize, new_size_in_bytes)` API call.

# ## Version control

Version control is a key aspect of any professional software development. It does not necessitate using very expensive tools or huge processes that cover who can update what. In large projects version control is absolutely essential. However, even for single-developer projects, something that may apply to many readers, it is important.

Consider for a moment that debugging a 30,000-thread program is easy. If you laugh at this statement then you realize just how hard a task you are setting yourself up for by not versioning your program, either regularly or whenever a major point is reached. Programmers are generally a fairly overconfident bunch of people and can be sure at the outset that a “simple” change will work without problems. However, when it doesn’t quite work to plan, remembering exactly the set of changes you made can be difficult. Without a working backup of the program it can be difficult if nearly impossible to get back to exactly the working version before the changes.

Most programs in the professional world are developed in teams. A colleague can be extremely helpful in providing a fresh pair of eyes with which to see a problem. If you have a versioned or baselined copy of the working code it makes it relatively easy to look simply at the differences and see what is now breaking the previously working solution. Without these periodic baselines it’s not easy to identify the place where the error might be, and thus instead of a few hundred lines of code, you may have to look at a few thousand.

# # DEVELOPING FOR FUTURE GPUS

# ## Kepler

The roadmap that NVIDIA has presented from Fermi and later versions is the Kepler GK104 (K10), the Kepler GK110 (K20), and the Maxwell. As of March 2012 the first of the Kepler releases was made, the GK104. This product was aimed squarely at the consumer market and lacked some of the