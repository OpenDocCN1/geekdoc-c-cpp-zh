# 506 Performance, Reliability, and Availability of Computational Systems

timely-ordered trace structure (Block I). Line 29 (Block I) stores the transaction trace to a CSV file. Similarly, Line 30 (Block I) stores the byte transferred trace to a CSV file. As mentioned, the flowchart (Figure 24.24) summarizes the set of steps to generate a transaction sample trace.

![](bbox=[0.248, 0.187, 0.751, 0.626])

Figure 24.24 Flowchart that Represents the Customers’ Online Bookstore Transaction Trace.

Executing Program 21, a sample trace of one thousand (1000) transactions was generated. The respective time series is shown in Figure 24.25. Figure 24.26 shows the autocorrelation, a long-range dependence between observations since the autocorrelation is high for large lags. The autocorrelation for lag size equal to 1 is 0.99696 and slowly decreases for the following lags. Even for a lag size equal to 22, the autocorrelation is still 0.932967.

Table 24.30 presents the statistical summary of the time between transactions of the generated workload and the respective bytes transferred in each transaction. The results shown in Table 24.30 are pretty much similar to the statistics shown in Table