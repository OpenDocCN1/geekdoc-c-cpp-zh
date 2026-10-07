
# 458 PARALLEL COMPUTING IN C++ AND R

Hello ya'll from processor 6
Hello ya'll from processor 1
Hello ya'll from processor 2
Hello ya'll from processor 3
Hello ya'll from processor 5

As a somewhat more complicated application let us develop code for performing a balanced simple one of variance (AOV) in parallel. The premise is that (very large) samples have been taken from each nP populations and the necessary AOV statistics for each sample will be computed using separate processors. Listing 11.3 provides one possible implementation of this idea.

Listing 11.3 anovaMPI.cpp

```cpp
//anovaMPI.cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
#include "mpi.h"
#include "summary.h"

using std::cout; using std::endl;
using std::ifstream;

int main(int argc, char** argv) {
    double** pData;
    double* pData;

    MPI::Init(argc, argv);

    int myRank = MPI::COMM_WORLD.Get_rank();
    int nP = MPI::COMM_WORLD.Get_size();
    int n = atoi(argv[1]);

    if(myRank == 0) {
        pData = new double*[nP];

        ifstream fin;
        fin.open(argv[2]);
        for(int j = 0; j < nP; j++){
            pData[j] = new double[n];
            for(int i = 0; i < n; i++){
                fin >> pData[j][i];
            }
        }
        fin.close();
    }

    for (int i = 1; i < nP; i++) {
        MPI::COMM_WORLD.Send(pData[i], n, MPI::DOUBLE, i, 0);
    }
    Summary mySummary(n, pData[0]);
    double* stat = new double[2];
    mySummary.west(stat);
    cout << "For processor " << myRank << "\n" << " mean and variance are " << "\n" << stat[0] << " and " << stat[1] << endl;
```

# BASIC MPI COMMANDS FOR C++

```cpp
double num = 0;
double xBar = stat[0];
double den = ((double)n - 1)*stat[1];

for(int i = 1; i < n; i++){
    MPI::COMM_WORLD.Recv(stat, 2, MPI::DOUBLE, i, 1);
    num += ((double)i)/(double)(i + 1))*(stat[0] - xBar);
    xBar = ((double)i)/(double)(i + 1))*xBar +
    stat[0] += ((double)i)/(double)(i + 1));
    den += ((double)(n - 1);
}

num *= *(double)n/(double(nP-1));
den /= (double)nP/(nP - n);
cout << "The average is " << xBar << " = " << num << " on " << (n - nP) << " degrees-of-freedom" << endl;
cout << "The denominator square is " << den << " on " << (n*nP - nP) << " degrees-of-freedom" << endl;
if(den != 0)
    cout << "The F-ratio is " << (new[double]/den) << endl;
}

else{
    double* myData = new double[n];
    MPI::COMM_WORLD.Recv(myData, n, MPI::DOUBLE, 0, 0);
    mySummary(myData);
    double* stat = new double[2];
    mySummary.west(stat);
    cout << "For processor " << myRank << " mean and variance " << stat[0] << " and " << stat[1] << endl;
    MPI::COMM_WORLD.Send(stat, 2, MPI::DOUBLE, 0, 1);
}

MPI::Finalize();

return 0;
```

The new feature encountered in List 11.3 is the use of argc and argv in the Init function. This alternative form allows the command line input obtained to become available to all the processors managed by the COMM_WORLD communicator execution. This is used explicitly by here argv[1] to contain the size of the data sets that the processors will be given.

The input/of data becomes complicated when more than one processor is involved and the ability of different processors to establish connections is system-dependent. For this program we have made the minimal assumption that the master or rank 0 processor is capable of reading from a file. The first analysis is for the master processor to read the data from a file name which is contained in argv[2]. This data is stored in double-precision pointer-to-format with rows corresponding to populations/treatments and column indices representing the observation number. The result is an nP x n “array” pData. The storage layout for pData runs counter to the statistical format that has columns representing the treatments. This is necessary

# PARALLEL COMPUTING IN C++ AND R

