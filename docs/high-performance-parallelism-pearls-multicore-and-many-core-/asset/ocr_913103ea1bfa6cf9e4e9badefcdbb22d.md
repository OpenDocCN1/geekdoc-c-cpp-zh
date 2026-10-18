```
```fortran
subroutine satice1_s ()
    do j = jts,jte
    do k = kts,kte
    do i = its, ite
        !...
    end do
    do i = its, ite
        !...
    end do
    do i = its, ite
        !...
    end do
    do i = its, ite
        !...
    end do
    do i = its, ite
        !...
    end do
    do i = its, ite
        !...
    end do
    do i = its, ite
        !...
    end do
    do i = its, ite
        !...
    end do
    do l = lts, lte
        !...
    end do
    end do
    end do
end subroutine satice1_s
```
```

![](bbox=[0.133, 0.622, 0.888, 0.642])

Code listing—after loop-splitting, the code is vectorizable. This code is from file `module_mp_gsfccge.F`, which is located in the directory `WRFV3/phys` in the source code of WRF.

be utilized again later in the chapter discussion using data alignment directives. Since each thread will process only 16 data elements, better data locality is achieved as more of the data can be accessed from the cache memories. In Figure 3.11, Goddard multithreaded code for this technique is shown. The processing time was reduced from 144.3 to 52.3 ms on the Intel Xeon Phi coprocessor and from 299.9 to 138.3 ms on the Intel Xeon CPU.

# ADDITION OF VECTOR ALIGNMENT DIRECTIVES

Next, we added vector alignment directives before each i-loop so that the compiler can use a single aligned load instruction rather than the two-instruction unaligned load sequence. The data is known to be aligned in the memory because input data were copied to cells, which have a width of 16 data elements of 4 bytes each. Output data and local data use similar cells, which are also aligned. Therefore,