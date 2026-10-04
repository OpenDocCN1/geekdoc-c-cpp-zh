# 2 Applied Time Series Analysis with R

![](bbox=[0.135, 0.125, 0.815, 0.303])

Figure 1.1 Two time series data sets. (a) West Texas intermediate crude. (b) Pennsylvania average monthly temperatures.

12 month (annual) pattern as would be expected because of the natural seasonal weather cycles.

**Using R:** The CRAN package tsw associated with this book contains over 100 data sets containing relation to the material in this book. Throughout the book, whenever a data set being discussed is included in the tsw package, the data name will be noted. In this case the data sets associated with Figure 1a and b wtcrude and patemp, respectively.

Time series analysis techniques are often classified into two major categories: time domain and frequency domain techniques. Time domain techniques include the analysis of the correlation structure, development of models that describe the manner in which such data evolve in time, and forecasting future behavior. Frequency domain approaches are designed to develop an understanding of time series data by examining the data from the perspective of their underlying cyclic (or frequency) content. The observation that the Pennsylvania temperature data to contain 12 month cycles is an example of examination of the frequency domain content. The basic frequency domain analysis tool is the power spectrum.

While frequency domain analysis is commonly used in the physical and engineering sciences, students with a statistics, mathematics, economics, or finance background may not be familiar with these methods. We do not assume a prior familiarity with frequency domain methods, and throughout the book we will introduce and discuss both time domain and frequency domain procedures for analyzing time series. In Sections 1.1 to 1.5 and 1.6 we present a basic introduction to frequency domain analysis and tools. In Section 1.7, we discuss several simulated and real-time series data sets from both time and frequency domain perspectives.