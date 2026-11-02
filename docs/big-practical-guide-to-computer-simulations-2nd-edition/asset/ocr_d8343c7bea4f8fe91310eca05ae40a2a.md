constant time O(1). This is much faster compared to the standard approach which takes O(log N), where N is the number of the possible outcomes.

+   - The Sec. 8.2.4 covers the *rejection method*, which allows one to draw random numbers according to a given probability density, usually applied for non-invertible distribution functions. The section has been extended by the general approach to border the target distribution by arbitrary probability density functions. This enlarges strongly the range of distributions which can be realized by this approach.
+   
+     Furthermore, as an example for generating random points in higher dimensions, drawing points uniformly on the surface of *d-dimensional hyper sphere* is included now.
+   - In Chap. 8 on data analysis, in the Sec. 8.5 on hypothesis test and measuring correlations in data sets, a subsection on the *Receiver-operator characteristic* (ROC) has been included. The ROC is an advanced yet widespread approach which allows for the determination of optimal parameters for hypothesis tests.
+   - Furthermore a subsection (8.5.5) on the *principal-component analysis* has been added. This is the simplest approach to search for the most important “directions” in high-dimensional data.
+   - *Data clustering methods* are an important tool in the analysis of big data sets, since they allow for looking for structure in overwhelming amounts of data. This is a very sophisticated way of data analysis, much beyond the level of averages, histograms and curve fitting. Several approaches, ranging from the most-simple *k-means* method to the advanced hierarchical clustering algorithms are now explained extensively in Sec. 8.5.6.
+   - The Sec. 8.6.2 on *fitting data* using *gnuplot* has been extended by how to restrict ranges of fitting parameters (which is not possible by default) and how to fit functions to multiple sets of data simultaneously.
+   - In the first edition, *gnuplot* was only used to generate “quick and dirty” plots of data. In Sec. 9.2.1 it is now shown how one can generate publication-quality plots using *gnuplot*.
+   - The Sec. 9.2.4 on the ray tracer *Povray* has been extended by some paragraphs which explain how this ray tracer can be used to generated three-dimensional pictures of simulation snapshots.
+   
+     By using sequences of such figures, small movies can be generated easily.