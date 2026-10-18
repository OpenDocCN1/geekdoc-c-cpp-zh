
```fortran
#ifdef ALIGN_OK
!DIR$ ASSUME_ALIGNED den:64,denqrs:64,qrs:64
#endif
    do k = kte, kts, -1
#ifdef ALIGN_OK
!DIR$ VECTOR_ALIGNED
#endif
    do i = its, ite
        denqrs(i,k,1) = den(i,k)*qrs(i,k,1)
        denqrs(i,k,2) = den(i,k)*qrs(i,k,2)
        denqrs(i,k,3) = den(i,k)*qrs(i,k,3)
    enddo
enddo
```

**FIGURE 2.5**

Code with Intel-specific alignment directives added. Note use of cpp token “ALIGN_OK” to disable directives for build configurations where arrays are not really aligned. This loop can be found in the sample code at line 470.

segfaults. To avoid incorrect alignment, we introduce cpp token “ALIGN_OK” which is only defined when compile-time constants are used (see below).

## LOOP RESTRUCTURING

Data locality is a key to good performance on all modern CPU and fine-grained architectures. In many cases, loop fusion can be used to demote temporary arrays to arrays of lower rank (or even to scalars). In other cases, loop fusion can improve cache reuse by allowing multiple computations that use the same array values to iterate through those values only once.

However, WSM6 contained a few large extremely complex loops that inhibited vectorization. These loops contain very intricately interwoven conditional blocks with multiple layers of data-dependent “if-else” constructs. Despite their good locality, these loops were simply too complicated for the vectorizer to understand and manual loop splitting was required. We were guided by compiler optimization reports when making these changes. See Figure 2.6 for a simplified example of one of these loops. This code computes changes in mass of cloud water, cloud ice, rain, snow, and graupel due to melting and freezing and adjusts temperatures in response to these changes. For brevity, complex inline computations are abbreviated as function calls (e.g., “rain_freeze()”). This snippet would normally be good for data locality since scalars “del2” and “del3” are reused for many different computations. Since the compiler could not vectorize this loop, even with directives added, we manually split the loop. This required promotion of scalars “del2” and “del3” to arrays as shown in Figure 2.7.

```fortran
REAL :: rain(its:ite,kts:kte)
REAL :: snow(its:ite,kts:kte)
! similar for water, ice, graupel, etc.
REAL :: del2,del3
do k = kts, kte
!DIR$ VECTOR ALIGNED
  do i = its, ite
    del2=0.; del3=0.
    if(rain(i,k).lt.qmin.and.snow(i,k).lt.qmin) del2=1.
    if(rain(i,k).lt.qmin) del3=1.
    ! if temperature is below freezing
    if(t(i,k).le.t0C) then
      rain(i,k) = rain_freeze(rain,snow,...,del2,del3)
      snow(i,k) = snow_freeze(rain,snow,...,del2,del3)
      ! similar for water, ice, graupel, etc.
    else
      rain(i,k) = rain_liq(rain,snow,...,del2,del3)
      snow(i,k) = snow_liq(rain,snow,...,del2,del3)
      ! similar for water, ice, graupel, etc.
    endif
  enddo
enddo
```

**FIGURE 2.6**

The ifort compiler could not vectorize this loop due to complexity. Normally, the use of scalars del2 and del3 would be ideal since they are reused by many following computations. This original loop does not appear in the sample code.

```fortran
! same array declarations for rain, snow, etc.
! del2, del3 promoted from scalars to arrays
REAL :: del2(its:ite,kts:kte)
REAL :: del3(its:ite,kts:kte)
do k = kts, kte
  !DIR$ VECTOR ALIGNED
  do i = its, ite
    del2(i,k)=0.; del3(i,k)=0.
    if (rain(i,k).lt.qmin.and.snow(i,k).lt.qmin) then
      del2(i,k)=1.
    endif
    if(rain(i,k).lt.qmin) del3(i,k)=1.
  enddo
enddo
do k = kts, kte
  !DIR$ VECTOR ALIGNED
  do i = its, ite
    ! if temperature is below freezing
    if(t(i,k).le.t0c) then
      rain(i,k) = rain_freeze(rain,snow,...,del2,del3)
    else
      rain(i,k) = rain_liq(rain,snow,...,del2,del3)
    endif
  enddo
enddo
! similar for snow, water, ice, graupel, etc.
```

**FIGURE 2.7**

