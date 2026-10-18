```
```fortran
! This section is as close as possible to top of program.
! May need a long list of “private” variables here:
!$OMP PARALLEL PRIVATE(i,j,k,n_loc,j_loc,k_loc, &
!$OMP& icount,xdist,ydist,zdist,...)
...
!$OMP SINGLE
            ! Only 1 thread does any I/O needed...
            ...
!$OMP END SINGLE
...
! Main loop over smoothing iterations:
        do icount=1,ncount
            call halo_exchange(ext_in,myrank,nx_loc,...)
            ...
!$OMP DO
!   Central smoothing nested loops as in Figure 1.1:
            do k=2,nz_loc+1
                ...
            end do
!$OMP END DO

            call halo_exchange(ext_out,myrank,nx_loc,...)

!$OMP DO
!   2nd smoothing pass, but from ext_out to ext_in:
            do k=2,nz_loc+1
                ...
            end do
!$OMP END DO
        end do    ! End of main outer loop over icount
!$OMP END PARALLEL
```
```

# FIGURE 17.2

Partial coarse-grained: schematic code for coarse-grained OpenMP implementation of the stencil application. Note that the parallel section now encloses the main outer loop, I/O, and message-passing in the halo_exchanges.

argument list of halo_exchange in Figure 17.2. (Similar variables ny_loc and nz_loc are not shown for brevity, but the points made here about nx_loc apply equally well to them too).

If NX is the number of (x-dimension) points in the “global” domain, nx_loc is the number of such points in each MPI subdomain. Any arrays of size nx_loc then span the entire subdomain. If any such arrays are declared inside an OpenMP parallel region (e.g., in the “halo_exchange” subroutine of the coarse-grained code in Figure 17.2), then a separate copy of those arrays will be created for each thread. This may not be a problem if OMP_NUM_THREADS is set to just 2 or 4 (e.g., to soak up hyper-threads on a Intel Xeon processor host node), but can be a major problem on a Intel Xeon Phi coprocessor, where OMP_NUM_THREADS could plausibly have a value as large as 244, but where memory is typically only a fraction of that available on the host node. If each OpenMP thread