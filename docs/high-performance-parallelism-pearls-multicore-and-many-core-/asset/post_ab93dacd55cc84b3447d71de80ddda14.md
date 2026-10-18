
c  Fr-TM-align converted into a subroutine

!dir$ attributes offload:mic::frtmalighn
!dir$ attributes offload:mic::d8
!dir$ attributes offload:mic::xa
!dir$ attributes offload:mic::nseq1
!dir$ attributes offload:mic::nseq2
!dir$ attributes offload:mic::ires1
!dir$ attributes offload:mic::resa
!dir$ attributes offload:mic::seq_a
!dir$ attributes offload:mic::isec
!dir$ attributes offload:mic::jsec
!dir$ attributes offload:mic::n1
!dir$ attributes offload:mic::n2
!dir$ attributes offload:mic::xt
!dir$ attributes offload:mic::yt
!dir$ attributes offload:mic::zt
!dir$ attributes offload:mic::xb
!dir$ attributes offload:mic::yb
!dir$ attributes offload:mic::zb

subroutine frtmalighn(tm_score1,tm_score2,tm_score3,tm_score4,target_len,
     &     template_len,target_seq,template_seq,tm_align,target_res,
     &     template_res,target_xyz,template_xyz,tm_tt1,tm_uu1,align_length)
     .
end

## FIGURE 5.8

Fortran77 subroutine frtmalighn offloaded to the coprocessor.

which are typically set to either compact, balanced, or scatter modes. Since the affinity mode may have an impact on the parallel performance, we first benchmarked eFindSite using different Intel KMP affinity settings, [export MIC_KMP_AFFINITY=compact/scatter/balanced].

In order to analyze the performance of eFindSite, we first developed a reliable measure to quantify its computing speed. As shown in Figure 5.3, the subroutine u3b is a frequently called low-level function that calculates a root-mean-square deviation (RMSD) between two sets of atomic coordinates. We found that the total number of RMSD calculations correlates well with the total wall time and the structure alignment time; the corresponding Pearson correlation coefficients are as high as 0.963 and 0.960, respectively. Thus, we use the number of RMSD calculations per second to measure the eFindSite performance.

In Figure 5.9, we plot the performance of eFindSite with the structure alignment portion of the code offloaded to the coprocessor. Note that the pre- and post-alignment steps are sequentially executed on the processor. Because some proteins in the benchmark dataset have less than 50 templates, we only consider parallel execution using up to 24 threads per task in order to avoid idle threads. Encouragingly, increasing the number of threads on the coprocessor clearly improves the performance of eFindSite. The average performance is 4.27 × 10⁴ and 2.30 × 10⁵ RMSD calculations per second as the number of threads increases from 4 to 24. Considering structure alignment calculations alone, almost a perfect linear scaling is achieved (open circles in Figure 5.9). In contrast, the performance of eFindSite reaches a plateau when the total wall time is plotted (black circles in Figure 5.9). Here, the number of RMSD calculations per second improves from 3.98 × 10⁴ for 4 threads to 1.76 × 10⁵ for 24 threads, which can be explained by Amdahl’s Law describing the relationship between the expected speedup of a parallel implementation relative to the serial algorithm. These performance measurements are carried out for the balanced and scatter thread affinity modes that maximize hardware utilization by evenly spreading

![](img/16cb41208935c5f22dd1044f03f2e31b_115_0.png)

## FIGURE 5.9

Performance of eFindSite using parallel coprocessor threads. The speed is measured by the number of RMSD calculations per second (mean ± standard deviation) for 4, 8, 16, and 24 threads across the benchmarking dataset of 501 proteins. Solid and open symbols correspond to the total time and the time spent calculating structure alignments, respectively. Circles and squares show the performance using balanced/scatter and compact thread affinity, respectively.

threads across coprocessor cores. For the compact affinity setting placing four threads on a single core before moving to the next one, the rate of RMSD calculations increases from 2.27 × 10⁴ to 1.25 × 10⁵ for the alignment time (open squares in Figure 5.9), and from 2.19 × 10⁴ to 1.06 × 10⁵ for the total time (black squares in Figure 5.9). Although the balanced/scatter thread affinity yields an approximately 1.8 times higher performance per thread compared to the compact affinity mode, its advantage starts diminishing when the total number of threads on the coprocessor exceeds 120, and all affinity modes become essentially the same when the thread count reaches 240. In fact, a core-to-core performance comparison shows a slightly higher performance of the compact mode at 2.44 × 10⁴ RMSD calculations per second compared to 2.38 × 10⁴ for the balanced and scatter modes.

## PARALLEL VERSION FOR A MULTICORE PROCESSOR

