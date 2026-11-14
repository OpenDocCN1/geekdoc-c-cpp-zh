
![](img/55beb9162c0073b3a3d7b44f1d5873e8_33_0.png)

FIG. 2.6 Block diagram of a typical multiple CPU/multiple cores architecture (with two quad-core CPUs) using a shared memory organization.

## MOST INTERCONNECTION OF THE CPUS AND OTHER COMPONENTS

The type of interconnections used in a target architecture depends on the level of performance required and the platform vendor.

An example of a switch fabric is the “TeraNet”. An example of a fast link is HyperLink. They are both used in some ARM-based SoCs proposed by Texas Instruments Inc., providing efficient interconnections of the subsystems to the ARM multicore CPUs and to the external accelerators.

In Intel-based computing systems, the memory subsystem is usually connected via Intel Scalable Memory Interfaces (SMI) provided by the integrated memory controllers in the CPU. They also include a fast link connecting other subsystems to the CPU using the Intel QuickPath Interconnect (QPI), a point-to-point interconnect technology. AMD provides the HyperTransport technology for point-to-point links.

Texas Instruments Inc., AM5K2GX0 multicore ARM KeyStone II system-on-chip (SoC), SPRS640D—November 2010. Intel Corp. An introduction to the Intel QuickPath interconnect. January 30, 2009. API networks accelerates use of hypertransport technology with launch of industry's first hypertransport technology-to-PCI bridge chip. (Press release). HyperTransport Consortium, 2001-04-02.

## 2.2.3 HETEROGENEOUS MULTIPROCESSOR/MULTICORE ARCHITECTURES

A current trend in computing organization is the Heterogeneous System-on-a-Chip (SoC) with multiple independent and distinct CPUs, where each processor has an arbitrary number of cores and other computing devices such as hardware accelerators. Fig. 2.7 shows a block diagram of an architecture with two distinct CPUs (one with two cores and the other with four cores) and a GPU. This computer organization is similar to the one used in mobile devices such as smartphones (see Heterogeneous SoCs).

![](img/55beb9162c0073b3a3d7b44f1d5873e8_34_0.png)

FIG. 2.7 Block diagram of a typical heterogeneous architecture.

## 2.2.4 OpenCL PLATFORM MODEL

Currently, parallel computing architectural models are being extensively used in part due to the existence of hardware implementations supporting them. One well-known example is the computing model proposed in the context of OpenCL (Open Computing Language) [15,16] and instances of the model are herein referred as OpenCL computing devices. This model is supported by a wide range of heterogeneous architectures, including multicore CPUs, and hardware accelerators such as GPUs and FPGAs. In the OpenCL approach, a program consists of two parts: the host program running on the CPU, and a set of kernels running on OpenCL-capable computing devices acting as coprocessors. Chapter 7 provides details about the OpenCL language and tools.

## HETEROGENEOUS SOCs

An example of a SoC with organization similar to the one presented in Fig. 2.7 is the Exynos 7 Hexa 7650 (Exynos 7650*) designed and manufactured by Samsung Electronics for some of the Samsung smartphones. The SoC includes one 1.8 GHz ARMv8A dual-core Cortex-A72, one 1.3 GHz ARMv8 quad-core Cortex-A53 (and with seamless support of 32-bit and 64-bit instruction sets), and one Mali-T860MP2 GPU.

![](img/55beb9162c0073b3a3d7b44f1d5873e8_35_0.png)

FIG. 2.8 High-level block diagram of the OpenCL platform model.

Fig. 2.8 shows a high-level block diagram of a typical OpenCL platform which may include one or more computing devices. Each device includes several Computing Units (CUs) and each Computing Unit consists of several Processing Elements (PEs). A single kernel can execute in one or more PEs in parallel within the same CU or in multiple CUs. The computing devices (e.g., a GPU board with support to OpenCL) are connected to a host CPU via a shared bus.

PEs are typically SIMD units responsible for executing sequences of instructions without conditional control flow. In some cases, control flow can be supported by applying if-conversion and/or by executing both branches and then selecting the required results by multiplexing the values provided by the different branches.

