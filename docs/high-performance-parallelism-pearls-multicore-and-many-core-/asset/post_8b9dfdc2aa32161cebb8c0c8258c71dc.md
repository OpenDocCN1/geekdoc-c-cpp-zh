
# THE pyMIC OFFLOAD MODULE

```python
import pyMIC
import numpy

# size of the matrices
m, n, k = 4096, 4096, 4096

# create some input data
alpha = 1.0
beta = 0.0
a = numpy.random.random(m*k).reshape((m, k))
b = numpy.random.random(k*n).reshape((k, n))
c = numpy.zeros((m, n))

# load kernel library
device = pymic.devices[0]
stream = device.get_default_stream()
library = device.load_library("libdgemm.so")

# perform the offload and wait for completion
stream.invoke_kernel(library.mydgemm,
                     a, b, c, m, n, k, alpha, beta)
stream.sync()
```

**FIGURE 14.3**  
dgemm.py: Using pyMIC to perform a dgemm operation on the coprocessor.

```c
#include <pymic_kernel.h>
#include <mkl.h>

PYMIC_KERNEL
void mydgemm(const double *A, const double *B, double *C,
             const int64_t *m, const int64_t *n,
             const int64_t *k,
             const double *alpha, const double *beta) {
    /* invoke dgemm of the cblas wrapper of MKL */
    cblas_dgemm(CblasRowMajor, CblasNoTrans, CblasNoTrans,
                *m, *n, *k, *alpha, A, *k, B, *n, *beta, C, *n);
}
```

**FIGURE 14.4**  
dgemm.c: Kernel in C implementing the offload part of Figure 14.3.

The table shown in Figure 14.5 summarizes the operations that are offered by the OffloadArray class. In addition, the OffloadArray implements the full set of array operations for element-wise addition, multiplication, etc. The operations are all performed on the target device and only require a data transfer if the input data of the second operand is not yet present on the target.

## THE LOW-LEVEL INTERFACE

In addition to the high-level interface of the OffloadArray class, pyMIC exposes the internal low-level interface for buffer management for additional flexibility and optimization opportunities (see Figure 14.6). The low-level interface consists of a memcpy-like interface that supports allocation and deallocation of device memory, data transfers to and from host and coprocessor as well between buffers on the coprocessor. These operations are also part of the streaming API of OffloadStream and thus interact with the high-level API in a natural way. By using this low-level API, programmers gain full control of the memory management and can control every aspect of it. It even becomes possible to perform pointer arithmetic on both host and device data. While this low-level programming may lead to improved performance, it is generally advised to stay with the high-level interfaces to avoid hard-to-find errors that arise from using Python in a nonstandard way.

| Operation | Semantics |
|---|---|
| update_host() | Transfer the buffer from the device |
| update_device() | Transfer the buffer to the device |
| fill(value) | Fill the buffer with the parameter |
| fillfrom(array) | Copy the content array to into the offload buffer |
| zero() | Fill the buffer with 0 (equivalent to fill(0.0)) |
| reverse() | Reverse the contents of the buffer |
| reshape() | Modify the dimensions of the buffer; creates a new view |

FIGURE 14.5
Operations of the OffloadArray class.

![](img/16cb41208935c5f22dd1044f03f2e31b_298_0.png)

FIGURE 14.6
Architecture of the pyMIC module.

Underneath the low-level API module, a Python extension module (`_pyMICImpl`) bridges the gap between the Python level and the low-level offload interfaces and libraries. This layer is written in C/C++ and performs the mapping between the Python data types and APIs into the world of C/C++ data types and low-level functions. The lowest level, the offload library, is based on LIBXSTREAM that implements asynchronous data transfers and offloads. In addition, pyMIC ships with a library that contains kernels for offloading the operations of the `OffloadArray` class to implement the typical array operations on the coprocessor.

## EXAMPLE: SINGULAR VALUE DECOMPOSITION

The following, more extensive, example of an image compression/decompression program that uses the singular-value decomposition (SVD) shows how pyMIC allows programmers to choose offload abstractions at different levels.

