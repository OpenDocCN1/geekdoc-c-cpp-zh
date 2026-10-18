use 24 threads per task on the coprocessor and 4 threads per task on the processor, we dispatch longer tasks to the coprocessor, whereas shorter jobs are executed on the processor. Running 4 parallel tasks on the processor and 10 parallel tasks on the coprocessor ensures that both resources are fully utilized. To avoid the oversubscription of coprocessor cores, the production code features an explicit mapping of parallel tasks to hardware threads at the compact thread affinity. Specifically, [export MIC_KMP_PLACE_THREADS=6c,4t,(i*6).'o'] defines the set of logical units assigned to each task, where 6c requests six cores, 4t starts four threads on each core, and (i*6).'o' is an offset of six cores between individual task. For example, when i=0, the first task runs on cores 0-5 with 4 threads per core totaling 24 threads, the next task sets i=1 to run on cores 6 through 11, and so forth. This way, the scheduler assigns different cores to different parallel tasks in order to conduct protein structure alignments at the maximum utilization of the accelerator hardware. Figure 5.12 lists partitioning details for the parallel execution for the benchmarking dataset using a computing node equipped with two 8-core Intel Xeon E5-2680 processors (8 threads, hyper-threading disabled) and one 61-core Intel Xeon Phi SE10P coprocessor (240 threads, compact thread affinity).

| Hardware | Core range | Number of threads | Percentage of computations |
|---|---|---|---|
| Processor | 1-4 | 4 | 12.2 |
|  | 5-6 | 4 | 12.5 |
|  | 7-11 | 4 | 12.7 |
|  | 12-16 | 4 | 11.8 |
| Coprocessor | 1-6 | 24 | 5.1 |
|  | 7-12 | 24 | 5.1 |
|  | 13-18 | 24 | 5.1 |
|  | 19-24 | 24 | 5.0 |
|  | 25-30 | 24 | 5.3 |
|  | 31-36 | 24 | 5.0 |
|  | 37-42 | 24 | 4.7 |
|  | 43-48 | 24 | 5.0 |
|  | 49-54 | 24 | 5.4 |
|  | 55-60 | 24 | 5.1 |
| Processor | 1-16 | 16 | 49.2 |
| Coprocessor | 1-60 | 240 | 50.8 |

# FIGURE 5.12

Partitioning details for processing 501 benchmarking proteins using eFindSite simultaneously on the processor and coprocessor. The amount of computations is approximated by the product of the target protein length and the number of template structures.