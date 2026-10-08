to set the mode to CUBLAS_POINTER_MODE_DEVICE when summing the rows of the output matrix on the device. When performing the final sum across rows the mode is set to CUBLAS_POINTER_MODE_HOST and the return address is set to a variable in the host application's address space. You may recall a brief explanation about the cuSPARSE version of function, cusparsePointerMode, in the section titled "Important Topics in cuSPARSE."

# # Summary of OpenACC

This section introduced you to the OpenACC execution and programming model. OpenACC is a flexible, easy-to-use high-performance programming model that complements CUDA and the CUDA libraries in many ways. Compared to the CUDA libraries, OpenACC is more flexible and allows you to write your own computational functions using the C language. Compared to CUDA, OpenACC is more convenient and requires less manual management of memory and computation than CUDA.

However, OpenACC is not without its downsides. A simple OpenACC implementation that ignores data movement often degrades performance due to unnecessary memory copies. OpenACC by default must be conservative about optimization strategies. With the async, copyin and copyout clauses OpenACC performance often lags behind hand-coded CUDA versions. Additionally, for many domains, OpenACC simply cannot beat the performance and usability of pre-written, expert-tuned CUDA libraries.

Despite these drawbacks, the balance of OpenACC across performance, usability, and customizability makes it an attractive programming model to complement CUDA for rapid development of high-performance GPU applications.

# # SUMMARY

This chapter prepared you to make use of cuSPARSE, cuBLAS, cuFFT, cuRAND, and OpenACC to accelerate your application and development process.

The CUDA libraries are powerful in their simplicity, usability, portability, and performance. They were deliberately designed to benefit domain experts with past experience in the fields for which they are most useful. Applications that do not require a large amount of customization can use of these libraries and their component functions as basic building blocks of GPU-accelerated applications.

More importantly, the focus on the general workflow, abstract concepts, and porting process shared among these libraries prepared you to move beyond the scope of this chapter and explore more advanced concepts in these libraries as well as entirely new CUDA libraries. Although the libraries specifically covered in this chapter were selected because of their applicability to a wide range of cases and applications, this chapter could only skim the surface of CUDA library functionality.

On the other hand, OpenACC offers you more control over GPU execution than CUDA libraries while eliminating the more mundane tasks of GPU programming. In OpenACC, many of the same operations supported by the CUDA API can be performed by using simple compiler directives that guide automatic parallelization. In fact, most of the performance lessons taught in this book