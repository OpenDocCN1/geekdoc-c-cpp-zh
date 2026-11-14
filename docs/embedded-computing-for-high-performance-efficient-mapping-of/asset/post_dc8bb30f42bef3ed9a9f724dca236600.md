
effectively used as a textbook for an advanced electrical, computer engineering, and computer science course focused on the development of high-performance embedded systems.

We are very conscious about the difficulty of presenting in a single book, and in a cohesive form, all the topics we consider important about the process of mapping computations to high-performance embedded computing platforms. However, we believe that the topics presented in this book should be mastered by the next generation of developers.

We hope you enjoy reading this book, and that it contributes to increasing your knowledge about developing efficient programs on high-performance embedded platforms, and that it serves as an inspiration to your projects.

João M.P. Cardoso
José Gabriel F. Coutinho
Pedro C. Diniz

## Acknowledgments

We would like to acknowledge Walid Najjar, from the University of California Riverside, United States, for reading a previous version of Chapter 2 and for providing important feedback and suggestions for improving it.

We would like to acknowledge all the members of the SpeCS group for their suggestions and discussions, namely, João Bispo, Tiago Carvalho, Pedro Pinto, Luís Reis, and Ricardo Nobre. We are also grateful to all of them for reviewing previous versions of this book’s chapters and for their valuable feedback that undoubtedly helped to improve the book.

Students of the PhD Program on Informatics Engineering (ProDEI) of the Faculty of Engineering of the University of Porto (FEUP) have also been a source of helpful feedback regarding some of the contents of this book, as earlier revisions from selected chapters were used as part of the class material for the High-Performance Embedded Computing (CEED) course.

In addition, we would also like to acknowledge the support given by the following companies. Xilinx Inc. (United States) provided, through their University Program, FPGA-based development boards and software licenses including Vivado and Vivado HLS. ARM Ltd. (United Kingdom) provided, through its ARM University Program, a sample ARM Lab-in-a-Box on Efficient Embedded Systems Design and Programming.

João M.P. Cardoso would like to acknowledge the support of the Department of Informatics Engineering of the Faculty of Engineering of the University of Porto, of INESC TEC, and the partial support provided by the following research projects: ANTEAR (H2020 FET-HPC-1-2014, ref. 671623), CONTEXTWA (FCT PTDC/EEI-SCR/6945/2014), and TECA4Growth—RL1 SMILES (NORTE-01-0145-FEDER-000020). José Gabriel F. Coutinho would like to acknowledge the support of Wayne Luk, the Department of Computing at Imperial College London, United Kingdom, and the partial support of the EXTRA research project (H2020 FET-HPC-1-2014, ref. 671653).

We would like to thank Elsevier for giving us the opportunity to write this book. A warm acknowledgment and appreciation to Lindsay Lawrence, our Elsevier editor, for her belief in this project since the very beginning, as well as her direction which helped us finish this book project.

Last but not least, we would like to thank our families for their support and understanding for the countless hours we had to devote to this book.

## Abbreviations

- ACPI advanced configuration and power interface. A standard promoted by Intel, Microsoft, and Toshiba
- ADC analog-to-digital converter
- AMD advanced micro devices
- AOP aspect-oriented programming
- API application programming interface
- ARM advanced RISC machines
- ASIP application-specific instruction-set processor
- AST abstract syntax tree
- AVX advanced vector extensions
- BRAM block RAM
- CD computing device
- CDFG control/data flow graph
- CFG control flow graph
- CG call graph
- CGRA coarse-grained reconfigurable array
- CISC complex instruction set computer
- CLB configurable logic block
- CMP chip multiprocessor
- COTS commercial off-the-shelf
- CPA critical path analysis
- CPU central processing unit
- CU computing unit
- DAC digital-to-analog converter
- DAG directed acyclic graph
- DDG data dependence graph
- DDR double data rate
- DFG data flow graph
- DFS dynamic frequency scaling
- DPM dynamic power management
- DRAM dynamic random-access memory (RAM)
- DSE design space exploration
- DSL domain-specific language
- DSP digital signal processing
- DVFS dynamic voltage and frequency scaling
- DVS dynamic voltage scaling
- EDA electronic design automation
- EDP energy delay product
- EEMBC embedded microprocessor benchmark consortium
- FMA fused multiply-add

