```
!$OMP PARALLEL DO PRIVATE ( ij,i,k,j,ipn ) &
!$OMP SCHEDULE(runtime)
    do j = jts,jte
        ij = (j-1)*CHUNK
        ! transpose from dynamics to physics
        do i = its,ite
            ipn = min(ij+i+ips-1,ipe)
            do k = kts,kte
                u_phy(i,k,j) = u_dyn(k,ipn)
                ! transpose other arrays...
            end do  ! k loop
        end do  ! i loop
        ! physics computations on chunk "j", including WSM6
        call nim_mpas_physics_driver(...)
        ! transpose from physics to dynamics
        do i = its,ite
            ipn = ij+i+ips-1
            if ((ips<=ipn).and.(ipn<=ipe)) then
                do k = kts,kte
                    su_dyn(k,ipn) = tend_u_phy(i,k,j)*r_dyn(k,ipn)
                    ! transpose other arrays...
                enddo  ! k loop
            endif
        enddo  ! i loop
    enddo  ! j loop
```

# FIGURE 2.4

Code to transpose between dynamics and physics data structures. Code additions needed to handle replication of the last dynamics column are highlighted. This code does not appear in the sample code because NIM dynamics is not included.

# ARRAY ALIGNMENT

Alignment of arrays in memory is key to good vector performance on the first generation of Intel Xeon Phi coprocessors. Unaligned arrays can generate inefficient scalar instructions to handle array elements at the beginning and end of each array. The Intel compiler option "-align array64byte" can be used to ensure that every array begins on a vector boundary. In a perfect world, this would be sufficient to ensure that all arrays are really aligned. However, the Intel compiler requires additional assistance in some cases to recognize that some arrays are really aligned. Use of the Intel compiler options "-qopt-report-phase=loop,vec -qopt-report=4" will cause the compiler to complain whenever it is not convinced that an array is really aligned. We use this information to identify opportunities to insert Intel-specific compiler directives "ASSUME_ALIGNED" and "VECTOR ALIGNED" as shown in Figure 2.5. Here the "ASSUME_ALIGNED" directive is used to tell the Intel compiler that the arrays listed are aligned on 64-byte boundaries (e.g., "worka:64"). The "VECTOR_ALIGNED" directive tells the compiler that all the arrays in the immediately following loop are aligned. Note that this optimization is best combined with optional compile-time constants for memory and loop bounds as described below. Telling the compiler that arrays are aligned when they are not will lead to incorrect results or