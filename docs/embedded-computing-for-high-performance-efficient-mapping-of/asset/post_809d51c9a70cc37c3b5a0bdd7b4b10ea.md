
![](img/55beb9162c0073b3a3d7b44f1d5873e8_28_0.png)

FIG. 2.1 Indicative computer architecture trends in terms of performance enhancements. Based on Lecture materials for “CSE 6230—High Performance Computing: Tools and Applications” course (Fall 2013): “Performance Tuning for CPU: SIMD Optimization”, by Marat Dukhan, Georgia Institute of Technology. United States.

- Find the best trade-off between accuracy and other nonfunctional requirements by reducing computation requirements of specific calculations while meeting numerical accuracy requirements, for example.
- Migrate (also known as offloading) sections of the code from the host CPU to one or more hardware accelerators (e.g., GPUs, FPGAs) to meet nonfunctional requirements, such as performance and energy efficiency.

In some instances, developers may simply consider the use of a more suitable hardware platform, which includes microprocessors, peripherals, and accelerators with more powerful computing capabilities.

## 2.2 TARGET ARCHITECTURES

A recent trend in embedded computing platforms involves the inclusion of multiple computing components that are either homogeneous or heterogeneous, and are connected using traditional bus systems or using more advanced communication systems based on networking such as those found in network-on-a-chip (NoC) devices. Typically, these architectures include multiple distributed memories, in addition to shared memories, at distinct levels of the memory hierarchy and with different address space views.

![](img/55beb9162c0073b3a3d7b44f1d5873e8_29_0.png)

FIG. 2.2 Block diagram of typical single CPU/single core architectures: (A) with all devices connected through a system bus; (B) with the possibility to have devices connected to the CPU using direct channels.

The simplest embedded computing system consists of a single CPU/core with a system bus that connects all the system devices, from I/O peripherals to memories, as illustrated by the block diagram in Fig. 2.2A. In some cases, computing devices (e.g., the CPU) have direct access to other components using point-to-point channels (Fig. 2.2B). In other cases, all the components are accessed using a memory-mapped addressing scheme where each component is selected and assigned to a specific region of the global address space.

In most high-performance systems, the CPU uses a hierarchical memory cache architecture. In such systems, the first level of memory has separate instruction and data caches [9]. For instance, in the system depicted in Fig. 2.2, the memory is organized as a level one (L1) instruction (I) and data (D) caches, a second level of cache (L2) and the main memory. However, there are cases, such as low-performance and safety-critical systems, where the system only supports one level of memory. This is because most safety-critical systems with stringent real-time requirements may not cope with the variability of the execution time that cache memories introduce. In particular, a system may not meet its real-time requirement as dictated by the worst-case execution time (WCET) when using cache memories, and therefore these systems may not include them.

### 2.2.1 HARDWARE ACCELERATORS AS COPROCESSORS

Simple embedded systems, such as the ones depicted in Fig. 2.2, can be extended by connecting the host CPU to coprocessors acting as hardware accelerators. One type of hardware accelerator is the FPGA, which is a reprogrammable silicon chip that can be customized to realize any digital circuit. Other examples of hardware accelerators include GPUs and network coprocessors (i.e., coprocessors specially devoted to the network interface and communication).

![](img/55beb9162c0073b3a3d7b44f1d5873e8_30_0.png)

FIG. 2.3 Block diagram of a typical single CPU/single core architecture extended with hardware accelerators.

Fig. 2.3 presents a block diagram of an architecture consisting of a CPU (③) and a hardware accelerator (②). Depending on the complexity of the hardware accelerator and how it is connected to the CPU (e.g., tightly or loosely coupled), the hardware accelerator may include local memories (③ on-chip and/or external, but directly connected to the hardware accelerator). The presence of local memories, tightly coupled to the accelerator, allows local data and intermediate results to be stored, which is an important architectural feature for supporting data-intensive applications.

