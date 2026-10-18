```
ptimized Code
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
/*Reset excl_img_flags_threds() back again after each bucket is searched */
do i = atm_mask_idx + 1, atm_mask_idx + atm_maskdata(atm_i)%cnt
    excl_img_flags(offset_excl + atm_img_map(atm_mask(i))) = 0
end do
................
OpenMP loop ends
```

FIGURE 6.6, Cont'd.

# MODIFICATION OF LOAD BALANCE ALGORITHM

The work involved in calculating the forces on the atoms is distributed to the MPI tasks using the Amber load balancing scheme. The algorithm is modified so that the coprocessor gets an appropriate share of the load and runs concurrently with the processor, as shown below:

# PME DIRECT SPACE SUM AND NEIGHBOR LIST WORK

All MPI tasks are assigned with PME direct space sum and neighbor list work. The load-balancer monitors the performance of each MPI task in calculating the PME direct space sum over 50–100 time steps and dynamically adjusts the amount of PME direct space sum and neighbor list work assigned to each MPI task accordingly. The neighbor list performance for each MPI task is not monitored as it is directly proportional to the performance of the PME direct space sum and so is automatically adjusted based on the PME direct space sum performance. At the start of a simulation, offloading MPIs outperform