of CFs. We define the discrepancy between \(\hat{w}\) and \(\bar{w}\) as aggregation error. At region-sectoral level, this is \((\hat{w}_j^s - \bar{w}_j^s)\). In addition, we use error rate, \((\hat{w}_j^s - \bar{w}_j^s)/\hat{w}_j^s\), to assess the relative, rather than the absolute, effects of aggregation. Error rate is used because the magnitude of aggregation errors can be extremely large due to the different economic scales of sectors in a national economy. The aggregation errors of some small sectors, although important to the sectors themselves, can be overlooked when compared with the aggregation errors of large-scale sectors.

# 3.3 RESULTS

To examine aggregation bias, we set aggregation schemes, determined by Z, randomly using Monte Carlo simulation. The procedure includes the following:

+   1. Randomly determine the number of regions in which aggregation will be conducted.
+   2. Randomly determine which regions are selected for conducting aggregation.
+   3. Randomly determine the number of sectors for each selected region.
+   4. Randomly determine which sectors are selected for aggregation in each selected region.

We repeated this procedure 100,000 times and obtained 100,000 randomly determined aggregation matrices \(Z_s\). For each \(Z_i\), we calculated \(\hat{w}^{Z_i} = ((\hat{w})^s Z_i)^T\), \(\bar{w}^{Z_i} = ((\bar{w})^s Z_i)^T\), \((\hat{w})^s Z_i - (\bar{w})^s Z_i\), and \([(\hat{w})^s Z_i - (\bar{w})^s Z_i]/(\hat{w})^s Z_i\). Because aggregation is conducted randomly many times, aggregation errors and error rates can be considered random variables.

The unaggregated MRIO model we used for this experiment is the AIO 2000. Because the inputs and outputs of Malaysian “unclassified sector” are all “0”s, which can cause a problem in the calculation of the Leontief inverse, we combined the “unclassified sector” with the “public administration” sector and named it the “unclassified” sector in the new MRIO system. For the calculation of carbon intensity, we used the GTAP-E Database Version 6 (Dimaranan, 2006). The GTAP Database Version 6 is the global database representing the world economy for 87 regions and 57 commodities for the year 2001. GTAP-E Database Version 6 provides the emissions data for corresponding regions and sectors in 2001.