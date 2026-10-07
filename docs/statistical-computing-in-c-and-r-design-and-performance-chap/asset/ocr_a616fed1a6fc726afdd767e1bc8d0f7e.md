# PARALLEL RANDOM NUMBER GENERATION

```
return 0;
}
```

The idea behind Listing 11.5 is straightforward. The master (or rank 0) processor uses our AdvanceSeed function along with an initial seed to determine seeds that will produce "inde-pent" random number streams for the other processors. These seeds are communicated to the processors using the Send and Recv functions. The processors then use these to initialize their individual RngStream objects. After finishing their tasks, the processors produce the uniform value they generated to the master process for output.

To check that our scheme for using RngStream objects produces the desired results both the seeds that are sent to each processor and the random numbers they generate are printed out by the master process. With four processors results

```
$ mpicxx -c RngStream.cpp
$ mpicxx -c ranMPI.cpp
$ mpicxx RngStream.o ranMPI.o -o ranMPI
$ mpiexec -np 4 ranMPI
```

+   1
2
3
4
5
6

For processor 1 the state is
3847595764
542750874
3358998068
4025640956
701604884
2546910389

For processor 2 the state is
3117713008
2901318700
433058656
3749492613
2059732357
994549473

For processor 3 the state is
3522649000
2524201075
3812486998
4095818817
2057726304
1219287084

The random number for processor 1 is 0.7017202
The random number for processor 2 is 0.476142
The random number for processor 3 is 0.0469012
The random number for process 0 is 0.00100995

This output agrees with our results from our OpenMP program as it should.
It remains to describe how "independent" random number streams can be obtained for