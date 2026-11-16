# 9.7 Performing Graphical Operations in Parallel

So far, we have discussed some techniques that help to improve overall performance, but we can go a step further and allow different processing units to work in parallel to create the final image for a frame. Modern games use multiple render targets within a single frame, and some of them are not accessed simultaneously by the GPU. For instance, it is often possible to access a back buffer with another processing unit such as an SPU to perform some post-processing effects while the GPU starts rendering the next frame. This gives up to a full frame to render the effects, while keeping the same frame rate, but at the expense of an additional frame of latency (see Figure 9.6).

![](bbox=[0.162, 0.412, 0.596, 0.602])

Figure 9.6: While the helper thread computes the post-effects, the GPU starts rendering the next frame.