After loops were split, the compiler was able to vectorize. Note that loop splitting forced promotion of del2 and del3 to higher rank, reducing data locality. These loops can be found in the sample code beginning at line 1038. Note that variable names have been shortened (e.g., “delta2” → “del2”) and code blocks have been abbreviated as function calls in the figure.

## COMPILE-TIME CONSTANTS FOR LOOP AND ARRAY BOUNDS

Some modern Fortran compilers (including the Intel and Cray compilers) are able to generate more efficient code when loop lengths and bounds of array dimensions are known at compile time. Ideally, a compiler would generate the fastest possible code and branch around it if alignment, loop lengths, and memory bounds were not “perfect.” In practice, the complexity of the conditionals that would have to be evaluated before every invocation of a loop would slow down code enough to overwhelm performance benefits in many cases. So user-supplied compile-time information yields performance improvements. Unfortunately, statically declaring array bounds is impractical because modern NWP codes such as NIM allow users to conduct successive runs on different numbers of MPI tasks without the need for recompilation. Run-time specification of array bounds satisfies this requirement while greatly simplifying the MPI-parallel code. On the other hand, for performance-critical operational weather forecasts, a single configuration and MPI task count of the model may be run many thousands of times; in these cases, defining array dimensions statically at compile time to achieve best performance is desirable, given the burden of recompilation is insignificant. Judicious use of information hiding can give the best of both worlds by optionally exposing only inner dimensions as compile-time constants.

The code snippets in Figures 2.8 and 2.9 illustrate this approach. Physics state array “t” is declared as allocatable in module “state_arrays.” Sizes of each array dimension are declared in a separate module “array_sizes.” Sizes of the outer dimensions are declared as variables and determined at run time. Use of cpp macro “_CHUNKSIZE_” allows the size of the innermost dimension, “chunksize,” to be determined at build time (i.e., when _CHUNKSIZE_ is defined) or at run time. A switch is added to the build automation to optionally set _CHUNKSIZE_ to a user-specified value (i.e., “-D_CHUNKSIZE_=8”).

```fortran
module state_arrays
  real, allocatable :: t(:,:,:)   ! (i,k,j)
end module state_arrays

module array_sizes
  integer :: nlevels       ! vertical (k) size
  integer :: numchunks     ! number of chunks (j)
#ifdef _CHUNKSIZE_
  ! chunk size is a compile-time constant
  integer, parameter :: chunksize = _CHUNKSIZE_
#else
  ! chunk size is set at run time prior to allocations
  integer :: chunksize
#endif
end module array_sizes
```

**FIGURE 2.8**

Modules used to implement optional compile-time constant loop and array bounds without sacrificing the flexibility of allocatable arrays. This code can be found in the sample code beginning at line 3450, in somewhat simplified form.

```fortran
subroutine allocate_state
    use state_arrays
    use array_sizes
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
    use array_sizes
    real, intent(inout) :: t(chunksize,nlevels,numchunks)
    integer :: i,j,k
    do j=1,numchunks
        do k=1,nlevels
            do i=1,chunksize
                t(i,k,j) = …
            enddo
        enddo
    enddo
end subroutine wsm6
```

**FIGURE 2.9**

Optional compile-time constant loop and array bounds in subroutines. Since the compiler cannot see the original allocatable declaration of array “t,” it must use the dummy argument declaration. Thus, the compiler sees a compile-time constant for the size of the inner dimension of “t” and for the length of the “i” loop in the wsm6 subroutine. This code does not appear in the sample code because it uses a somewhat simpler and less flexible approach.

Using both of the above modules, subroutine “allocate_state” sets the outer two dimensions at run time, sets chunksize at run time when _CHUNKSIZE_ is not defined, and allocates “t.” At some point during each model time step, the wsm6 subroutine is called (not shown) and passed “t” as its first argument. All three array dimensions appear in the dummy argument declaration for “t.” Since the compiler cannot see the original declaration of actual argument “t” in module state_arrays, it cannot know that “t” was actually allocated. Therefore, it will see both the size of innermost dimension of “t” and the length of any “i” loops as being compile-time constants inside the wsm6 subroutine. This has significant performance benefit as described below.

The “chunksize” compile-time switch allows a great deal of performance tuning flexibility within a single-source code. For NVIDIA GPUs, setting “chunksize” to be a multiple of streaming multiprocessor size (32) yields the most efficient code. For processors and coprocessors with cores that support vector instructions, such as Intel® Advanced Vector Extensions, it is usually best to set chunksize equal to vector length, as will be seen below.

WSM6 also performs some expensive computations inside “single-column” loops that have “k” innermost. These loops consume about 20% of the execution time. Initially, we were concerned that
