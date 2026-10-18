```
```fortran
subroutine allocate_state
    use module state_arrays
    use module array_sizes
    ! set number of vertical levels and number of chunks at
    ! run time
    nlevels = …
    numchunks = …
#ifndef _CHUNKSIZE_
    ! set chunksize at run time
    chunksize = …
#endif
    allocate(t(chunksize,nlevels,numchunks))
end subroutine allocate_state

subroutine wsm6(t,...)
    use module array_sizes
    real, intent(inout) :: t(chunk,nlevels,numchunks)
    integer :: i,j,k
    do j=1,numchunks
        do k=1,nlevels
            do i=1,numchunks
                t(i,k,j) = …
            enddo
        enddo
    enddo
end subroutine wsm6
```
```

# FIGURE 2.9

Optional compile-time constant loop and array bounds in subroutines. Since the compiler cannot see the original allocatable declaration of array “t,” it must use the dummy argument declaration. Thus, the compiler sees a compile-time constant for the size of the inner dimension of “t” and for the length of the “i” loop in the wsm6 subroutine. This code does not appear in the sample code because it uses a somewhat simpler and less flexible approach.

during each model time step, the wsm6 subroutine is called (not shown) and passed “t” as its first argument. All three array dimensions appear in the dummy argument declaration for “t.” Since the compiler cannot see the original declaration of actual argument “t” in module state_arrays, it cannot know that “t” was actually allocated. Therefore, it will see both the size of innermost dimension of “t” and the length of any “i” loops as being compile-time constants inside the wsm6 subroutine. This has significant performance benefit as described below.

The “chunksize” compile-time switch allows a great deal of performance tuning flexibility within a single-source code. For NVIDIA GPUs, setting “chunksize” to be a multiple of streaming multiprocessor size (32) yields the most efficient code. For processors and coprocessors with cores that support vector instructions, such as Intel® Advanced Vector Extensions, it is usually best to set chunksize equal to vector length, as will be seen below.

WSM6 also performs some expensive computations inside “single-column” loops that have “k” innermost. These loops consume about 20% of the execution time. Initially, we were concerned that