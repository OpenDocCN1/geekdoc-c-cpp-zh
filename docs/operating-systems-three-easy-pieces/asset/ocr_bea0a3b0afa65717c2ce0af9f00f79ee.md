# Homework (Simulation)

In this homework, we'll use multi.py to simulate a multi-processor CPU scheduler, and learn about some of its details. Read the related README for more information about the simulator and its options.

# Questions

+   1. To start off, let's learn how to use the simulator to study how to build an effective multi-processor scheduler. The first simulation will run one job, which has a run-time of 30, and a working-set size of 200. Run this job `./multi.py -n -L a:200` on simulated CPU as follows: How long will it take to complete? Turn on the -c flag to see a final answer, and the -t flag to see tick-by-tick trace of the job and how it is scheduled.

+   2. Increase the cache size to make the working set (size=200) fit in cache (which, by default, size=100); for example, `./multi.py -n -L a:300 -M 300. Can you predict how fast the job will run once it fits? (hint: remember the key parameter of the warm_rate, which is set by the -r flag) Check your answer by running with the solve flag (-c) enabled.

+   3. One thing about multi.py is you can see more detail about what is going on with different tracing flags. Run the simulation as above, but this time with time.left tracing (-T). This flag shows both that the job was scheduled on a CPU at each step, as well as much run-time that job has left after each tick has run. What do you notice about how second column decreases?

+   4. Add one bit of tracing, to show the status of CPU cache for each job, with the -c flag. For each job, each cache will either show a blank space (if the cache is cold for job) or a 'w' (if the cache is warm for job). At what point does the cache become warm for job 'a' in this simple example? What happens as you change the warmup_time parameter (-w) to lower or higher values than the default?

+   5. At this point, you should have a good idea of how the simulator works for a single job running on a single CPU. But hey, isn't this multi-processor CPU scheduling chapter? Oh! So let's start working with multiple jobs. Specifically, let's run the three jobs on a two-CPU system (i.e., type `./multi.py -n 2 -L a:100,b:100,c:100`). Can you predict how long this will take, given a round-robin scheduler? Use -c to see it, and dive down into details with -t