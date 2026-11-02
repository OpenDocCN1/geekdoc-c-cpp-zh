experiments that process different-sized rating files. First, we order the Netflix data set by time. Assuming 200 ratings made by users every second, the data set is of 200 ratings per second \* 24 (hours) \* 3600 (seconds) \* N records on the Nth day. We run our movie recommendation jobs over the period of days as N = 1, 3, 6 (Figure 2.12) and compare the results.

Understanding how the minimal time interval or frequency of data processing varies according to the data update sizes helps to make scaling decisions on the optimal resource provision settings. Table 2.3 shows the elapsed time of Hadoop jobs with different sizes of input data. The elapsed time implies, given a certain data size, the minimal time required to run the Hadoop application that updates the movie recommendation list. For example, the first entry in Table 2.3 means that given the current capacity, it is only possible to rerun the Hadoop movie recommendation application with a frequency of once per hour for processing rating data updated in 1 day. For any shorter frequencies or larger data sets, more EMR instances need to be provisioned. Further analysis in Figure 2.13 shows the linear trend of the elapsed time of this Hadoop application according to the data sizes.

![](bbox=[0.18, 0.39, 0.82, 0.54])

TABLE 2.3 Elapsed Time of Movie Recommendation Jobs

| Scenario | Data File Size | Records | Elapsed Time |
|---|---:|---:|---:|
| 1 day | 428 MB | 17,280,000 | 56 min |
| 3 day | 1.2 GB | 51,840,000 | 177 min |
| 6 day | 2.4 GB | 103,680,000 | 407 min |

![](bbox=[0.12, 0.685, 0.76, 0.886])