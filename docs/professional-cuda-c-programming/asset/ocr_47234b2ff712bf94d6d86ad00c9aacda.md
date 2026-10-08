same command. This _syncthreads will ensure that all writes complete before thread 0 starts
scanning, preventing a read-after-write hazard.

Looking at the new output log, a warning has appeared. Note that this hazard occurs between
the two locations in the code, but is a write-after-read hazard instead. This must mean that now
trites are occurring before the scanning can complete. This could only happen if
threads proceed to the next iteration of the loop before the scanning completes. The
kernel must ensure that any additional writes are done to a memory location, the scanning
thread must finish reading its current value. To prevent this, another synchronization point be
ininserted at line 73, forcing all threads to wait for scanning to complete. Rebuild and rerun to see if
this prevents the write-after-read hazard.

You should now have a log file that reports:

```
======== CUDA-MEMCHECK
========RACECHECK SUMMARY: 0 hazards displayed (0 errors, warnings)
```

Great! racecheck finds no hazards in this program. While this does not guarantee that your
program is hazard-free, it is a strong indicator that there are no hazards in shared memory.

# Debugging Summary

This section briefly covered common use cases for kernel and memory debugging tools in CUDA.

You examined cuda-gdb's ability to inspect running program state on the GPU device, dynamically
pasing and resuming threads to check for correctness. An example demonstrated cuda-gdb
can be used to debug a memory error.

You also examined the debugging features of the cuda-memcheck suite and its two tools:
memcheck and racecheck, demonstrated the ability to provide information about
memory errors, as out-of-bounds accesses, NULL pointer references, memory leaks, and
more. racecheck showed similar metrics on potential hazards in shared memory, making
debugging of pathologically difficult situations simpler.

Debugging a CUDA-based application involves inspecting a process running in a separate
space, on physically separated hardware, and outside of any operating system. Although this seems
challenging, the tools presented in this chapter make CUDA applications as straightforward-
ward debugging any host application. Using these tools is crucial to being an effective and eff-
cient CUDA developer, particularly as you begin to explore more advanced topics.

# A CASE STUDY IN PORTING C PROGRAMS TO CUDA C

Previously, this chapter covered the APOD workflow and described how it could be used to port
legacy applications to CUDA. This section will concretely demonstrate these concepts for you
by taking an example legacy application through the full APOD process, ending with an optimized
CUDA application.