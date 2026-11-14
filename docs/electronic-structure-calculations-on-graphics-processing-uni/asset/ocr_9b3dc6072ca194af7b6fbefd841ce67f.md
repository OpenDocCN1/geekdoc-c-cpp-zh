programming interface. Finally, good performance has been demonstrated on one of the largest GPU based supercomputers worldwide. To further benefit from the GPU compute power, new message passing algorithms are being developed.

# Acknowledgments

The authors acknowledge Urban Borštnik, Florian Schiffmann, Florian Thöle, Jinwoong Cha, Valéry Weber, Christine Pousa Ribeiro, Iain Bethune (EPCC), Chris Mundy (PNNL), Nikolay Markovskiy (NVIDIA), Neil Stringfellow (CSCS), Gilles Fourestey (CSCS), Alfio Lazzaro (Cray), and Roberto Ansaloni (Cray) for their help with the implementation, discussions, and applications. J.V. acknowledges financial support by the European Union FP7 in the form of an ERC Starting Grant under contract no. 277910. Calculations were enabled by a grant of the Swiss National Supercomputing Centre (CSCS) under project IDs s244, 8441, and 05n3. In preparation of this research, resources of the Oak Ridge Leadership Computing Facility at the Oak Ridge National Laboratory, which is supported by the Office of Science of the U.S. Department of Energy under Contract No. DE-AC05-00OR22725, have been used. The research leading to these results has received funding from the Swiss University Conference through the High Performance and High Productivity Computing (HP2C) Programme.

# References

+   1. Goedecker, S. (1999) Linear scaling electronic structure methods. *Rev. Mod. Phys.*, **71** (4), 1085–1123.
+   2. Bowler, D.R. and Miyazaki, T. (2012) O(N) methods in electronic structure calculations. *Rep. Prog. Phys.*, **75** (3), 036503.
+   3. The CP2K developers group. 2013. CP2K is freely available from: `http://www.cp2k.org/` (accessed 18 September 2015).
+   4. VandeVondele, J., Borštnik, U. and Hutter, J. (2012) Linear scaling self-consistent field calculations with millions of atoms in the condensed phase. *J. Chem. Theory Comput.*, **8** (10), 3565–3573.
+   5. Higham, N.J. (2008) *Functions of Matrices: Theory and Computation*. Society for Industrial and Applied Mathematics, Philadelphia, PA.
+   6. Beyklky, G., Coul, N. and Mohlenkamp, M. (1999) Fast spectral projection algorithms for density-matrix computations. *J. Comput. Phys.*, **152** (1), 32–54.
+   7. Nemeth, K. and Scuseria, G. (2000) Linear scaling density matrix search based on sign matrices. *J. Chem. Phys.*, **113** (15), 6035–6041.
+   8. Palser, A. and Manolopoulos, D. (1998) Canonical purification of the density matrix in electronic-structure theory. *Phys. Rev. B*, **58** (19), 12704–12711.
+   9. Niklasson, A.M.N., Tymczak, C.J. and Challacombe, M. (2003) Trace resetting density matrix purification in O(N) self-consistent-field theory. *J. Chem. Phys.*, **118** (19), 8611–8620.
+   10. Li, X., Nunes, R. and Vanderbilt, D. (1993) Density-matrix electronic-structure method with linear-system-size scaling. *Phys. Rev. B*, **47** (16), 10891–10894.
+   11. Helgaker, T., Larsen, H., Olsen, J. and Jørgensen, P. (2000) Direct optimization of the AO density matrix in Hartree-Fock and Kohn–Sham theories. *Chem. Phys. Lett.*, **327** (5–6), 397–403.
+   12. Shao, Y., Saravanan, C., Head-Gordon, M. and White, C. (2003) Curvy steps for density matrix-based energy minimization: application to large-scale self-consistent-field calculations. *J. Chem. Phys.*, **118** (14), 6144–6151.
+   13. Salak, P., Host, S., Thøgersen, L., Jørgensen, P., Manninen, P., Olsen, J. *et al.* (2007) Linear-scaling implementation of molecular electronic self-consistent field theory. *J. Chem. Phys.*, **126** (11), 114110.