There are, of course, many others that are not shown here. We maintain a list of CUDA libraries at www.cudalibs.com, including a number of our own libraries, provided free for personal or academic use, or licensed and supported for commercial use.

# General library conventions

The NVIDIA-provided libraries, as a general principle, do no memory management for the caller. They instead expect the caller to provide pointers to the area of allocated memory *on the device*. This allows a number of functions on the device to be run one after another without unnecessary device/ host transfer operations between calls.

As they perform no memory operations, it is the caller’s responsibility to both allocate and free memory after usage. This extends even to providing memory for any scratch space or buffer areas used by the library calls.

Although this may seem an overhead to place onto the programmer, it’s actually a very good design principle and one you should follow when designing libraries. Memory allocation is a costly operation. Resources are limited. Having a library continuously allocating and freeing memory in the background is far less efficient than you performing these operations once at startup and then again at program exit.

# NPP (Nvidia Performance Primitives)

The NPP library provides a set of functions for image and general signal processing. It supports all CUDA platforms. To include NPP into your project, simply include the relevant header files and link to the precompiled library.

For signal processing functions, the library expects one or more source pointers (pSrc1, pSrc2, etc.), one or more destination pointers (pDst1, pDst2, etc.), or one or more mixed pointers for in-place operations (pSrcDst1, pSrcDst2, etc.). The library names the functions according to the data type processed. C++ function name overloading—that is, using a single name for a common function—is not supported.

The supported data types for signal processing are Npp8u, Npp8s, Npp16u, Npp16s, Npp32u, Npp32s, Npp64u, Npp64s, Npp32f, and Npp64f. These equate to unsigned and signed versions of 8, 16, 32, and 64 types plus the 32- and 64-bit single-precision and double-precision floating-point types.

The image part of the library follows a similar naming convention, in that the function names reflect intended usage and data type. Image data can be organized in a number of ways, so there are a few key letters that allow you to see the functionality and data type from the name. These are:

+   - A—Used where the image contains an alpha channel that should not be processed.

+   - Cn—Used where the data is laid out in a packed or interleaved format of n channels, for example [R, G, B], [R, G, B], [R, G, B], etc. would be C3.

+   - Pn—Used where the color data is split into planes, such as all the data from one color is contiguous, so [R, R, R], [G, G, G], [B, B, B], etc. would be P3.

In addition to how the data is organized, the naming also tells you how the function will manipulate the data.

+   - I—Used where the image data is manipulated in-place. That is, the source image data will be overwritten by the operation being performed on it.