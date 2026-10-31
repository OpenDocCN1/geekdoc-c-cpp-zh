![](bbox=[0.27, 0.13, 0.86, 0.44])

Figure 14-7: Graph of Input versus Output Rates

# Benchmarking Complex Components

Benchmarking complex components is, well, complex! Such components typically perform multiple activities, and these activities can be of different types. Complicating things further, different types of activities may consume different levels of resources. Components that manage processes fall into this category, with ActiveMatrix BusinessWorks and TIBCO ActiveMatrix® BPM being common examples.

What makes the benchmarking of these components complex is that there are virtually an infinite number of ways in which the activities can be combined into processes that are then executed by the components. The likelihood that your process will be similar enough to a given benchmark process for those benchmark results to be useful is very small. So how do you go about establishing useful benchmarks for components like these?

The answer is to obtain data about individual aspects of component behavior that you can then combine analytically to get some reasonable estimate of your design’s performance. So what data do you need? In general, you need three kinds:

+   1. Overhead benchmarks
+   2. Individual activity benchmarks
+   3. Common scenario benchmarks