| Abbreviation | Definition |
|---|---|
| FPGA | field-programmable gate array |
| FPS | frames per second |
| FSM | finite state machine |
| GA | genetic algorithm |
| GCC | GNU compiler collection (originally named GNU C Compiler) |
| GPGPU | general-purpose graphics processing unit (also known as general-purpose computing on graphics processing unit) |
| GPIO | general-purpose input/output (IO) |
| GPU | graphics processing unit |
| HLS | high-level synthesis |
| HPC | high-performance computing |
| HPECC | high-performance embedded computing |
| HPPF | high performance Fortran |
| ICC | Intel C/C++ compiler |
| IDE | integrated design environment |
| ILP | instruction-level parallelism or integer-linear programming |
| IO | input/output |
| IOB | input/output block |
| IR | intermediate representation |
| ISA | instruction set architecture |
| LDG | loop dependence graph |
| LLVM | low level virtual machine |
| LOC | lines of code |
| MIC | many integrated core |
| MPI | message passing interface |
| MPSoC | multiprocessor SoC (system-on-a-chip) |
| NFRs | nonfunctional requirements |
| NUMA | nonuniform memory access |
| OpenACC | open accelerators |
| OpenCL | open computing language |
| OpenMP | open multiprocessing |
| PC | personal computer |
| PCI | peripheral component interconnect |
| PCIe | peripheral component interconnect express |
| PE | processing element |
| QoE | quality of experience |
| QoS | quality of service |
| QPI | Intel QuickPath interconnect |
| RAM | random-access memory |
| RISC | reduced-instruction set computer |
| ROM | read-only memory |
| RTOS | real-time operating system |
| SA | simulated annealing |

- SDR single data rate
- SDRAM synchronous dynamic random-access memory
- SIMD single instruction, multiple data
- SIMT single instruction, multiple thread
- SLP subword-level parallelism
- SMT simultaneous multithreading
- SNR signal-to-noise ratio
- SoC system-on-a-chip
- SPIR standard portable intermediate representation
- SPM ScratchPad memory
- SPMD single program, multiple data
- SRAM static random-access memory (RAM)
- SSA static single assignment
- SSE streaming SIMD extensions
- TG task graph
- TMR triple-module redundancy
- UART universal asynchronous receiver/transmitter
- UMA uniform memory access
- UML unified modeling language
- USB universal serial bus
- VL vector register length
- WCET worst-case execution time

## Introduction

### 1.1 OVERVIEW

Embedded computing systems permeate our lives from consumer devices, such as smartphones and game consoles, to less visible electronic devices that control, for instance, different aspects of a car’s operation. Applications executing on current embedded systems exhibit a sophistication on par with applications running on desktop computers. In particular, mobile devices now support computationally intensive applications, and the trend points to a further increase in application complexity to meet the growing expectations of their users. In addition to performance requirements, energy and power consumption are of paramount importance for embedded applications, imposing restrictions on how applications are developed and which algorithms can be used.

Fig. 1.1 presents a generic and simplified architecture of an embedded computing system. A key distinguishing feature of an embedded system lies in the diversity of its input and output devices, generically known as sensors and actuators, fueled by the need to customize their use for each specific domain. In this diagram, we have a bus-based computing core system consisting of a RAM, ROM, and a processor unit. The computing core system interacts with its physical environment via a set of actuators and sensors using Analog-to-Digital (ADC) and Digital-to-Analog (DAC) converter units. At the software level, the operating system and application software are stored in ROM or in Flash memory, possibly running a customized version of the Linux operating system able to satisfy specific memory and/or real-time requirements [1] and can support additional software components, such as resident monitors, required by the embedded system.

Developing applications in heavily constrained environments, which are typical targets of embedded applications, requires considerable programming skills. Not only programmers need to understand the limitations of the underlying hardware and accompanying runtime support, but they must also develop solutions able to meet stringent nonfunctional requirements, such as performance. Developing these interdisciplinary skills is nontrivial and not surprisingly there is a lack of textbooks addressing the development of the relevant competences. These aptitudes are addressed when developing and mapping high-performance applications to current and emerging embedded computing systems. We believe that this textbook is a step in this direction.
