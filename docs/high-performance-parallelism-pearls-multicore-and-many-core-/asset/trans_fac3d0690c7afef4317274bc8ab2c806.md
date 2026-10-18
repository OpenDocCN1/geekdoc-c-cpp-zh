

```python
import numpy
from PIL import Image

def read_image(file):
    # open the image and convert it to gray scale
    img = Image.open(file)
    img = img.convert("LA")
    return img

def compute_svd(image):
    # convert the gray-scale image into numpy.matrix
    mtx = numpy.asarray(image.getdata(), dtype=float)
    mtx.shape = (image.size[1], image.size[0])
    mtx = numpy.matrix(mtx)
    U, sigma, V = numpy.linalg.svd(mtx)
    return U, sigma, V

def compress_image(file, factor):
    # read image and decompose it
    image = read_image(file)
    U, sigma, V = compute_svd(image)

    # compress
    c = numpy.matrix(U[:, :factor])
    Sc = numpy.diag(sigma[:factor])
    Vc = numpy.matrix(V[:factor, :])

def decompress_image(U, sigma, V):
    # reconstruct the image data
    M_prime = U * sigma * V
    image = Image.fromarray(M_prime)
    return image
```

svd.py：为以 JPEG 数据存储的图像构造 SVD。

reconstruct_image 创建 OffloadArrays 来存储矩阵和临时数据。对于矩阵 U、Σ 和 V，它使用 bind 操作创建一个与现有 Numpy 数组关联的 offload 缓冲区。对于 tmp 和 M_prime，它在协处理器上分配空缓冲区来存储数据。将 update_host 参数设为 False，指示 pyMIC 只分配缓冲区，而不要将数据传输到主机内存。随后代码像之前一样调用内核，但现在传递的是 offload 数组而非 Numpy 数组。pyMIC 模块据此识别，不对这些数组发出 copy-in/copy-out 请求。最后，使用 OffloadArray 的 update_host 方法来更新并获取 M_prime 数组的主机副本。

```python
def reconstruct_image(U, sigma, V):
    alpha, beta = 1.0, 0.0
    tmp = numpy.empty((U.shape[0], U.shape[1]), dtype=float)
    m_prime = numpy.empty((U.shape[0], V.shape[1]), dtype=float)

    # tmp = U * sigma
    m, k, n = U.shape[0], U.shape[1], sigma.shape[1]
    stream.invoke(library.mydgemm,
                  U, sigma, tmp, m, n, k, alpha, beta)

    # m_prime = tmp * V
    m, k, n = tmp.shape[0], tmp.shape[1], V.shape[1]
    stream.invoke(library.mydgemm,
                  tmp, V, m_prime, m, n, k, alpha, beta)

    stream.sync()

    # reconstruct the image from the matrix
    image = Image.fromarray(m_prime)
    return image
```

**图 14.9** svd_decompress_simple.py：将解压缩例程卸载到协处理器。

## GPAW

### 概述

GPAW 是一个开源软件包，用于与材料和纳米科学相关的各种研究问题中的电子结构计算。GPAW 基于 DFT，并实现了多种 post-DFT 方法，如含时 DFT、GW 近似和 Bethe-Salpeter 方程。GPAW 利用投影缀加波（PAW）方法处理原子核附近的区域，并使用不同的基组（即均匀实空间网格、平面波、数值原子轨道）对方程进行离散化。本工作中，我们专注于使用均匀实空间网格的基本 DFT 计算。

传统上，HPC 应用使用 Fortran 和 C 等编译型语言。相反，GPAW 使用 Python 和 C 的组合。高层算法用 Python 实现，使应用开发者能够受益于 Python 的高层特性，而关键数值内核则用 C 实现或利用如 Intel 数学核心函数库等库。这种方法既提供了高程序员生产率，又保持了高性能。

