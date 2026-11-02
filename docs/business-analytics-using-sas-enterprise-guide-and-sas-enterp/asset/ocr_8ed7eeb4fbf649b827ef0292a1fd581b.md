# Figure 7.16: View the Property Menu for the Add-Cluster Process

![](bbox=[0.15, 0.2, 0.53, 0.78])

Continuous variables come in different scales, such as counts, minutes, and dollars. You will want to standardize these variables for clustering. Otherwise, the variables with the higher scale will have an advantage. Under Train, change Internal Standardization to Range. This option standardizes the values for each variable to a value between 0 and 1. For Clustering Method, select Centroid. This method is usually better than the Ward method for handling contrasting data. Change the Seed Initialization Method to Full Replacement to select seeds that are well-separated. Right click, then click Run. When the run is complete, click on Results.

Output 7.2 shows the upper left and lower left quadrants of in the Results windows four quadrants. Each quadrant offers insights into the results of the process as defined:

+   - *Segment Plot*—the upper left quadrant displays a segment plot of the clustering variables with the highest importance. The results show how the values of age, log, and gender are distributed among the clusters. To see the value of the segment and other statistics, place your cursor on the color within each segment.