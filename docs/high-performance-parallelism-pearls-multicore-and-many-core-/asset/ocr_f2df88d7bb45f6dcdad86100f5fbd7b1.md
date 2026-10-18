```
!dir$ offload begin mandatory signal(sig1) target (mic:0) &
in(flat_cit(0:cit_tbl_x_dim*cit_tbl_y_dim*cit_tbl_z_dim-1) : alloc_if(.false.) free_if(.false.) into(flat_cit_dev(:)))&
in(fraction(:,1:atm_cnt) : alloc_if(.false.) free_if(.false.) into(fraction_dev(:, :)))&
in(x_bkts(0 : cit_tbl_x_dim_dev * 3 - 1) : alloc_if(.false.) free_if(.false.) into(x_bkts_dev(:)))&
in(x_trans(0 : cit_tbl_x_dim_dev * 3 - 1) : alloc_if(.false.) free_if(.false.) into(x_trans_dev(:)))&
in(y_trans(0 : cit_tbl_y_dim_dev * 3 - 1) : alloc_if(.false.) free_if(.false.) into(y_trans_dev(:)))&
in(y_bkts(0 : cit_tbl_y_dim_dev * 3 - 1) : alloc_if(.false.) free_if(.false.) into(y_bkts_dev(:)))&
in(z_bkts(0 : cit_tbl_z_dim_dev * 2 - 1) : alloc_if(.false.) free_if(.false.) into(z_bkts_dev(:)))&
in(z_trans(0 : cit_tbl_z_dim_dev * 2 - 1) : alloc_if(.false.) free_if(.false.) into(z_trans_dev(:)))&
out(used_img_lst_thread_dev(1:atm_local) : alloc_if(.false.) free_if(.false.))
................................
/*Offload code to build neighbor list for Xeon Phi*/
!dir$ end offload
................................
/*Host code to build neighbor list for host*/
/*Synchronize Host and Xeon Phi*/
!dir$ offload begin mandatory target(mic:0) wait(sig1)
!dir$ end offload
```

# FIGURE 6.4

Code snippet of the parallel neighbor list build on both host and coprocessor. The complete code can be found in get_nb_list_offload() routine in nb_pairlist.F90 file of the Amber source code.

+   (3) Variables that are required on every time step are asynchronously transferred to the coprocessor allowing simultaneous execution on the host and coprocessor.
+   (4) Indexing code allows for identifying neighbors in the statically allocated coprocessor neighbor list.
+   (5) The force calculations start on the coprocessor using OpenMP threads spawned from offloading MPI ranks.
+   (6) Control is immediately passed back to the host allowing asynchronous computation of the PME direct space sum on the host and coprocessor.
+   (7) Each OpenMP thread has an individual copy of the array used to store the forces, as otherwise race conditions would occur. The use of locks to save memory was investigated and the results showed that even with the costly initialization and reduction of the multiple copies of the force array when using the private array approach, private arrays performed roughly 10-15% faster than the alternative lock approach.