As depicted in Fig. 2.9, an OpenCL computing device may also include a hierarchical memory organization consisting of private memories (registers tightly coupled to the PEs (one memory per PE), a local memory per CU, a global read-only memory that can be written by the host CPU but only read by the computing device, and a global memory read/written by the computing device and by the host CPU. Each CU's local memory is shared by all the CU's PEs.

The OpenCL kernels execute through parallel work items (each one with an associated ID and seen as hardware threads) and the work items define groups (known as work groups). Each work group executes on a CU and its associated work items execute on its PEs.

The OpenCL platform is very suitable for computations structured in SIMT (Single Instruction, Multiple Thread) as is the case when targeting GPUs. Recently, the main FPGA vendors have adhered to the OpenCL model and provide toolchain support to map the model to the FPGA resources (i.e., making FPGAs OpenCL computing devices).

![](img/55beb9162c0073b3a3d7b44f1d5873e8_36_0.png)

FIG. 2.9 Block diagram of the OpenCL model [15].

## 2.3 CORE-BASED ARCHITECTURAL ENHANCEMENTS

In addition to the recent multicore trend, CPU cores have also been enhanced to further support parallelism and specific type of computations. This includes the use of SIMD, FMA units, and support for multithreading.

### 2.3.1 SINGLE INSTRUCTION, MULTIPLE DATA UNITS

Single Instruction, Multiple Data (SIMD) units refer to hardware components that perform the same operation on multiple data operands concurrently. Typically, a SIMD unit receives as input two vectors (each one with a set of operands), performs the same operation on both sets of operands (one operand from each vector), and outputs a vector with the results. Fig. 2.10 illustrates a simple example of a SIMD unit executing four operations in parallel (as represented as follows).

```
C[3:0] = A[3:0] op1 B[3:0];
```

### SIMD UNITS

SIMD units have been available in Intel microprocessors since the advent of the MMX, SSE (Streaming SIMD Extensions), and AVX (Advanced Vector Extensions) ISA extensions [17]. The MMX extensions were initially included to speed up the performance of multimedia applications and other application domains requiring image and signal processing.

ARM has also introduced SIMD extensions to ARM Cortex architectures with their NEON technology. The NEON SIMD unit is 128-bit wide and includes 16 128-bit registers that can be used as 32 64-bit registers. These registers can be thought of as vectors of elements of the same data type, being the data types assigned 8, 16, 32, 64-bit, and single precision floating point. The following example shows how vector statement involving single precision floating-point data can be implemented in a Cortex-A9 using the SIMD unit.

```
A[3:0] = B[3:0] x C[3:0];
// assembly
VLD1.32 {r0}, {s15}
Vldmia.32 r1!, {s14}
Vmul.f32 s15, s15, s14
vstmia.32 r2!, {s15}
```

Typically, the operations in SIMD units include basic arithmetic operations (such as addition, subtraction, multiplication, negation) and other operations such as absolute (abs) and square root (sqrt).

Another factor contributing to the increased performance of SIMD units is the fact that multiple data items can be simultaneously loaded/stored from/to memory exploiting the full width of the memory data bus. Fig. 2.11 depicts a simple illustrative example using SIMD units and vector processing. As can be seen in Fig. 2.11C, the code using SIMD units executes ¼ of the instructions in ¼ of the clock cycles when compared with code executing without SIMD units (Fig. 2.11B).

To exploit SIMD units, it is very important to be able to combine multiple load or store accesses in a single SIMD instruction. This can be achieved when using contiguous memory accesses, e.g., in the presence of unit stride accesses, and when array elements are aligned. In the previous example, arrays A, B, and C are accessed with unit stride and we assume they are aligned (i.e., the base address of each element

![](img/55beb9162c0073b3a3d7b44f1d5873e8_37_0.png)

FIG. 2.10 Example of a SIMD unit, executing in this example the same four operations (with different operands) in parallel.
