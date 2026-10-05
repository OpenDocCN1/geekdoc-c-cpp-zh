# 6.1. MPI Getting started

# 6.1.1 Initializing MPI

MPI is the most commonly used library for solving scientific problems on networked computers. MPI calls itself a fully featured library—with some justice. It has a lot of features. We will use only a thin sliver of MPI. Our goal is to write programs informed by the underlying network architecture, many of MPI's features are of little concern to us. The features we use are the ones that are best optimized by MPI implementations.

When an MPI run is set up, each node will have a process on it. For example, if the run is with 8 processes, each of the 8 nodes in figure 6.1 may have one process on it. The processes communicate by sending and receiving messages. We begin by looking at how the processes are set up and turn to message passing later.

Our first MPI program follows. This program assumes that the processor name is shorter than 199 characters.

```
#include <mpi.h>
int main(int argc, char **argv) {
    MPI_Init(NULL, NULL);
    int numprocs, rank;
    MPI_Comm_size(MPI_COMM_WORLD, &numprocs);
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);
    char procname[200];
    int procnamelen;
    MPI_Get_processor_name(procname, &procnamelen);
    cout<<"proc " <<procname<<" rank="<<rank<<endl;
    MPI_Finalize();
}
```

On line 10, each process prints the name of the compute node it is running on. Thus, the purpose of this program is to print the name of the nodes that the processes run on. If the program is started up with 10 processes, there will be 10 names printed.

> The MPI standard is posted at http://www.mpi-forum.org/docs/docs.html. Also see Snir et al. (1998) and Gropp et al. (1998).

> In general, it would be better to use MPI_MAX_PROCESSOR_NAME instead of guessing the maximum limit on the length of the processor's name. It is not employed here to prevent our first MPI program from getting too complicated.