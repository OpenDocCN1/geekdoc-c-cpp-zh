# Listing 10.3 laplace.c Serial solution of Laplace's equation using a finite difference technique.

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

# 10.14.1

# Domain Decomposition Exercises

+   1. Get the serial version of either laplace.c or laplace.f running.
+   2. Increase the lattice size to 1000 and determine the CPU time required for convergence to six places. Make sure that this is the actual run time and does not include any system time. (You can get this type of information, depending upon the operating system, by inserting timer calls in your program.)
+   3. Decompose the domain into four subdomains and get an MPI version of the code running on four compute nodes. [Recall, we give an example of how to do this in the Codes directory with the serial code poisson_1d.c and its MPI implementation, poisson_parallel_1d.c (courtesy of Michel Vallieres).]
+   4. Convert the serial code to three dimensions. This makes the application more realistic, but also more complicated. Describe the changes you have had to make.
+   5. Decompose the 3D domain into four subdomains and get an MPI version of the code running on four compute nodes. This can be quite a bit more complicated than the 2D problem.
+   6. Conduct a weak scaling test for the 2D or 3D code.
+   7. Conduct a strong scaling test for the 2D or 3D code.