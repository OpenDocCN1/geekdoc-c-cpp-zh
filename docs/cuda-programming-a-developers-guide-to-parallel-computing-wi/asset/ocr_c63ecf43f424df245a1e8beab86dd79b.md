# # Setting Up CUDA

# ## INTRODUCTION

This chapter is here for anyone who is completely new to CUDA. We look at how to install CUDA on the various OSs, what tools you can use, and how CUDA compiles. Finally, we look at how to have the API help you identify the coding and API errors everyone makes.

CUDA is supported on three major OSs: Windows, Mac, and Linux. By far the easiest platform to use and learn CUDA with is the OS you are most familiar with using for programming development. For an absolute beginner, the Windows OS in conjunction with Microsoft Visual C++ is likely to be the best choice. Both the Windows and Mac installations are fairly much point and click. Both provide fairly standard integrated development environments that work well with CUDA.

# ## INSTALLING THE SDK UNDER WINDOWS

To install CUDA onto a PC running Windows, you’ll need to download the following components from the NVIDIA developer portal at http://developer.nvidia.com/cuda-toolkit-41. Note by the time this book hit the press release 5 of the toolkit was in its release candidate phase. Please check the NVIDIA website for the latest version.

You will need an already installed version of Microsoft Visual Studio 2005, 2008, or 2010. The first step is to download and install the latest set of NVIDIA development drivers for your relevant operating system from the previous link. Then you will need either the 32- or 64-bit version of the CUDA toolkit and GPU computing SDK code samples. Make sure you pick the correct version for your OS. Install them in this order:

+   1. NVIDIA development drivers
+   2. CUDA toolkit
+   3. CUDA SDK
+   4. GPU computing SDK
+   5. Parallel Nsight debugger