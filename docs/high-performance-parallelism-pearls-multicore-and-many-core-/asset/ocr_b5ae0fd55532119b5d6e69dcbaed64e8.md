```
Offload to transfer sequences S1 and S2;
Offload to allocate block-level GW, GV and GD buffers on the coprocessor;
for (d = 0; d < Rmpi+Cmpi-1; ++d) {
    sMpiRow = max(0,d-Cmpi+1);
    eMpiRow = min(d,Rmpi-1);
    sMpiCol = d-eMpiRow;
    eMpiCol = d-sMpiRow;
    currMpiCol = mpiRank;
    currMpiRow = d-currMpiCol;
    MPI_Barrier(MPI_COMM_WORLD);
    if (currMpiCol>=sMpiCol && currMpiCol<=eMpiCol) {
        #pragma offload target (mic: micIndex) in/out
        variable list{
            Invoke the Xeon Phi kernel;
            Calculate the local maximum score lMaxScore;
        }
    }
    Communicate intermediate data using MPI_Isend and
    MPI_Irecv;
}
MPI_Reduce over lmaxScore to get overall optimal score;
```

# FIGURE 4.7

Pseudocode of the MPI parallelization (refer to function _alignDistributed()_ in AlignCoreTiling.cpp).

| Seq. | Length | Accession No. | Genome definition |
|---|---:|---|---|
| S4.4 | 4,411,532 | NC_000962.3 | *Mycobacterium tuberculosis* H37Rv |
| S4.6 | 4,641,652 | NC_000913.3 | *Escherichia coli* K12 MG1655 |
| S23 | 23,011,544 | NT_033779.4 | *Drosophila melanogaster* chr. 2L |
| S33 | 32,799,110 | BA000046.3 | *Pan troglodytes* DNA chr. 22 |
| S42 | 42,034,648 | NC_019481.1 | *Ovis aries* breed Texel chr. 24 |
| S50 | 50,073,674 | NC_019478.1 | *Ovis aries* breed Texel chr. 21 |

# FIGURE 4.8

Information of the genome sequences used.

We first evaluate the scalability of the tiled approach with respect to a varying number of threads on a single coprocessor using the S4.4 and S4.6 sequence pair, where we start from T = 60 threads and increment T until reaching 236 (equals to the value returned by omp_get_num_procs()). The speed gradually increases as T grows, albeit having some tiny fluctuations, and eventually reaches the maximum at T = 236 (see Figure 4.9).