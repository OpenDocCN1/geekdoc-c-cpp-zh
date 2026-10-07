# OPENMP

# 451

* firstprivate which has a similar function to private except that the objects/variables are initialized in the parallel section using initial values from a serial code segment.

The code list below provides an example of using a pragma to parallelize a block of code.

# Listing 11.1 ompEx.cpp

```
//ompEx.cpp
#include <omp.h>
#include <iostream>

int main () {
    int nP = omp_get_num_procs();
    omp_set_num_threads(nP);
    int myNumber;
    #pragma omp parallel private(myNumber)
    {
        myNumber = omp_get_thread_num();
        std::cout << "Hi ya'll from thread " <<
        myNumber << "!" << std::endl;
    }
    return 0;
}
```

The first thing to observe in Listing 11.1 is the inclusion of the OpenMP header file omp.h. Then, two OpenMP functions

omp_get_num_procs and omp_set_num_threads

are used to return the number of processors and set the number of threads, respectively. In this case the number of threads to be used in each parallel section has been specified as being the same as the number of processors.

The block of code in Listing 11.1 is created using a parallel directive with the variable myNumber being given a memory location for each of the n threads through use of a private clause. When the master thread forks at the beginning of a pragma every thread gets a unique ID starting with 0. The value of a particular thread is identified using omp_get_thread_num which is written into the variable myNumber in the program. Since myNumber not been designated as private as its value would have been stored in a single memory location that was accessible by all threads shared and The resulting behavior of the program would be unpredictable with one thread able to write its value for myNumber into the space of time prior to accessing the value and using omp to write its message to standard output.

Compilation of OpenMP programs follows the fopenmp compiler option. The command line for a program programName.cpp would look like

```
g++ -fopenmp programName.cpp -o executableName
```

This has the effect of creating executableName as the executable version of the program. For example, Listing 11.1 was compiled and executed with

```
$ -fopenmp ompEx.cpp -o ompEx
./ompEx
```

Hi ya'll from thread Hi ya'll from thread Hi ya'll from thread
Hi ya'll from thread 1!!302!!