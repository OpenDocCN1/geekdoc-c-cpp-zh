
- [43] Kun Y, Shumao O, Hsiao-Hwa C. On effective offloading services for resource-constrained mobile devices running heavier mobile internet applications. IEEE Commun Mag 2008;46(1):56–63.

- [44] Hill MD, Marty MR. Amdahl’s law in the multicore era. IEEE Comput 2008;41:33–8.

- [45] Cassidy AS, Andreou AG. Beyond Amdahl’s law: an objective function that links multiprocessor performance gains to delay and energy. IEEE Trans Comput 2012;61(8):1110–26.

- [46] Saha S, Ravindran B. An experimental evaluation of real-time DVFS scheduling algorithms. In: Proceedings of the 5th annual international systems and storage conf. (SYSTOR 12). New York, NY: ACM; 2012. Article 7. 12 pages.

- [47] Bambaci M, Marinoni M, Aydin H, Buttazzo G. Energy-aware scheduling for real-time systems: a survey. ACM Trans Embed Comput Syst 2016;15(1):1–34.

- [48] Melhem R, Graybill R, editors. Power aware computing. Norwell, MA, USA: Kluwer Academic/Plenum Publishers; May, 2002.

- [49] Zhang L, Tiwana B, Qian Z, Wang Z, Dick RP, Morley Mao Z, et al. Accurate online power estimation and automatic battery behavior based power model generation for smartphones. In: Proc. of the 8th Int. conf. on hardware/software codesign and system synthesis (CODES+ISSS 2010), Scottsdale, AZ, October 24–28; 2010. p. 105–14.

- [50] Dong M, Zhong L. Self-constructive high-rate system energy modeling for battery-powered mobile systems. In: Proceedings of the 9th international conference on Mobile systems, applications, and services (MobiSys’11). New York, NY: ACM; 2011. p. 335–48.

- [51] Williams S, Waterman A, Patterson D. Roofline: an insightful visual performance model for multicore architectures. Commun ACM 2009;52(4):65–76.

## Controlling the design and development cycle

### 3.1 INTRODUCTION

The availability of rich programming and visualization environments has allowed the development of high-performance embedded systems using the so-called fourth-generation programming languages such as MATLAB [1] and Simulink [2]. This development approach, in its basic form, starts with a model specification where end-to-end functions are verified taking into account internal feedback loops and specific numeric variable precision requirements. Once this first functional specification is complete, designers and developers can focus on meeting additional specification requirements. These requirements typically involve performance and/or energy goals, and in some extreme cases where Application-Specific Integrated Circuits (ASICs) are sought, design area constraints for specific clock rate ranges. To keep design options open for later phases of the implementation of a design, it is common to encapsulate expensive arithmetic operations as abstract operators at behavioral level. Even for integer value representations, there is a wide variety of implementations for basic operators such as addition and multiplication. This exploration of suitable operator implementations is largely guided by performance factors such as clock rate and timing.

Common design space exploration (DSE) approaches lack the language mechanisms that allow designers to convey specific target requirements, as well as the lack of tools that can use the information conveyed by different stages of the design flow to effectively explore and derive efficient design solutions. While there are tools that perform hardware DSE, they tend to be tightly integrated in a hardware synthesis toolchain (e.g., [3]), or only allow the exploration using a limited set of parameters (such as the unroll loop factor), and thus do not provide the flexibility to explore alternative and potentially more optimized solutions. Other tools focus exclusively on the exploration of arithmetic precision concerns to meet specific algorithmic-level requirements (e.g., noise level).

To make matters worse, these hardware designs often need to be certified for timing requirements and integrated in the context of complex systems-on-a-chip (SoC), in many cases executing under the supervision of a Real-Time Operating System (RTOS). The validation and certification of such systems is extremely complex. While specific hardware designs can meet stringent timing targets, their inclusion in real-time systems requires a perfect synchronization of the timing and the priorities of multiple threads on computing cores with nondeterministic execution. It is common for designers in this case to settle for the worst-case execution time scenarios, which often leads to an increase in resource usage and to suboptimal energy-wise design solutions.

