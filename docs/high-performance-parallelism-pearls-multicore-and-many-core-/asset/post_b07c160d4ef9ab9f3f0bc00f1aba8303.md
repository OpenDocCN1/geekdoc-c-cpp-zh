
![](img/16cb41208935c5f22dd1044f03f2e31b_289_0.png)

**FIGURE 13.10**

Coprocessor-side results for the *None* affinity pattern.

![](img/16cb41208935c5f22dd1044f03f2e31b_289_1.png)

**FIGURE 13.11**

Coprocessor-side results for the *Scatter* affinity pattern.

## CHAPTER 13 EXPLORING USE OF THE RESERVED CORE

![](img/16cb41208935c5f22dd1044f03f2e31b_290_0.png)

**FIGURE 13.12**

Coprocessor-side results for the *Selective* affinity pattern.

### HOST-SIDE RESULTS

Figure 13.13 visualizes results from the 16 simulations performed on the host-side. Below are notes regarding host-side results:

![](img/16cb41208935c5f22dd1044f03f2e31b_291_0.png)

**FIGURE 13.13**

Host-side results.

- Marks correspond to the average elapsed execution time per compute timestep (in seconds).
- PPT corresponds to the ratio of mesh patches to threads. Note that each thread is not guaranteed to compute this number of mesh patches.
- Over 10 identical host-side simulations, there existed not more than a 3.35% difference in performance between two identical runs.
- There existed a 10.14% difference in performance between the fastest and slowest run configurations.

### FURTHER ANALYSIS

Addressing comparisons between architectures first, the two Xeon processors outperformed the single Xeon Phi coprocessor. Specifically, there existed a 39.43% difference in performance between the fastest-run configurations for each architecture. Regarding accuracy, simulation results computed by each architecture were identical to one another up to a relative tolerance of 1E-15 digits.

Given this has been a naive port of our CPU-based algorithm, these results are encouraging as they leave ample opportunity to shift performance in favor of the coprocessor. Having not yet adequately pursued such optimizations, effective memory management and vectorization are believed to be the factors attributing to these differences. Supporting this conclusion, version 15.0 compiler optimization reports and experimentation with simpler vectorization approaches (e.g., SIMD directives) suggest that little, if any, vectorization is being achieved. Further, predominantly 100% core usage during compute timesteps suggests that thread-level parallelism is sufficient.

Turning to observations, performance disparities among coprocessor-based results deserve attention. As more hardware TPPC were utilized, the difference in performance between fastest and slowest run configurations increased. This is likely attributed to the sharing of the 512 kB per core L2 cache among four hardware threads. Though it offered better run times, use of more hardware TPPC further divided the amount of L2 cache available to a given thread. This resulted in increased sensitivity to simulation mesh decomposition.

Moving forward, the overarching takeaway from these native execution-based experiments is that no one thread placement strategy dominated performance. For similar algorithms, this suggests that time may be best spent by first pursuing more favorable areas of optimization.

Returning to the question motivating this work, our fastest run configurations utilized the 61st core. Further, performance was not profoundly impacted when explicitly oversubscribing the coprocessor operating system thread. For similar algorithms, this suggests that use of the 61st core may be both forgiving and capable of offering modest performance improvements.

### SUMMARY

These experiments have helped establish valuable baselines for our future efforts addressing both single-node performance and scalability. Perhaps more important, they have also provided valuable insight regarding potential challenges and areas to address as we strive to achieve performance with the Intel Xeon Phi products. When considering these results, it is important to remember that we have examined native execution exclusively. When operating in offload mode, Intel guidance is to refrain from using the reserved core as it actively supports offloading.

### ACKNOWLEDGMENTS

These research efforts have been supported by the National Nuclear Security Administration’s PSAAP II project. This work utilized equipment donations to the University of Utah’s Intel Parallel Computing Center (IPCC) at the SCI Institute. We would also like to thank Aaron Knoll, IPCC Principal Investigator, for his assistance along the way.

### FOR MORE INFORMATION

- To learn more about the UCF, please refer to the link below:
  http://www.uintah.utah.edu/

- To explore Uintah and C-SAFE-related publications, please refer to the link below:
  http://www.uintah.utah.edu/pubs/pubs.html

- To learn more about radiative heat transfer and the discrete ordinates method-based radiation model, please refer to the publication referenced below:
  Spinti, J.P., Thornock, J.N., Eddings, E.G., Smith, P.J., Sarofim, A.F., 2008. Heat transfer to objects in pool fires. In: Transport Phenomena in Fires. WIT Press, Southampton, UK.

- To learn more about the RMCRT-based radiation model, please refer to the publication referenced below:
  Humphrey, A., Meng, Q., Berzins, M., Harman, T., 2012. Radiation modeling using the Uintah heterogeneous CPU/GPU runtime system. In: Proceedings of the 1st Conference of the Extreme Science and Engineering Discovery Environment (XSEDE12). ACM.

- To download the version of Uintah used for this chapter, please refer to the link below:
  http://lotsofcores.com/downloads

- To learn more about installing and using the UCF, please refer to the link below:
  http://uintah-build.sci.utah.edu/trac/wiki

## 14 HIGH PERFORMANCE PYTHON OFFLOADING

Jussi Enkovaara*, Michael Klemm†, Freddie Witherden‡

CSC, Finland*  
Intel Corporation, Germany†  
Imperial College of London, United Kingdom‡

Python applications, running on a host processor, can use the pyMIC module to load and execute code on the Intel® Xeon Phi™ coprocessor. This chapter demonstrates the usage of pyMIC within two high performance computing (HPC) applications, GPAW and PyFR. This chapter also reviews the design, implementation, and performance of pyMIC.

It is worth noting that Python code can be run directly on a coprocessor using PyPhi. That is not covered in this chapter but there are references at the end of this chapter for PyPhi.

The pyMIC offload model supports management of data transfers and offloading at various levels of control. Programmers can start from a naïve, simplistic solution and incrementally increase the level of control to gain additional performance or extend the offloaded code regions. The current version of pyMIC requires the programmer to write the offload kernels in C, C++, or Fortran, and compile them for native coprocessor execution. In contrast to the native version of Python that ships with the Intel® Manycore Platform Software Stack (MPSS), Python code runs on the host while the offloaded code relies on native execution and multithreading for maximum performance. At the end of this chapter, the “For more information” section contains links for pyMIC (offload from Python to a coprocessor) and PyPhi (run Python on a coprocessor).

### BACKGROUND

Python is one of the most commonly used programming languages within the computing industry. Throughout its existence, Python has proven to be an easy-to-use, elegant scripting language that allows for rapid prototyping and development of highly flexible software. Python has gained substantial popularity in the HPC community. Add-on packages such as Numpy and SciPy provide efficient implementations of containers for bulk floating-point data and typical number-crunching algorithms. Extensions like these usually use compiled languages such as C or Fortran for performance. Therefore, Python can provide the performance needed for widespread HPC usage.

GPAW is one prominent example of a Python HPC application. It is a versatile open-source software package for various electronic structure simulations of nanostructures and materials science research problems. GPAW is based on the density-functional theory (DFT) and time-dependent DFT, and it offers several options for discretizing the underlying equations, such as uniform real-space grids, plane waves, and localized atomic orbital basis. GPAW can be run on wide variety of HPC systems, and depending on the input data, simulations can scale up to tens of thousands of traditional CPU
