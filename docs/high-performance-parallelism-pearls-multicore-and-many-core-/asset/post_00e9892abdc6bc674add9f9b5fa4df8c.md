
- (8) The PME direct space sum on the host uses a look-up table (LUT) to calculate the complementary error function, erfc. However, on the coprocessor the LUT created high memory access latency as a consequence of L2 cache misses. It causes poor performance when the coprocessor attempts to vectorize accesses. By calculating erfc on the fly, some of the latency is reduced (however, not all as some other arrays, i.e., the force and coordinate arrays, still have latency overheads due to irregular array accesses) which improves performance by a further 5%.

- (9) Reduce the force arrays into a single force array once all OpenMP threads have finished.

- (10) Host execution waits for the return signal from the coprocessor before continuing.

- (11) The coprocessor force array is asynchronously copied back to the host and combined with the host force array.

## ADDITIONAL OPTIMIZATIONS IN COPROCESSOR CODE

This section describes three key optimization techniques that have been applied to accelerate the coprocessor offload implementation in Amber 14.

### REMOVING LOCKS WHENEVER POSSIBLE

In the original code snippet in Figure 6.5, the array index img_j defines a neighboring atom to the current atom being calculated. The updates to arrays indexed using img_j occur simultaneously as the loop is distributed across cores using an OpenMP loop. It is possible that multiple atoms have the same neighboring atom(s); therefore, img_j can be the same for multiple OpenMP threads resulting in a race condition.

To prevent this race condition, an OpenMP critical section was used in the original code. Since OpenMP critical sections of code are detrimental to performance, a work-around was found to avoid the critical section entirely, as shown in the optimized code. The used_img_map() array, and used_img_cnt variable are used to store values sequentially in the used_img_lst() array. Since two separate neighbor lists are built for Host and Phi, two versions of used_img_lst() and used_img_map() have been built; then, these two versions are combined to produce combined version of the two arrays. Later, both of these arrays are used in other routines. All of the functionality can be achieved by the simpler and lockless code as shown in the optimized code column. All OpenMP threads update this shared array, and the same positions can be updated (placing 1) by multiple threads. The used_img_map() now contains “1”s in the position of img_j, which is an atom index. After used_img_map() array is built on the coprocessor, it is used with the host version of used_img_lst() and used_img_map() to build the combined version of used_img_lst() and used_img_map(). The optimization is possible because used_img_map() is single byte type and 1’s are stored on specific array positions. The optimized code can be found in get_nb_list_offload() routine inside the nb_pairlist.F90 file of the Amber source code.

| Original Code | Optimized Code |
|---|---|
| <pre>/*Xeon Phi offload code*/<br>OpenMP Do loop starts<br><br>................<br><br>!$omp critical<br>&nbsp;&nbsp;if (used_img_map(img_j) .eq. 0) then<br>&nbsp;&nbsp;&nbsp;&nbsp;used_img_map(img_j) = 1<br>&nbsp;&nbsp;&nbsp;&nbsp;used_img_cnt = used_img_cnt + 1<br>&nbsp;&nbsp;&nbsp;&nbsp;used_img_lst(used_img_cnt) = img_j<br>&nbsp;&nbsp;end if<br>!$omp end critical<br><br>................<br>OpenMP loop ends<br>................<br>/*Xeon Phi and Host version of used_img_map() are combined. Similarly two versions of used_img_lst() are combined for later use*/</pre> | <pre>/*Xeon Phi offload code*/<br>OpenMP Do loop starts<br><br>................<br><br>used_img_map(img_j) = 1<br><br>................<br>OpenMP loop ends<br>................<br>/*Xeon Phi version of used_img_map() is used with existing img_map() and used_img_lst() to get combined version of used_img_lst() and used_img_map() for later use*/</pre> |

FIGURE 6.5

Code snippets to show the optimization of the assignment of neighboring atoms by removal of an omp critical section.

### EXCLUSION LIST OPTIMIZATION