Figure 14.7 shows six images that have been processed with SVD for different quality and thus different rates of compression. The upper left image shows the original image in JPEG format (original resolution 1920 × 2560). The compression starts with the image as a gray-scale image of n × m pixels;

![](img/16cb41208935c5f22dd1044f03f2e31b_299_0.png)

# FIGURE 14.7

SVD algorithm applied to a gray-scale picture.

each pixel of the image is stored as a matrix $M$ of floating-point values that correspond to the gray-scale value of each pixel. The compression then performs the SVD to calculate three matrices $U$, $\Sigma$, and $V$ such that $M = U\Sigma V^T$. If $M$ is a matrix with real numbers, then $U$ is a unitary $m \times m$ matrix, $\Sigma$ is an $n \times m$ diagonal matrix, and $V^T$ is a transposed $n \times n$ unitary matrix. To compress the image, the algorithm creates a new diagonal matrix $\Sigma'$ that only contains some values of the $\Sigma$ matrix, for example, by restricting it to a submatrix or by dropping values that are close to zero or below a threshold value. Correspondingly, rows and columns of $U$ and $V$ may be removed to match the dimensionality of $\Sigma'$, leading to $U'$ and $V'$.

To reconstruct the image, the decompression algorithm computes $M' = U'\Sigma'V'^T$ and uses the resulting matrix $M'$ as the output image. One particularly interesting property of this algorithm is that even with very low dimensionality of $\Sigma'$, the most important features of the compressed image become visible as shown by Figure 14.7. The images in the upper row of Figure 14.7 are the result of retaining only one and two values in the $\Sigma$ matrix, whereas the lower row contains the outcome of keeping 10, 25, and 100 values in $\Sigma'$. This corresponds to a data reduction of 99.9% and 99.8% for the images in the top row, and 99.0%, 97.7%, and 90.7% for the lower row.

The corresponding compression code for the construction of the SVD is shown in Figure 14.8. The `read_image` function takes a file name as the argument, reads the image from disk, and converts it to gray-scale data. Another function, `compute_svd`, converts the image data into Numpy’s matrix data type and then applies the SVD algorithm to compute and pass back the three matrices. For the sake of brevity, we rely on Numpy’s implementation of the SVD algorithm.

The functions `read_image` and `compute_svd` are called from the `compress_image` function, which then restricts each of the matrices according to the compression factor. The factor determines how many rows and columns of the matrices will be preserved; the lower the factor, the higher the compression. The function `decompress_image` implements the inverse operation by calculating $M'$ by applying two matrix-matrix multiplications.

Using the offloaded `dgemm` kernel of Figure 14.4 and pyMIC’s high-level offloading, one can easily replace the matrix multiplications with invocations of `dgemm` (see Figure 14.9). The Numpy array `tmp` is supposed to store the result of multiplying $U$ and $\Sigma$, `M_prime` will store the result of the second `dgemm` operation. After preparing all needed arguments, the code performs two offloads to compute the two matrix multiplications. In this example, it is easy to see that pyMIC’s copy-in/copy-out semantics leads to superfluous data transfers; `tmp` and `M_prime` are copied to the coprocessor, although they will be overwritten there. In addition, the matrix `tmp` is transferred from the coprocessor to the host and is then immediately copied back.

For applications that have more complex algorithms, it will be more difficult to see when and in which part of the code data transfers are happening. To help optimize data transfers and/or offloads, pyMIC comes with some basic debugging and performance analysis features. Setting the environment variable `PYMIC_TRACE` to a value greater than 1 enables the tracing feature of pyMIC. After the application finishes, pyMIC outputs a postmortem list of all call sites of its API and the respective stack traces of these call sites. The pyMIC module also supports on-the-fly debugging output of key API calls. The environment variable `PYMIC_DEBUG` enables the additional output to visualize all requests for both implicit and explicit data transfers as well as invocations of offloaded kernels. Please see the documentation of pyMIC for further information.

Figure 14.10 shows how to avoid the aforementioned unnecessary data transfers for the SVD reconstruction. Instead of working on the Numpy data structures, the optimized version of
