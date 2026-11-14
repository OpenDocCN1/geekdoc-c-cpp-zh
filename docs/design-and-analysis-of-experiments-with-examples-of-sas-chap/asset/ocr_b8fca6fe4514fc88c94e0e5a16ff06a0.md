# 10.8 Blocked Response Surface (BRS) Designs

When experimental units are not homogeneous, it is always advantageous to group them into more homogeneous blocks and use a blocked experimental design. Earlier it was mentioned that the three-factor central composite designs could be run in two blocks; the factorial portion plus three center points in one block, and the axial portion and remaining center points in the other block. This is actually an example of an incomplete block design, like those described in Chapter 7, since not all the treatment combinations are represented in each block. It is possible to create an incomplete block design out of any response surface design so that the coefficients can be estimated more precisely.

Standard response surface designs such as the central composite designs (CCDs) and Box-Behnken designs (BBDs) have been blocked in a way that the blocks are orthogonal to the coded factor levels, squares of coded factor levels, and interactions among coded factor levels. In this way the least squares estimates of the parameters of the general quadratic model are not correlated with the block effects and these standard designs are 100% $D_s$ efficient as described in Section 7.8.1. The example described earlier, where the three-factor central composite design was blocked into two blocks with block sizes 11 and 9, is not 100% $D_s$ efficient. In order to achieve 100% efficiency, some additional restrictions must be made in terms of the number of blocks, the block sizes, and the axial radius. This will affect the distribution of the variance of a predicted value over the design region, and a compromise must be made. Table 10.7 shows the number of blocks and block sizes for orthogonally blocked CCDs and BBDs with $k = 2$ to 5 factors.

Table 10.7 Number of Blocks and Block Sizes for Orthogonally Blocked CCD and BBD Designs

| Number Factors | CCD No. Blocks | CCD Block Sizes | BBD No. Blocks | BBD Block Sizes |
| :--- | :--- | :--- | :--- | :--- |
| 2 | 2 | 7, 7 | | |
| 3 | 3 | 6, 6, 8 | | |
| 4 | 3 | 10, 10, 10 | 3 | 9, 9, 9 |
| 5 | 2 | 22, 11 | 2 | 23, 23 |

These designs can be created easily with the SAS ADX tool. It will automatically use the optimal block size and axial radius. To create a blocked response