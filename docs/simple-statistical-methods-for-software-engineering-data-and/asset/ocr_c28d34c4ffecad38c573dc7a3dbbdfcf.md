The parameters α and β can be extracted by (1) the method of moments (MOM), (2) the maximum likelihood method, and (3) the minimum χ² method. We would pursue the MOM in this chapter; hence, we use the following two relationships:

β is the scale factor = mean of Ln(x) (17.3)

σ is the shape factor = standard deviation of Ln(x) (17.4)

These relationships are inherent in the Excel function LOGNORM.DIST, as we have seen while creating Figure 17.3. Methods 2 and 3 compute parameters by iteration, and it is a good idea to use Equations 17.3 and 17.4 to generate initial values that may help the following iteration runs to converge faster.

Even manual techniques of parameter extraction begin with Equations 17.3 and 17.4. If we apply them to design complexity data, the scale and shape parameters would become 0.771 and 0.896, the starting values.

The NIST suggestion becomes a valuable option: the scale parameter may be taken as Ln(Median(x)) instead of Mean of Ln(x). The scale parameter by NIST option will be 0.693 instead of the standard 0.771. This is based on a logic that log-normal distributions are centered on the median, and we need not search for the scale parameter iteratively.

# Working with a Pictorial Approach

Let us now consider a graphical way of connecting with mathematical distribution. We can construct and use a histogram, known for its pattern extraction capabilities. Such a histogram of design complexity data is shown in Figure 17.4.

The histogram has extracted a distinctive pattern, with well-defined and clearly discernible features: mode (peak), shape, and tail. These graphical features provide guidance in the choice of a sensitive log-normal parameter: the shape factor. Using graphical matching, we can select the most appropriate from a set of design complexity log-normal curves.

A set of log-normal curves are given in Figure 17.5, with four sets of log-normal parameters given as follows:

+   1. Shape 0.7, scale 0.5
+   2. Shape 0.896, scale 0.771 (obtained by MOM)
+   3. Shape 1.1, scale 1.0
+   4. Shape 1.3, scale 1.4

These curves have been obtained iteratively by perturbing the parameter values around an initial value, a second pair of parameters, with a shape of 0.896 and a scale of 0.771, obtained using MOM.