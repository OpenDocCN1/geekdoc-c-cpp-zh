
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

## FIGURE 5.12

Partitioning details for processing 501 benchmarking proteins using eFindSite simultaneously on the processor and coprocessor. The amount of computations is approximated by the product of the target protein length and the number of template structures.

![](img/16cb41208935c5f22dd1044f03f2e31b_119_0.png)

## FIGURE 5.13

Speedups of the parallel versions of eFindSite over the serial code. Computations are performed using three parallel versions: multiple processor threads (4 tasks, each running on 4 threads), multiple coprocessor threads (10 tasks, each running on 24 threads), and multiple processor and coprocessor threads running simultaneously.

We processed the entire dataset of 501 proteins using task-level parallelism and measured the time-to-completion, defined as the total time required for the prediction of ligand-binding sites. Figure 5.13 compares the results for the serial version and three parallel processing schemes. The speedup over the serial version is 11.8, 10.1, and 17.6 for the parallel processing using the processor, the coprocessor, and both resources, respectively. Therefore, using the coprocessor in addition to the processor accelerates the prediction of binding sites across large protein datasets. We also monitored the utilization of computing resources to demonstrate that all hardware threads are utilized. Figure 5.14 shows that the average usage of the processor and the coprocessor during production simulations is 99.9% and 82.2%, respectively. The coprocessor threads periodically become idle while waiting for the processor to start the pre-alignment (reading input files, performing sequence alignments) and finish the post-alignment (pocket clustering and ranking) tasks resulting a relatively lower utilization of the coprocessor. On the other hand, the processor remains fully utilized not only facilitating tasks offloaded to the coprocessor but also performing eFindSite calculations by itself. Finally, we checked for the numerical correctness of the results. Different versions of eFindSite produce identical results, thus the parallelization of eFindSite using OpenMP and offloading to the Intel Xeon Phi coprocessor fully maintains the functionality of the original code with a great benefit of much shorter simulation times.

![](img/16cb41208935c5f22dd1044f03f2e31b_120_0.png)

## FIGURE 5.14

Resource utilization during the execution of the heterogeneous parallel version of eFindSite. Time courses of the percentage of processor usage (black line) are compared to that of the coprocessor (gray line).

## CASE STUDY

Finally, we present a case study to illustrate binding pocket prediction using eFindSite. The target protein selected from the benchmarking dataset is human arginase I (PDB-ID: 3gn0, chain A), a binuclear manganese metalloenzyme hydrolyzing L-arginine. The abnormal activity of this protein is implicated in various disease states including erectile dysfunction, atherosclerosis, and cerebral malaria. eFindSite predicted a total of 10 pockets for this protein and assigned a confidence score of 91.9% to the top-ranked binding site. Figure 5.15 shows the crystal structure of this protein (transparent ribbons) with the top-ranked binding pocket predicted by eFindSite marked by a solid ball. The corresponding predicted binding residues are shown as a transparent gray surface. Two additional smaller balls mark the location of pockets at ranks 2 and 3. The prediction accuracy can be evaluated by revealing the location of a ligand α-difluoromethylornithine bound to the target protein in the experimental complex structure represented by solid sticks. We note that the ligand position was not part of the prediction procedure and it is used for validation purposes only. The distance between the predicted top-ranked binding site and the geometric center of the ligand is only 2.22 Å, demonstrating a high prediction accuracy of eFindSite. As a reliable tool for ligand-binding prediction, eFindSite is well suited for a broad range of applications ranging from protein function annotation to virtual screening and drug discovery.

## SUMMARY

eFindSite is a ligand-binding site prediction software used in drug discovery and design. To meet the challenges of proteome-scale applications, we implemented a parallel version of eFindSite for processing large datasets using HPC systems equipped with Intel Xeon Phi coprocessors. This parallel version of eFindSite achieves 17.6 speedup over the serial code using both processor and coprocessor

![](img/16cb41208935c5f22dd1044f03f2e31b_121_0.png)

**FIGURE 5.15**

Ligand-binding pocket prediction for human arginase I using *eFindSite*. The crystal structure of the target protein and the binding ligand is displayed as transparent gray ribbons and solid black sticks, respectively. The top-ranked predicted binding site is shown as a solid ball representing the pocket center and a transparent molecular surface around the binding residues. Two smaller balls represent the centers of binding pockets predicted at ranks 2 and 3.

resources, which is considered significant when normalized by the cost of the hardware. The x86 coprocessor architecture allows for open-standard and portable parallel programming on both traditional processors as well as coprocessors. In particular, using OpenMP makes it relatively easy to parallelize portions of the code. *eFindSite* represents a typical scientific software written mostly by domain scientists, who contributed different components to the code using different programming languages and styles. From our porting experience, even fairly complex codes, such as the hybrid C++/Fortran77 source code of *eFindSite*, can be successfully ported to utilize both Intel Xeon processors and Intel Xeon Phi coprocessors together yielding speedups at minimal coding efforts.

The development of the parallel version of *eFindSite* was fairly straightforward; however, we would like to discuss a couple of problems encountered throughout this process. First, due to the extensive use of thread-unsafe common blocks in the Fortran77 code, we initially attempted to rewrite those subroutines to pass parameters explicitly instead of accessing common blocks. However, these efforts took a very long time and considering the “spaghetti-like” nature of the code with multiple access points to common blocks, we could not reproduce the correct results in a timely fashion. For that reason, we decided to use OpenMP pragmas to mark the global variables as thread-private in the original code. This method turned out to be very practical and time efficient in the process of developing a thread-safe parallel implementation. Another issue we ran into was related to the stack size. We found that the default stack size on some HPC systems is smaller than that set for *eFindSite* using `OMP_STACKSIZE` causing segmentation fault errors. Consequently, in addition to OpenMP pragmas, modifying the default system stack size using `ulimit -s` may be required.
