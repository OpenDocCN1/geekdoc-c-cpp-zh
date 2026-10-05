# Chapter 8

# Special Topic: Graphics Coprocessor Programming Using CUDA

Graphics libraries such as DirectX and OpenGL are widely used in the computer gaming industry. The graphics libraries provide a number of functions for rendering, shading, texture manipulation, and similar tasks. If a suitable graphics card and driver are installed, these functions are sent from the processor to the graphics card for faster execution.

The graphics cards are powerful processors in their own right. A high-end graphics card may have more than a billion transistors, same as a processor package. The instruction set and design of the graphics processor reflects its principal function. The graphics processor prefers to think in terms of pixels, and the instruction set architecture supports threading at a very fine level. If there is 1 GB of data to be handled, an OpenMP program may divide the data between a dozen $10^4$ or $10^5$ or even more threads.

Despite the focus on pixels and images, the capabilities of graphics processors