In the original code as shown in Figure 6.6, on every time step the excl_img_flags() array (an array used in the neighbor list calculation) is initialized, allocated for each OpenMP thread and then reset back again after each bucket is searched.

All of the tasks in the original code can be optimized by:

- 1. allocating a larger array of size *atm_cnt* × *number of threads*, allowing one allocation of the array during system setup, removing the need to reallocate on each loop iteration
- 2. One time initialization of the array in system setup
- 3. using this larger array with proper indexing in the neighbor list code
- 4. resetting only the positions of the larger array which have already been used. Thus, the array can be used again in the next time step.

With this optimization, we can save the time of resetting and allocating the array inside the OpenMP runtime in every time step; both of which are expensive. The optimized code can be found in get_nb_list_offload() routine inside nb_pairlist.F90 file.

### REDUCE DATA TRANSFER AND COMPUTATION IN OFFLOAD CODE

In the original Amber MD code, as shown in Figure 6.7, each MPI rank allocates and uses the global atom list and force arrays. Thus, in the offload implementation, the global atom list and force arrays have to be transferred back and forth between the host and the coprocessor. However, since each MPI rank does not use the full list of atoms, an optimization is used to reduce data transfers and computation in the offloaded code. The ranges of atom indices are determined by finding the maximum and minimum indices of the used atoms before the direct space sum calculation.

This optimization is extended to other arrays where the full range of atoms (1 to atm_cnt) is not required. The optimized code can be found in get_nb_energy_offload() routine inside get_nb_energy_offload.i file.

The loop has been further optimized as shown in Figure 6.6. Fortran allows loop accesses to be indexed so that all the positions of the array are contiguous in memory to the compiler, which allows for memset to be issued in fewer clock cycles.

```text
Original Code
/*inside neighbor list routine*/
/*Reset the array in each step*/
do i = 1, atm_cnt
  excl_img_flags(i) = 0
end do
OpenMP loop starts
............
/*allocate arrays for each OpenMP threads*/
!$omp firstprivate(excl_img_flags_dev)
..........
/*Reset excl_img_flags() back again after each bucket of atoms are searched for neighbors*/
  do i = atm_mask_idx + 1, atm_mask_idx + atm_maskdata(atm_i)%cnt
    excl_img_flags(offset_excl + atm_img_map(atm_mask(i))) = 0
  end do
............
OpenMP loop ends
```

```text
Optimized Code
/*inside an initial setup routine*/
do i = 1, atm_cnt*num_threads
    excl_img_flags_threaded(i) = 0
end do
/*inside neighbor list routine*/
OpenMP loop starts
............
do i = atm_mask_idx + 1, atm_mask_idx + atm_maskdata(atm_i)%cnt
    excl_img_flags_threaded(offset_excl + atm_img_map(atm_mask(i))) = 0
end do
..........
/*Reset excl_img_flags_threaded() back again after each bucket is searched */
do i = atm_mask_idx + 1, atm_mask_idx + atm_maskdata(atm_i)%cnt
    excl_img_flags(offset_excl + atm_img_map(atm_mask(i))) = 0
end do
................
OpenMP loop ends
```

FIGURE 6.6
Code snippets to show the optimization of the exclusion list calculation.
FIGURE 6.6, Cont'd.

### MODIFICATION OF LOAD BALANCE ALGORITHM

The work involved in calculating the forces on the atoms is distributed to the MPI tasks using the Amber load balancing scheme. The algorithm is modified so that the coprocessor gets an appropriate share of the load and runs concurrently with the processor, as shown below:

### PME DIRECT SPACE SUM AND NEIGHBOR LIST WORK

All MPI tasks are assigned with PME direct space sum and neighbor list work. The load-balancer monitors the performance of each MPI task in calculating the PME direct space sum over 50–100 time steps and dynamically adjusts the amount of PME direct space sum and neighbor list work assigned to each MPI task accordingly. The neighbor list performance for each MPI task is not monitored as it is directly proportional to the performance of the PME direct space sum and so is automatically adjusted based on the PME direct space sum performance. At the start of a simulation, offloading MPIs outperform
