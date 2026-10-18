```
#Script to reduce the data
$ sed -n '/^OMP/ p; /Completed/{N;N;N;N;N; p;}; /Mop/ p; /^PWR/{N;N;p}' epC_1_244_4_scatter_1.log > epC_1_244_4_scatter_reducedA.log
#strip out unused lines
$ sed -n '/Time/{s/[^0-9.]*\/n/; p}; /threads/{s/[^0-9.]*//g; p}; /Mop/{s/[^0-9.]*//g; p}; /^PWR/{N;N;s/^PWR[*]*\n//;p}' epC_1_244_4_scatter_reducedA.log > epC_1_244_4_scatter_reducedB.csv
#strip out unwanted text
$ sed -n '/^$/{N;N;N;N;N;N; s/\n/,/g; p}' epC_1_244_4_scatter_reducedB.csv > epC_1_244_4_scatter_reducedC.csv
#put in csv format using ",".
```

# FIGURE 25.5

Script to extract desired performance power data and delete unneeded data.

customization without the need to edit and validate each time. Figures 25.6 and 25.7 are examples of both outputs. Perform this data collection for both

```
KMP_AFFINITY = 'scatter,granularity=fine' and
KMP_AFFINITY = 'compact,granularity=fine'.
```

Use another script, such as that shown in Figure 25.7, to extract the data. The sed (Stream EDitor) script in Figure 25.7 extracts the Number of available threads, CPU time, Mop/s total, Mop/s/thread, Total power for win 0, and Total power for win 1. It then places the result in a CSV data format.

(For the coprocessor, there is little documentation for the format of the data output of /sys/class/micras/power outside of the source code, and even that poorly defines what exactly “win 0” and “win 1” are other than that they are power averages over some interval. See the article, https://software.intel.com/en-us/articles/measuring-power-on-intel-xeon-phi-product-family-devices. Try using one versus the other to see if there are any significant differences.)

Use your own favorite tool to plot the result. We used Microsoft Excel to import, reduce, and plot the data.

Obtain two plots for this data, Performance/Power, and Power/Thread Number. Both provide insight into how affinity can influence application power consumption. Your plots should be very similar to Figures 25.8 and 25.9. Figure 25.8 shows the performance per watt (Mops/s/W) as a function of the number of OpenMP threads used. Figure 25.9 shows power (watts) by itself as a function of the number of threads.

# ANALYSIS

We will first look at the power and performance of the Intel Xeon Phi coprocessor, and then at the Intel Xeon processor. We can point to some of the key features of the plots and deduce their origin. You should compare these plots to your own and see if you can identify similar features. Figure 25.8 shows performance (Mega operations/sec) per power consumed or Mops/s/W. This plot of performance per watt is perhaps the most dramatic evidence of the influence of OpenMP affinity on the power consumed by an application.

What is the largest difference you see between the scattered affinity results verses compact? Figure 25.8 shows that at points, scattered affinity has a more than two Mop/s greater performance per watt than if compact affinity were used instead. As a sanity check, verify that the two plots converge