(or least convenient) to the row-major order ordered by C/C++. As the goal is to ultimately sample the data from each pool to the different populations, the n elements of pdata need to the initial locations of the n storage blocks that are allocated for each of the n samples. Once the processor reads the data it uses for loop to pass out the samples by sending each processor element of pdata that is determined by the receiving rank. All the processors, including the master, then analyze their respective samples using an object with class Summary. This class is structured along the lines of Exercise 3.3. In particular, it contains an implementation (the method called worst) for computing a sample mean and variance. These two statistics are stored in locations accessed through pointers that are sent back to the master once each processor's work is completed. Finally, the master processor combines the results(also via Algorithm 2.3) from the other processors to obtain the F-statistic for testing the hypothesis that all populations have the same mean. To try out our parallel ANOVA code were generated in R

```r
> seed(123)
> A <- replicate(4, rnorm(100000))
> Apply(A, 2)
[1] -5.21437e-04 -1.5513e-03 1.54123e-06 1.775802e-04
> Apply(A, 2)
[1] 0.998541 0.999512 1.000192 1.001254
> write.table(t, file = "anova.txt", quote = FALSE, row.names = FALSE, col.names = FALSE)
```

Here we used the replicate function in a similar manner to Section 5.6 for the purpose of random number generation. 1,000,000 samples were produced from each of four "treatments". Some summary statistics were also generated that will provide a check for certain aspects of C++ results. The parallel ANOVA program was then compiled using the commands

```
$ mpc -c summary.cpp
$ mpc -c anova.cpp
$ mpc anova.summary -o anovaMPI
```

Upon execution the results

```
$ mpie -np 4 ANOVA mean and variance are -0.00155515 0.999512
For processor 2 the mean and variance are 1.54123e-06 1.00019
For processor 0 the mean and variance are -0.000521437 0.999854
For processor 3 the mean and variance are 0.00017758 1.00125
The grand average is -0.00047457
The numerator mean square is 0.607539 on 3 degrees-of-freedom
The denominator mean square is 1.00029 on 3.999996 degrees-of-freedom
The F-ratio is 0.607415
```

Comparison with the results from R suggests the output is correct. As expected, the F-statistic is not significant with a p-value of .6.

# 11.4 Parallel processing in R

It remains to consider how parallel processing can be carried out in R. There are several packages that enable R with threading capabilities. These include RParallel, snow and Rmpi. The CRAN website has a task view for high-performance computing that provides an indication of future developments and the current state of parallel computing using R.

# PARALLEL PROCESSING IN R

a thorough treatment of parallel processing in R covering sixteen different packages that can be used for parallelization. A companion article by Eust, et al. (2011) provides a tutorial on using four of these packages. Our focus in this section will be initially on the Rmpi package that provides an interface to MPI. This can be used to produce an interactive parallel processing environment via the "master/slave" command structure.

To begin Rmpi we load the Rmpi package using

```r
> library(Rmpi)
```

To create n slave processors the function mpi.spawn.Rslaves can be used with argument nslaves = n. For example, the code of n = 3 produces

```r
> library(Rmpi)
> mpi.spawn.Rslaves(nslaves = 3)
```

```
3 slaves are spawned successfully. 0 failed.
master (rank 0, comm 1) of size 4 is running on: eub-2
slave1 (rank 1, comm 1) of size 4 is running on: eub-2
slave2 (rank 2, comm 1) of size 4 is running on: eub-2
slave3 (rank 3, comm 1) of size 4 is running on: eub-2
```

All slaves are closed via the command mpi.close.Rslaves(). To quit R one should use use.quit() rather than quit() since the former command will make certain that mpi.finalize() is called.

As true for threads with OpenMP it is possible to have more slaves than the physical number of processors on a machine. This will not generally improve program performance in terms of running time. Thus to simplify treat each slave as corresponding to a different processor.

The Rmpi versions of the MPI functions Get.rank and Get.size are

```r
mpi.comm.rank()
```

and

```r
mpi.comm.size()
```

These functions return the rank of the calling slave processors and the total number of processors: i., the number of slaves to a master slave plus one for the master processor.

Objects are sent from the master to slave using an analog of the broadcast function Bcast discussed in Exercise 11.4. This function sends an R object to all the slaves. The syntax is

```r
mpi.bcast.Robj2slave(object)
```

with any type of R object including a function.

The slaves are instructed to run a specific set of R code, rCode, through the command

```r
mpi.remote.exec(rCode)
```

Upon executing this command on the master the slaves will carry out the tasks specified in rCode and return control to the master processor once they have completed their assignments.

Our first example of using Rmpi involves the obligatory greeting message with a minor twist. The R function hello is created first in the form
