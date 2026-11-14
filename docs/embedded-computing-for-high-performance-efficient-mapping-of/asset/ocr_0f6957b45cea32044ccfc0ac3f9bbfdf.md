compute bound—say running 80% or more of the CPU share, or memory/IO bound in this case running 20% or less. Intuitively, if the computation is compute bound, we want to match the number of threads to the number of available cores. If it is memory or IO bound, we use more threads to reduce the number of idle cores. The heuristics used to determine the number of threads can be easily changed or adapted in this aspect to capture more complex conditions and metrics. Finally, we instrument selected loops (line 19) with the OpenMP directive #pragma omp for with the identified number of threads.

# 6.8.3 MONITORING AN MPI APPLICATION

MPI applications can be difficult to monitor and debug since they consist of multiple communicating parallel processes, each of them running in their own memory space. A simple strategy for monitoring and tracing execution, as mentioned in Chapter 4, is to wrap library functions with augmented functionality, which in this case would monitor the behavior of each MPI process.

In our strategy, we develop a new monitoring library, e.g., TrackMPI, for tracking the behavior of each MPI routine used in the program. To ease the integration of TrackMPI on existing MPI programs, we name each monitoring routine after the corresponding MPI routine, prefixing it with “Track”. Hence, TrackMPI_Recv tracks calls to MPI_Recv. All that remains is to replace the original MPI calls with the corresponding monitoring calls, which is performed by the following aspect:

```
1. aspectdef TrackMPI
2.
3. select file end
4. apply
5. ${file.exec addInclude("mpi_track.h", true);}
6. end
7.
8. var mpiFn = [ "MPI_Init",
9. "MPI_Comm_size",
10. "MPI_Comm_rank",
11. "MPI_Finalize",
12. "MPI_Send",
13. "MPI_Recv",
14. "MPI_Recv",
15. "MPI_Recv",
16. "MPI_Gather",
17. "MPI_Scatter",
18. "MPI_Gatherv" ];
19.
20. select function call: end
21. apply
22. var name = $call.name;
23.
24. if (mpiFn.indexOf(name) > -1) {
25. $call.exec setName("Track" + name);
26. }
27. end
28. end
```