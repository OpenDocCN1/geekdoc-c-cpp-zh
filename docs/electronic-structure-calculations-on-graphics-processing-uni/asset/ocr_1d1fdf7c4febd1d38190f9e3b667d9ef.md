![](bbox=[0.11, 0.1, 0.84, 0.31])

Figure 4.5 Organization of ERIs for Coulomb formation. Rows and columns correspond to primitive bra and ket pairs, respectively. Each ERI is colored according to the magnitude of its Schwarz bound. Data are derived from calculation on ethane molecule. Figure (a) obtained by arbitrary ordering of pairs within each angular momentum class and suffers from load imbalance because large and small integrals are computed in neighboring cells, and (b) that sorts bra and ket primitives by Schwarz contribution within each momentum class, providing an efficient structure for parallel evaluation

# Presorted |kj| pairwise quantities

![](bbox=[0.11, 0.45, 0.84, 0.8])

Figure 4.6 Schematic representation of a J-Engine kernel for one angular momentum class, for example, (ss|ss). Cyan squares represent significant ERI contributions. Sorted bra and ket vectors are represented by triangles to the left and above the grid. The path of a 2 x 2 block as it sweeps across the grid is shown in orange. The final reduction across rows of the block is illustrated within the inset to the right