```python
def reconstruct_image(U, sigma, V):
    alpha, beta = 1.0, 0.0

    # create offload buffers
    offl_U = stream.bind(U)
    offl_sigma = stream.bind(sigma)
    offl_V = stream.bind(V)
    offl_tmp = stream.empty((U.shape[0], U.shape[1]),
                            dtype=float, update_host=False)
    offl_M_prime = stream.empty((U.shape[0], V.shape[1]),
                            dtype=float, update_host=False)

    # tmp = U * sigma
    m, k, n = U.shape[0], U.shape[1], sigma.shape[1]
    stream.invoke(library.mydgemm, offl_U, offl_sigma, offl_tmp,
                  m, n, k, alpha, beta)

    # M_prime = tmp * V
    m, k, n = offl_tmp.shape[0], offl_tmp.shape[1], V.shape[1]
    stream.invoke(library.mydgemm,
                  offl_tmp, offl_V, offl_M_prime,
                  m, n, k, alpha, beta)
    M_prime = offl_M_prime.update_host().array
    stream.sync()

    image = Image.fromarray(M_prime)
    return image
```

**图 14.10** svd_decompress_opt.py：带卸载到协处理器的解压缩例程。

即使在标准 CPU 上 Python 开销通常很小（5-10%），Python 部分仍是串行的，无法在 Intel Xeon Phi 协处理器上原生执行。然而，pyMIC 接口允许从 GPAW 的高层 Python 代码启动内核并控制数据传输，这使得卸载方法成为可行的选择。

### DFT 算法

下面我们使用原子单位（ℏ = m = e = 4π/ε₀ = 1）。基态 DFT 的所谓 Kohn-Sham 方程可以写成

$$H\psi_n(r) = \epsilon_n \psi_n(r), \tag{14.1}$$

$$H = -\frac{1}{2}\nabla^2 + v_{\mathrm{eff}}(r) = -\frac{1}{2}\nabla^2 + v_H(r) + v_{\mathrm{ext}}(r) + v_{\mathrm{xc}}(r), \tag{14.2}$$

$$\nabla^2 v_H(r) = -4\pi\rho(r), \tag{14.3}$$

$$\rho(r) = \sum_i |\psi_i(r)|^2, \tag{14.4}$$

网格点 $G^a$ 定义在原子 $a$ 的缀加球内。最后，波函数乘以对角化矩阵 $H_{nn'}^D$，

$$\psi'_{nG}=\sum_{n'}H_{nn'}^D\psi_{n'G}.\tag{14.10}$$

3. 波函数的迭代细化需要将 Hamiltonian 作用于波函数，以及多重网格预处理，后者使用与 Poisson 问题类似的限制和插值操作。
4. 波函数的正交归一化需要构造重叠矩阵

$$S_{nn'}=\sum_G\psi_{nG}\sum_{G'}S_{GG'}\psi_{n'G'},\tag{14.11}$$

其中重叠算符涉及与子空间对角化相同的投影函数操作。重叠矩阵经过 Cholesky 分解并求逆，得到矩阵 $S_{nn'}^D$，之后正交归一的波函数通过下式获得

$$\psi'_{nG}=\sum_{n'}S_{nn'}^D\psi_{n'G}.\tag{14.12}$$

表征计算量的两个主要参数是网格点数 $N_G$ 和电子能带数 $N_b$，两者都与系统中的原子数 $N_a$ 成正比。关键操作的计算复杂度总结于图 14.11 所示的表格中。

### 卸载

上一节对 DFT 算法的描述表明，在大规模计算中，子空间对角化和正交归一化中的 $\mathcal{O}(N_a^3)$ 操作将主导计算时间（见图 14.11）。为进一步量化计算瓶颈，图 14.12 展示了一个相对较大的生产级基准测试用例的执行剖析。该基准由 Pb 表面上的两个富勒烯分子组成，系统中总共有 232 个原子。基准系统如图 14.13 所示。

| 操作 | 复杂度 |
|---|---|
| Poisson 方程 | $\mathcal{O}(N_a)$ |
| 子空间对角化 | $\mathcal{O}(N_a^3)$ |
| 波函数细化 | $\mathcal{O}(N_a^2)$ |
| 正交归一化 | $\mathcal{O}(N_a^3)$ |

**图 14.11** DFT 算法各部分的计算复杂度，其中 $N_a$ 为计算中的原子数。

**图 14.12** 在 Intel VTune Amplifier XE 中 GPAW 基准测试（无卸载）的热点剖析。

![](img/16cb41208935c5f22dd1044f03f2e31b_306_0.png)

**图 14.13** 由 Pb 表面上两个富勒烯分子组成的基准系统。

![](img/16cb41208935c5f22dd1044f03f2e31b_306_1.png)

