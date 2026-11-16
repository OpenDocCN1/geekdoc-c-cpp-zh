# 9.1 The Memory Model

Regardless of how the display lists get created, a renderer might ultimately be restricted by memory access speed, particularly when the graphics commands are generated through a single thread. In recent years, the increasing performance gap between GPU processing power and memory latencies has made it harder to feed the GPU due to expensive data accesses in system memory, as shown in Figure 9.3. A typical frame is subdivided into passes which handle, for instance, rendering shadow maps, rendering the main scene, and rendering fullscreen post-processing effects. A unit of work during rendering is often referred to as a batch and combines a set of render states, shaders, and geometry elements as exemplified by the following listing:

```
//setting up a batch
setRenderStates (...);
bindTextures (...);
setShaders (...);
setShaderConstants (...);
setVertexBuffer (...);
setIndexBuffer (...);
drawCall (...);
```

![](bbox=[0.17, 0.63, 0.56, 0.86])

Figure 9.3: Both the render thread and the graphics API are