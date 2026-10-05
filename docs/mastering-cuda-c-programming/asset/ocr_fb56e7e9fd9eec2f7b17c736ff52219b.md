# Factors Affecting Occupancy

Several factors play a crucial role in determining the occupancy of a CUDA kernel. These factors are primarily related to the resources required by each thread and block, as well as the limitations imposed by the hardware. They include:

Threads per number of threads instantiated in each block affects how many threads can be simultaneously active on an SM. High numbers of threads per block may reduce the potential occupancy due to the limited number of threads an SM can handle at once.

Block to threads per block, the size of each block (in terms of threads) impacts the occupancy. Blocks that are too large may limit the number of active blocks on an SM.

Registers per thread uses registers for storing temporary data. The more registers a thread requires, the fewer threads can be active on an SM, affecting occupancy negatively.

Shared memory per use can use shared memory for fast data exchange among threads. However, since shared memory is limited, excessive usage per block can reduce occupancy.