calculated by multiplying tid by the size of the elements making up the array. Let's assume they all are integer arrays, so the size is 4 bytes per entry.

We very quickly hit the first dependency in the calculation of tid (Figure 9.11). The warp dispatches the multiply of blockIdx.x and blockDim.x to the integer MADD units in the CUDA cores. Until the multiply and add instruction to calculate tid has completed we can continue no further, so the warp is marked as blocked and suspended.

At this point, the next warp is selected, which does the same operation and is again suspended at the calculation of tid. After all warps have progressed to this point, enough clocks have passed such that the value of tid in warp 0 is now known and can be fed into the multiply for the destination address calculations. Thus, three additional MADD instructions are dispatched to the CUDA cores, to calculate the address offsets. The next instruction would be a couple of loads, but for this we need the address of a and b from the multiply instructions. At this point we again suspend the warp and the other warps execute.

Once the address calculation of a is available, the load instruction can be dispatched. It's likely, due to the address calculation of b being issued back to back with that of a, that the address calculation of b will be retired by the time the load for a has been dispatched. Thus, we immediately issue the load for the 'b'. The next instruction in the stream would be a multiply of 'a' and 'b', neither of which will be available for some time yet as they have to be fetched from main memory to the SM. Thus, the warp is suspended and the subsequent warps execute to the same point.

As memory fetches take a long time, all warps dispatch the necessary load instructions to the LSU and are suspended. If there is no other work to do from other blocks, the SM will idle pending the memory transactions completing.

![](bbox=[0.3, 0.52, 0.7, 0.85])

FIGURE 9.11 Data flow dependency.