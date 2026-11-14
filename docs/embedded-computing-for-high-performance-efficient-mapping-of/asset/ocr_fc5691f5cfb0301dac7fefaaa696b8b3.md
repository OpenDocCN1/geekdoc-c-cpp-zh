![](bbox=[0.14, 0.11, 0.86, 0.54])

FIG. 4.15
Task graph (TG) for the Edge Detection UT DSP benchmark.

therefore prime candidates for optimization. To identify hotspots, most developers rely on freely available tools such as GNU gprof, which provides information about the amount of execution of time spent on each module of the program. GNU gcov is another utility, which can be useful in this case to present code coverage results. Such tools exhibit limited capabilities as they do not provide a general mechanism for selecting which regions of code to profile and which regions to ignore. Without relying on profiling tools, one simple strategy to find hotspots is to manually instrument the code as follows:

+   1. Profiling API header. Include the profiling API header at the beginning of each source file to access timing and reporting functions.
+   2. Candidate code statements. Insert timing calls at the beginning and at the end of each function definition to compute the corresponding elapsed time. We only time functions that either have calls or loops.
+   3. Timing report. Before the application terminates, a timing report must be generated and output.