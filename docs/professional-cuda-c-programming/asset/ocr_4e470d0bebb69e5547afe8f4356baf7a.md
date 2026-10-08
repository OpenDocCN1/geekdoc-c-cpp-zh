The changes for the kernel implementation of crypt is straightforward. First, the keyword device__ is added to doCrypt to indicate it should be executed on the GPU. Second, encrypt_decrypt is declared a __global__ function and the loop it contains is transformed to execute every chunk of data on neighboring device threads based on ID. Third, a new function called encrypt_decrypt_driver is added that launches an encrypt_decrypt kernel with a kernel execution determined by the number of input chunks.

The encrypt_decrypt_driver kernel also performs memory management for the ported kernel, including:

+   1. Allocating all memory required for any input and output data
2. Transferring all application data to the device
3. Freeing all allocated device memory

With these simple changes, the crypt application is executing the majority of computation in CUDA. However you might have noticed a number of ways the performance of this implementation could be improved. The next section will focus on taking the result of this parallelization process and accelerating it to its full potential using profile-driven optimization.

# Optimizing crypt

You have been using profile-driven optimization throughout this book. The NVIDIA Visual Profiler nvvp is a graphical tool that hints to guide your optimization efforts towards the portions of an application where it could be effective. In this section, the profile-driven approach will be used alongside an understanding of the crypt application to take the implementation produced by the Parallelization stage and turn it into a well-performing CUDA application.

For the first stage of profile-driven optimization, you use CUDA profiling tools to gain insight into the performance characteristics of your application. With that information, you can make a decision on where to target optimization efforts. Once you have made changes, you can re-profile your application to determine next steps, leading to iterative improvements in performance.

To get started, use nvvp in unguided-mode to generate a comprehensive profile including suggestions for improvement. When setting up nvvp is as simple as specifying the name of the executable and the location of input and output files in the "Create New Session" popup window, as shown in Figure 10-11.

| File: /home/max/crypt_legacy | Browse |
| Working directory: Enter working-directory [optional] | Browse |
| Arguments: /home/max/text/home/max/crypt/home/max/key | |
| Environment: Name Value Add |
| | Delete |

FIGURE 10-11