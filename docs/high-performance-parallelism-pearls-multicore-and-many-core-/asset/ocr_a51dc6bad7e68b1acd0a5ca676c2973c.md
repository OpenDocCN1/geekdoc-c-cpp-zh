(8) The PME direct space sum on the host uses a look-up table (LUT) to calculate the complementary error function, erfc. However, on the coprocessor the LUT created high memory access latency as a consequence of L2 cache misses. It causes poor performance when the coprocessor attempts to vectorize accesses. By calculating erfc on the fly, some of the latency is reduced (however, not all as some other arrays, i.e., the force and coordinate arrays, still have latency overheads due to irregular array accesses) which improves performance by a further 5%.

(9) Reduce the force arrays into a single force array once all OpenMP threads have finished.

(10) Host execution waits for the return signal from the coprocessor before continuing.

(11) The coprocessor force array is asynchronously copied back to the host and combined with the host force array.

# ADDITIONAL OPTIMIZATIONS IN COPROCESSOR CODE

This section describes three key optimization techniques that have been applied to accelerate the coprocessor offload implementation in Amber 14.

# REMOVING LOCKS WHENEVER POSSIBLE

In the original code snippet in Figure 6.5, the array index img_j defines a neighboring atom to the current atom being calculated. The updates to arrays indexed using img_j occur simultaneously as the loop is distributed across cores using an OpenMP loop. It is possible that multiple atoms have the same neighboring atom(s); therefore, img_j can be the same for multiple OpenMP threads resulting in a race condition.

To prevent this race condition, an OpenMP critical section was used in the original code. Since OpenMP critical sections of code are detrimental to performance, a work-around was found to avoid the critical section entirely, as shown in the optimized code. The used_img_map() array, and used_img_cnt variable are used to store values sequentially in the used_img_lst() array. Since two separate neighbor list is built for Host and Phi, two version of use_img_lst() and used_img_map() have been built; then, these two versions are combined to produce combined version of the two arrays. Later, both of these arrays are used in other routines. All of the functionality can be achieved by the simpler and lockless code as shown in the optimized code column. All OpenMP threads update this shared array, and same positions can be updated (placing 1) by multiple threads. The used_img_map() now contains “1”s in the position of img_j, which is an atom index. After used_img_map() array is built on the coprocessor, it is used with the host version of used_img_lst() and used_img_map() to build the combined version of used_img_lst() and used_img_map(). The optimization is possible because used_img_map() is single byte type and 1’s are stored on specific array positions. The optimized code can be found in get_nb_list_offload() routine inside the nb_pairlist.F90 file of the Amber source code.

# EXCLUSION LIST OPTIMIZATION

In the original code as shown in Figure 6.6, on every time step the excl_img_flags() array (an array used in the neighbor list calculation) is initialized, allocated for each OpenMP thread and then reset back again after each bucket is searched.