In addition to the Intel Xeon Phi coprocessor version of eFindSite, we also implemented a parallel code that can be executed on multicore processors. Similarly, we employed pragma-based OpenMP to parallelize structure alignment calculations with both pre- and post-alignment steps executed sequentially. We also increased the memory available to each thread to 64M using [export

![](img/16cb41208935c5f22dd1044f03f2e31b_116_0.png)

**FIGURE 5.10**
Performance of *eFindSite* using parallel processor threads. The speed is measured by the number of RMSD calculations per second (mean ± standard deviation) for 2, 4, 8, and 16 threads across the benchmarking dataset of 501 proteins. Solid triangles and open squares correspond to the total time and the time spent calculating structure alignments, respectively.

`OMP_STACKSIZE=64M`. In Figure 5.10, we plot the performance of the multi-threaded version of *eFindSite* on the Intel® Xeon® E5-2680 processor. Using the total simulation time, the serial (1 thread) and parallel (16 threads) versions have an average performance across the benchmarking dataset of 1.06 × 10⁵ and 6.16 × 10⁵ RMSD calculations per second, respectively. When considering the time spent calculating structure alignments, the average performance increases to 1.24 × 10⁵ and 1.85 × 10⁶ RMSD calculations per second. A good linear scaling is achieved with a speedup over the serial execution of 15 when 16 processor threads are utilized. The performance reaches a plateau at a speedup of 5.8 for the total wall time; we note that according to Amdahl’s law, the maximum theoretical speedup of a code that is 90% parallelized using 16 threads is 6.4.

## TASK-LEVEL SCHEDULING FOR PROCESSOR AND COPROCESSOR

Computing nodes equipped with Intel Xeon Phi coprocessor cards provide massively parallel capabilities through multicore processors and many-core coprocessors. Therefore, our ultimate goal was to develop a production code of *eFindSite* that takes full advantage of both resources. The production scheme

for predicting ligand-binding sites across large datasets of proteins using eFindSite involves using both the processor and the coprocessor simultaneously. The processor executes the serial portion of the code, while structure alignments are offloaded to the coprocessor with the compact affinity mode to maximize the performance of eFindSite. At the same time, the processor also runs a parallel version of eFindSite as well, using relatively few threads. This way, we process multiple proteins concurrently by multiple parallel tasks executed simultaneously on both computing units.

We developed a job scheduler in Perl to launch up to 4 parallel tasks on the processor with 4 threads per task, and up to 10 parallel tasks on the coprocessor, each using 24 threads in the compact affinity mode. As shown in Figure 5.11, we first sort target proteins by a product of the residue count and the number of templates, which estimates the wall time required to complete the calculations. Because we

```
use Proc::Background;
my $n_mic = 10;    // 10 parallel jobs on a coprocessor
my $n_cpu = 4;     // four parallel jobs on a processor
my @lst3 = ();     // template protein list
foreach my $wlst2 ( sort { $lst2{$a} <=> $lst2{$b} } keys %lst2 ){
    push(@lst3, $wlst2);
}
while ( @lst3 ){
    # dispatching jobs to Xeon processor
    for ( my $xa = 0; $xa < $n_cpu; $xa++ ){
        # start a new process if the current is finished
        if ( @lst3 and !$j_cpu[$xa]->alive() ){
            #get an item from the top of the list (smaller template)
            my $job = shift(@lst3);
            printf("CPU%d <- %s ... %.1f%%\n", $xa, $job, \
                (++$prgl/$n1st3)*100.0, '%');
            $j_cpu[$xa]=Proc::Background->new("$ef_omp -s $job.pdb \
                -t $job.ethread-fun -i $job.ss -e $job.prf -o $job- \
                efindsite -b $foptb -x $foptx > $job.log 2>&1");
            $c_cpu[$xa]++;
            $l_cpu[$xa] += $lst2{$job};
        }
    }
    # offloading jobs to Xeon MIC jobs
    for ( my $xa = 0; $xa < $n_mic; $xa++ ){
        if ( @lst3 and !$j_mic[$xa]->alive() ){
            #get an item from the bottom of the list (larger template)
            my $job = pop(@lst3);
            my $kpt='export \
                MIC_KMP_PLACE_THREADS=6c,4t,'.int($xa*6).'O';
            printf("MIC%d <- %s ... %.1f%%\n", $xa, $job, \
                (++$prgl/$n1st3)*100.0, '%');
            $j_mic[$xa] = Proc::Background->new('$kpt ; $ef_mic -s \
                $job.pdb -t $job.ethread-fun -i $job.ss -e $job.prf -o \
                $job-efindsite -b $foptb -x $foptx > $job.log 2>&1");
            $c_mic[$xa]++;
            $l_mic[$xa] += $lst2{$job};
        }
    }
    sleep(2) if ( @lst3 );
}
```

## FIGURE 5.11

Part of the task scheduler implemented in Perl dispatching four parallel tasks (4 threads per task) on the processor and 10 parallel tasks (10 threads per task) on the coprocessor.