Most of the complexity in designing these systems stems from the fact that it is extremely hard to trace the original project design goals, such as overall energy or timing requirements, to individual design components. As it is common in many areas of engineering, designers organize their solutions into a hierarchy of logically related modules. Tracing and propagating down these requirements across the boundaries of the hierarchy is extremely complex as multiple solutions may exhibit feasible individual design points but when put together, the combined design may not meet its requirements. Thus, exposing requirements at a higher design level and allowing a tool to understand how these requirements can be translated up and down the module hierarchy is a critical aspect of modern high-performance embedded systems design.

In the remainder of this chapter, we address this need using a series of design specifications and examples assuming that readers are familiar with imperative programming languages such as C and MATLAB.

### 3.2 SPECIFICATIONS IN MATLAB AND C: PROTOTYPING AND DEVELOPMENT

The language used to program an application, a model, an algorithm, or a prototype greatly influences the effort required to efficiently map them to the target computing system. High-level abstraction languages typically promote design productivity while also increasing the number of mapping solutions of the resulting designs without requiring complex code restructuring/refactoring techniques. In the following sections, we use MATLAB [1] and C [4] programming languages to describe the prototyping and the programming development stages.

### 3.2.1 ABSTRACTION LEVELS

Programming languages such as C are usually considered low level as algorithms are implemented using constructs and primitives closer to the target processor instructions, since most operations, such as arithmetic, logic, and memory accesses, are directly supported by the microprocessor instruction set. For instance, if a low-level programming language does not directly support matrix multiplication or sort operations (either natively or through a library), developers are forced to provide their own implementations using low-level operations. Such low-level implementations can constrain the translation and mapping process of the computation defined at this level of abstraction, since the compiler is naturally limited to a narrow translation and mapping path, leaving relatively little room for high-level optimizations.

Alternatively, developers may use programming languages with higher levels of abstraction which natively support high-level operations such as matrix

```
D=A*B*C;
```

```
D=mult(mult(A,B),C);
```

FIG. 3.1 Simple MATLAB example (A); C example considering the existence of the function “mult” (B).

multiplication and sorting. This is the case of MATLAB [11], Octave [5], and Scilab [6] which natively support a wide range of linear algebra matrix operations (overloaded with common arithmetic operators on scalars). Fig. 3.1A presents an example of a MATLAB statement using matrix multiplications. This native support makes the code simpler and more concise, allowing the compiler to easily recognize the operation as a matrix multiplication, and thus associate the best algorithm to implement it (e.g., based on the knowledge whether the matrices are sparse or not). Fig. 3.1B presents a possible equivalent C statement considering the existence of the “mult” function and a data structure to store matrices (including also the size and shape of the matrix). For a compiler to recognize that the “mult” function is an actual implementation of a matrix multiplication operation, it requires a mechanism for programmers to convey that information, e.g., through code annotations.1

The abstractions provided by matrix-oriented programming languages, such as MATLAB, are helpful in many situations. Herein we use the edge detection application provided by the UTDS benchmark repository [7], and compare several MATLAB implementations against the corresponding C implementations available in this repository, highlighting possible mappings.

The edge detection application uses a function to convolve two input matrices. Fig. 3.2 presents an excerpt of a possible MATLAB code to implement the 2D convolution. In this example, the natively supported dot product “.*” is used to calculate the multiplications of the pixels in a window of K x K size with the kernel matrix. Fig. 3.3 shows a MATLAB code, very similar to the C code present in the repository, which does not use the “.*” operator.

```
% Convolve the input image with the kernel.
for r = 0:1:(N-K)
    for c = 0:1:(N-K)
        sum = sum(input_image(r+1:r+K,c+1:c+K).*kernel));
        output_image(r+dead_rows1,c+dead_cols1) = (sum / normal_factor);
    end
end
```

FIG. 3.2 MATLAB code using the native dot product operation for a 2D convolution of an input image with a kernel (matrix of coefficients).

1 Note that languages like C++ support operator overloading, which would allow the code to be as simple as the MATLAB code presented in Fig. 3.1, however the developer must still provide an implementation or use a domain-specific library.
