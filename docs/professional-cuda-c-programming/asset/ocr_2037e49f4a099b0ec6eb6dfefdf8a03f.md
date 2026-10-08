# 3

# CUDA Execution Model

WHAT'S IN THIS CHAPTER?

+   - Developing kernels with a profile-driven approach
- Understanding the nature of warp execution
- Exposing more parallelism to the GPU
- Mastering grid and block configuration heuristics
- Learning dynamic CUDA performance metrics and execution
- Probing dynamic parallelism and nested execution

```
CODE DOWNLOAD The wrox.com downloads for this chapter are found at www.wrox.com/go/producae on the Download Code tab. The code is in the Chapter 3 download and individually named to the names throughout the chapter.
```

Through the exercises in the last chapter, you will learn how to organize threads into grids and blocks to deliver the best performance. While you can find the best execution configuration through trial-and-error, you might be left wondering why the selected execution outperforms others. If you want to know if there are some guidelines for selecting grid and block configurations. This chapter will answer those questions and provide you with deeper insight into kernel launch configurations and performance profile information, from a different angle: the hardware perspective.



In general, an execution model provides an operational view of how instructions are executed on a specific computing architecture. The CUDA execution model exposes an abstract view of