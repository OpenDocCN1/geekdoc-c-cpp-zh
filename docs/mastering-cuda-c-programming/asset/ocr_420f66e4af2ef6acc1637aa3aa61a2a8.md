# Creating and Executing a CUDA Graph

To illustrate the process of creating and executing a CUDA graph, consider a simple example where two GPU kernels must be executed in sequence, followed by a memory copy operation from device to host.

```
#include __global__ void kernelA() { Kernel A implementation }
__global void kernelB() { Kernel B implementation } void
createAndExecuteGraph() { stream; graph; 0); Node for kernelA
kernelNode; kernelAParams = {0}; == dim3(1, 1, 1); == dim3(1, 1, 1);
graph, NULL, 0, &kernelAParams); Add dependencies (edges) Note:
Node for kernelBNode;
kernelBParams = {0}; == dim3(1, 1, 1); = dim3(1, 1, 1); graph,
&kernelANode, 1, &kernelBParams); Note:
This is implicitly done by specifying kernelANode as a dependency for
kernelBNode Instantiate and launch the graph graphExec; graph, NULL,
NULL, 0); stream; Cleanup
```

In this example, two kernels, kernelA and are encapsulated in a CUDA graph. The dependency between kernelB and kernelA is established by specifying kernelA as a predecessor when adding kernelB to the graph. This ensures that kernelB will not start execution until kernelA has completed. Finally, the graph is instantiated and launched for execution on the GPU.

This programming model allows for intricate sequences of operations to be clearly defined and executed efficiently, reducing the need for CPU-side management of individual tasks and dependencies.