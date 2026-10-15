How might you use a uniform random uniform deviate along with a manipulation of the exponential cumulative distribution function to generate a random exponential deviate?

3. Place the code from “Case Study 2: Bisection Root Finder” into a SAS/IML module. This module should solve the square root of an arbitrary value x where the initial interval endpoints (lo and hi) and the convergence criterion delta are input to this module. How would you build in checks to determine whether the lo and hi values are properly specified?

4. Write a numerical integration module (e.g., trapezoidal rule or Simpson’s rule) to estimate π by finding the area under f(x)=4√1−x² in the first quadrant.

5. Use SAS/IML to merge three different files into one matrix. Output this matrix to a SAS data set. Note: This is a redo of a homework exercise in Chapter 2. Enter each column of the data table into a separate SAS data set, and then import each data set into SAS/IML for processing. Print the resulting SAS data set.

The following description is verbatim from the second exercise in Chapter 2:
Fifty animals were exposed to one of five concentration levels of nitrofen⁴ (10 animals per group, but some observations might be missing in the data). The data was recorded separately for three broods produced by each of the 50 animals. Thus, each animal can have data in each of the three brood data sets. A particular animal is uniquely identified by the ID variable. Produce a combined data set containing observations (animals and IDs) that has data on all three broods. In addition, construct an additional variable for the total number of young produced in all three broods.