and mapping tools to exploit heterogeneous architectures and hardware accelerators effectively. Specifically, the book considers the support of data and task parallelism provided by multicore architectures and the use of GPUs and FPGAs for hardware acceleration (via C and OpenCL code).

In the description of the various topics, it has been our intention to focus on concepts rather than on actual implementations using current technologies to avoid making the contents of this book obsolete in the short term. Still, we provide over the various chapters “sideboxes” with specific examples to connect the concepts to current implementations or technologies. In addition, we also provide complementary online material regarding each chapter, including in many cases complete source code examples, highlighting in more depth the use of the concepts using today’s technologies.

# 1.7 COMPLEMENTARY BIBLIOGRAPHY

Although there exists a number of technical textbooks (e.g., [4,13–15]) supporting embedded system courses, the topics covered in this book are only partially addressed by other volumes. Conversely, other texts, such as Refs. [16–18], cover complementary topics not addressed in this text.

The texts about compilation techniques for high-performance systems [14], embedded computing [19], performance tuning [20], high-performance computing [21], the AOP approach provided by LARA [22], hardware/software codesign [23], and reconfigurable computing [5,24], also address topics relevant to the topics addressed in this book and can thus serve as complementary bibliography.

Other relevant texts in the context of optimizations for high-performance computing (HPC) include the books from Crawford and Wadleigh [25], from Garg and Sharapov [26], and from Gerber et al. [27].

# 1.8 DEPENDENCES IN TERMS OF KNOWLEDGE

In order to follow the topics addressed in this book, readers should have basic knowledge on high-level programming, data structures and algorithms, digital systems, computer architecture, operating systems, and compilers. Fig. 1.5 illustrates the dependences between these topics in general, and high-performance embedded computing (HPEC) in particular. Topics related to parallel computing and reconfigurable computing are seen as complementary, and readers with those skills are able to work on more advanced HPEC projects and/or to focus their work on specific technologies.