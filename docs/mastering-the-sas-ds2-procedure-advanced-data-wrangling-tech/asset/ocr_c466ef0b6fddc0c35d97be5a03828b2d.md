# Chapter 6: Parallel Processing in DS 11

```
method term();
put 'Thread ' _threadid_ 'processed ' Count ' observations.';
end;
endthread;
run;
quit;
proc ds2;
data scored_thread/overwrite=yes;
dcl thread ScoreIt th;
method run();
  set from th;
end;
enddata;
run;
quit;
```

Here is the log excerpt from the DS2 data program executing a single thread program:

Thread 0 processed 10000 observations.
NOTE: Execution succeeded. 10000 rows affected.
NOTE: PROCEDURE DS2 used (Total process time):
real time 0.45 seconds
cpu time 0.46 seconds

The threaded version is running without error, and it's taking about the same time as the original data program. This is expected, as we did not specify THREADS= so the program was running single. My laptop has four cores, so let's execute this in four threads and whether it improves performance.

```
proc ds2;
data scored_threads/overwrite=yes;
dcl thread ScoreIt th;
method run();
  set from th threads=4;
end;
enddata;
run;
;
```

DS2 log excerpt from the DS2 data program executing four thread programs in parallel:

Thread 3 processed 1634 observations.
Thread 0 processed 2314 observations.
Thread 2 processed 2492 observations.
Thread 1 processed 3560 observations.
NOTE: Execution succeeded. 10000 rows affected.
NOTE: PROCEDURE DS2 used (Total process time):
real time 0.23 seconds
cpu time 0.56 seconds

The multi-threaded version also ran without error, and cut execution time in half!