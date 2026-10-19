
![](img/bccda43674e4a93dee81c749eba8d2f7_264_0.png)

**Figure 10.10** A representation of the lattice in a 2D rectangular space upon which Laplace’s equation is solved using a finite difference approach. The lattice sites with white centers correspond to the boundary of the physical system, upon which boundary conditions must be imposed for a unique solution. The large circles in the middle of the lattice represent the algorithm used to solve Laplace’s equation in which the potential at the point $(x,y)=(i,j)\Delta$ is set to the average of the potential values at the four nearest-neighbor points.

When thinking of parallelizing this program, we note an algorithm being applied to a space of data points, in which case we can divide the domain into subspaces and assign each subspace to a different processor. This is domain decomposition or data parallelism. In essence, we have divided a large boundary-value problem into an equivalent set of smaller boundary-value problems that eventually get fit back together. Often extra storage is allocated on each processor to hold the data values that get communicated from neighboring processors. These storage locations are referred to as *ghost cells, ghost rows, ghost columns, halo cells,* or *overlap areas*.

Two points are essential in domain decomposition: (i) Load balancing is critical, and is obtained here by having each domain contain the same number of lattice points. (ii) Communication among the processors should be minimized because this is a slow process. Clearly the processors must communicate to agree on the potential values at the domain boundaries, except for those boundaries on the edge of the box that remain grounded at 0 V. But because there are many more lattice sites that need computing than there are boundaries, communication should not slow down the computation severely for large lattices.

To see an example of how this is carried out, the serial code `poisson__1d.c` solves Laplace’s equation in 1D, and `poisson__parallel__1d.c` solves the same 1D equation in parallel (codes courtesy of Michel Vallieres). This code uses an accelerated version of the iteration algorithm using the parameter $\Omega$, a separate method for domain decomposition, as well as ghost cells to communicate the boundaries.

## Listing 10.3 laplace.c Serial solution of Laplace's equation using a finite difference technique.

```
/* laplace.c: Solve Laplace equation with finite differences */

#include <stdio.h>
#define max 40                 /* number of grid points */
main()
{
    double x, p[max][max];
    int i, j, iter, y;
    FILE *output;               /* save data in laplace.dat */
    output = fopen("laplace.dat","w");
    for (i=0; i<max; i++)       /* clear the array */
    { for (j=0; j<max; j++) p[i][j] = 0;}
    for(i=0; i<max; i++) p[i][0] = 100.0;   /* p[i][0] = 100 V */
    for (iter=0; iter<1000; iter++)         /* iterations */
    { for(i=1; i<(max-1); i++)               /* x-direction */
      { for (j=1; j<(max-1); j++)            /* y-direction */
        { p[i][j] = 0.25*(p[i+1][j]+p[i-1][j]+p[i][j+1]+p[i][j-1]); }
      }
    }
    for (i=0; i<max ; i++)          /* write data gnuplot 3D format */
    { for (j=0; j<max; j++)
      { fprintf(output,"%f\n",p[i][j]); }
      fprintf(output,"\n");       /* empty line for gnuplot */
    }
    printf("data stored in laplace.dat\n");
    fclose(output);
}
```

## 10.14.1

## Domain Decomposition Exercises

- 1. Get the serial version of either laplace.c or laplace.f running.
- 2. Increase the lattice size to 1000 and determine the CPU time required for convergence to six places. Make sure that this is the actual run time and does not include any system time. (You can get this type of information, depending upon the operating system, by inserting timer calls in your program.)
- 3. Decompose the domain into four subdomains and get an MPI version of the code running on four compute nodes. [Recall, we give an example of how to do this in the Codes directory with the serial code poisson_1d.c and its MPI implementation, poisson_parallel_1d.c (courtesy of Michel Vallieres).]
- 4. Convert the serial code to three dimensions. This makes the application more realistic, but also more complicated. Describe the changes you have had to make.
- 5. Decompose the 3D domain into four subdomains and get an MPI version of the code running on four compute nodes. This can be quite a bit more complicated than the 2D problem.
- 6. Conduct a weak scaling test for the 2D or 3D code.
- 7. Conduct a strong scaling test for the 2D or 3D code.

![](img/bccda43674e4a93dee81c749eba8d2f7_267_0.png)

cost in both time and money would be for Windows!) and utilizes the hardware by running a distributed memory MPI with C, C++, and Fortran90 compilers. Blue Gene has three separate communication networks (Figure 10.13). At the heart of the network is a 3D torus that connects all the nodes, for example, Figure 10.13 a shows a sample torus of 2 × 2 × 2 nodes. The links are made by special link chips that also compute; they provide both direct neighbor–neighbor communications and cut-through communication across the network. The result of this sophisticated communications network is that there are approximately the same effective bandwidth and latencies (response times) between all nodes. However, the bandwidth may be affected by interference among messages, with the actual latency also depending on the number of hops to get from one node to another.4) A rate of 1.4 Gb/s is obtained for node-to-node communication. The collective network in Figure 10.13b is used for collective communications among processors, such as a broadcast. Finally, the control and gigabit ethernet network (Figure 10.13c) is used for I/O to communicate with the switch (the hardware communication center) and with ethernet devices.

The computing heart of Blue Gene is its integrated circuit and the associated memory system (Figure 10.12). This is essentially an entire computer system on a chip, with the exact specifications depending upon the model, and changing with time.

> 4) The number of hops is the number of devices a given data packet passes through.

![](img/bccda43674e4a93dee81c749eba8d2f7_269_0.png)

Figure 10.14 A schematic of an exascale computer in which, in addition to each chip having multiple cores, a graphical processing unit is attached to each chip (adapted from Dongarra (2011)).

and supercomputers at the exascale, in terms of both flops and memory, probably with millions of nodes.

Look again at the schematic in Figure 10.14. As in Blue Gene, there really are large numbers of chip boards and large numbers of cabinets. Here we show just one node and one cabinet and not the full number of cores. The dashed line in Figure 10.14 represents communications, and it is seen to permeate all components of the computer. Indeed, communications have become such an essential part of modern supercomputers, which may contain 100s of 1000s of CPUs, that the network interface “card” may be directly on the chip board. Because a computer of this sort contains shared memory at the node level and distributed memory at the cabinet or higher levels, programming for the requisite data transfer among the multiple elements is a fundamental challenge, with significant new investments likely to occur (Dongarra et al., 2014).

## 11

## Applied HPC: Optimization, Tuning, and GPU Programming

> More computing sins are committed in the name of efficiency (without necessarily achieving it) than for any other single reason – including blind stupidity.
> 
> *W.A. Wulf*

> We should forget about small efficiencies, say about 97% of the time: premature optimization is the root of all evil.
> 
> *Donald Knuth*

> The best is the enemy of the good.
> 
> *Voltaire*

This chapter continues the discussion of high-performance computing (HPC) began in the previous chapter. Here we lead the reader through exercises that demonstrates some techniques for writing programs that are optimized for HPC hardware, and how the effects of optimization may be different in different computer languages. We then move on to tips for programming on a multicore computer. We conclude with an example of programming in compute unified device architecture (CUDA) on a graphics processing card, a subject beyond the general scope of this text, but one of high current interest.

## 11.1

## General Program Optimization

- **Rule 1** Do not do it.
- **Rule 2** (for experts only): Do not do it yet.
- **Rule 3** Do not optimize as you go: Write your program without regard to possible optimizations, concentrating instead on making sure that the code is clean, correct, and understandable. If it is too big or too slow when you have finished, then you can consider optimizing it.