At a programmatic level, an important aspect to consider when using hardware accelerators is the data movement cost between the accelerator and the host processor. Often, the accelerator only has control of its local storage, and data communication between the host processor and the accelerator is accomplished explicitly via data messaging. Despite its conceptual simplicity, this organization imposes a significant communication overhead if the CPU must be involved in transferring data from the main memory (⑤) to the accelerator (②). An alternative arrangement that incurs in a much lower communication overhead relies on the use of direct memory access (DMA), as the accelerator can autonomously access data in the main memory (⑤→②). In this case, only the data location needs to be communicated between the host CPU and the accelerator (①↔②). In addition, and depending on the system-level connectivity of the input/output devices, the hardware accelerator may be directly connected to input/output channels (④↔②), e.g., using FIFOs thereby bypassing the host CPU altogether.

Hardware accelerators are also used in desktops and servers, and are commonly connected to the CPU via a PCI-express (PCIe) bus. Although PCIe provides a dedicated connection, it still imposes a high data transfer latency and exhibits low throughput. Thus, only computationally intensive regions of code where the ratio of computational effort to data transferred is high may profit from offloading them to hardware accelerators.

![](img/55beb9162c0073b3a3d7b44f1d5873e8_31_0.png)

FIG. 2.4 Block diagram of a typical multicore architecture (quad-core CPU).

### 2.2.2 MULTIPROCESSOR AND MULTICORE ARCHITECTURES

Modern microprocessors are based on multicore architectures consisting of a number of processing cores. Typically, each core has its own instruction and data memories (L1 caches) and all cores share a second level (L2) on-chip cache. Fig. 2.4 presents a block diagram of a typical multicore (a quad-core in this case) CPU computing system where all cores share an L2 cache. The CPU is also connected to an external memory and includes link controllers to access external system components. There are, however, multicore architectures where one L2 cache is shared by a subset of cores (e.g., each L2 cache is shared by two cores in a quad-core, or is shared by four cores in an octa-core CPU). This is common in computing systems with additional memory levels. The external memories are often grouped in multiple levels and use different storage technologies. Typically, the first level is organized using SRAM devices, whereas the second level uses DDRAMs.

### COMBINING CPUS WITH FPGA-BASED ACCELERATORS

Several platforms provide FPGA-based hardware extensions to commodity CPUs. Examples include the Intel QuickAssist QPI-FPGA [10], IBM Netezza [11], CAPI [12], and Xilinx Zynq [13]. Other platforms, such as Refif [14], focus on vendor-independent support by providing an integration framework to interface FPGA-based accelerators with the CPU system bus using the PCI Express (PCIe) links.

![](img/55beb9162c0073b3a3d7b44f1d5873e8_32_0.png)

FIG. 2.5 Block diagram of a typical multiple CPU/multiple cores architecture (with two quad-core CPUs) using a distributed memory organization.

Other system components, such as GPIO, UART, USB interface, PCIe, network coprocessor, and power manager, are connected via a fast link possibly being memory mapped. In other architectures, however, the CPU connects to these subsystems (including memory) exclusively using fast links and/or switch fabrics (e.g., via a partial crossbar), thus providing point-to-point communication channels between the architecture components.

In computing systems requiring higher performance demands, it is common to include more than one multicore CPU (e.g., with all CPUs integrated as a CMP*). Figs. 2.5 and 2.6 illustrate two possible organizations of CMPs, one using a distributed memory organization (Fig. 2.5) and another one using a shared memory organization (Fig. 2.6).

Fig. 2.5 presents an example of a nonuniform memory access architecture (NUMA). In such systems, the distributed memories are viewed as one combined memory by all CPUs; however, access times and throughputs differ depending on the location of the memory and the CPU. For instance, the memory accesses of the CPU located at the opposite side of where the target memory is located incurs in a larger latency than the accesses to a nearby memory.

CPUs also provide parallel execution support for multiple threads per core. Systems with more than one multicore CPU have the potential to have many concurrently executing threads, thus supporting multithreaded applications.
