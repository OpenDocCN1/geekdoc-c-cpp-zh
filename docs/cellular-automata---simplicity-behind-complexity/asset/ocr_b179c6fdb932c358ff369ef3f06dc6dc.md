as required by the programmer. Last not least, the state transition function is defined by means of a simple but nevertheless fully-fledged programming language whose design is geared towards the given purpose and, in particular, features a number of non-deterministic constructs.

Our CAOS compiler exploits the restricted pattern of communication characteristic for cellular automata for generating executable code whose runtime performance is highly competitive on modern computer architectures. Fully automatic parallelisation for shared memory architectures based on OpenMP as well as for distributed memory architectures based on MPI provides easy access to high-performance computing infrastructures from state-of-the-art symmetric multiprocessors to clusters of workstations and supercomputers. All this can be harnessed with only modest (sequential) programming skills and practically no familiarity with modern computer architecture or parallel computing issues.

We currently pursue two directions of future work. Firstly, we plan to continue on the successful route to support compiler-directed parallelisation through a restricted model of computation and extend the CAOS compiler to support emerging architectures such as general purpose graphics processors. Secondly, we are working on completing the CAOS language by support for agents that substantially increase the expressiveness of CAOS for advanced simulation.

Further information on the CAOS project, including a technical report that covers compilation in-depth Greick & Penczek (2007) and a source distribution with demos for download, is available at

http://www.caos-home.org/ .

# 8. References

+   - Ackermann, J., Tangen, U., Bödekker, B., Breyer, J., Stoll, E. & McCaskill, J. (2001). Parallel random number generator for inexpensive configurable hardware cells, *Computer Physics Communications* 140: 293–302.
+   - Amarasinghe, S. (2008). (How can Programmers Conquer the Multicore Menace?, *17th International Conference on Parallel Architectures and Compilation Techniques (PACT’08)*), ACM, New York, NY, USA, pp. 133–133.
+   - Boccara, N., Goles, E., Martinez, S. & Picco, P. (eds) (1993). *Cryptography with Dynamical Systems*, Kluwer Academic Publishers, pp. 237–274.
+   - Calidonna, C. & Furnari, M. (2004). The cellular automata network compiler system: Modules and features, *International Conference on Parallel Computing in Electrical Engineering*, pp. 271–276.
+   - Canyurt, O. & Hajela, P. (2005). A cellular framework for structural analysis and optimization, *Computer Methods in Applied Mechanics and Engineering* 194: 3516–3534.
+   - Chapman, B. (2007). The Multicore Programming Challenge, *Advanced Parallel Processing Technologies*, p. 3.
+   - Chou, H., Huang, W. & Reggia, J. A. (2002). The Trend cellular automata programming environment, *SIMULATION* 78: 59–75.
+   - Conway, J. (1970). The game of life, *Scientific American*.
+   - Dagum, L. & Menon, R. (1998). OpenMP: An Industry-Standard API for Shared-Memory Programming, *IEEE Transactions on Computational Science and Engineering* 5(1).
+   - D’Ambrosio, D., Iovine, G., Spataro, W. & Miyamoto, H. (2007). A macroscopic collision model for debris-flows simulation, *Environmental Modelling & Software* 22: 1417–1436.
+   - Eckart, D. (1992). A cellular automata simulation system: Version 2.0, *ACM SIGPLAN Notices* 27.