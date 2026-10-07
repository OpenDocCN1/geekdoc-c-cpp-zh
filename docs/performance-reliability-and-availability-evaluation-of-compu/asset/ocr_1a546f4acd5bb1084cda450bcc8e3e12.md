# Workload Characterization

459

```
// the elapsed time

gettimeofday(&end, 0);
long seconds = end.tv_sec - begin.tv_sec;
long microseconds = end.tv_use - begin.tv_use;
double elapsed = seconds + microseconds*1e-6;
printf("Duration: %.3f sec.\n \n",elapsed);
return 0;
```

where the execution time of the Linpack executable is registered in variable elapsed and displayed on the screen as it "Duration". The script file depicted later redirects output to the text file "Linpack.result.txt". Besides, the three pieces of code below were commented. They are:

# Piece of Code 1

# Piece of Code 2

and

# Piece of Code 3

An script (scriptlinpack) was also implemented to execute the benchmark n time (in the case below n = 100.). The script lines are