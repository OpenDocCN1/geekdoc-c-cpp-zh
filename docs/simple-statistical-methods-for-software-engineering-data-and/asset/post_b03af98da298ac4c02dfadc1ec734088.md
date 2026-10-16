
## Case Study 1: Business Perspectives from CSAT Box Plots

This case study is about managing CSAT across a large organization with four strategic business units (SBUs). The annual average CSAT index of the organization has been computed as 3.217, which is far below the target of 4 in a Likert scale of 1–5. The CSAT data are obtained by a survey of the overall satisfaction of customers. The calculation of the average of ordinal data is a subject of ongoing debate. Strictly speaking, average is meaningless in ordinal data, but average is taken as an effective indicator. It is easier to estimate and report. If we use box plots instead of mean, we tend to see more details of CSAT. If we plot separate box plots for different SBUs, we get more information and an easy intercomparison, as shown in Figure 4.5.

### CSAT Analysis across SBUs

In one glance, we are able to take in several details of CSAT. The linear structure of box plot accommodates several box plots in one chart. In Figure 4.5, there are lower whiskers; the lower whiskers touch the floor level, particularly in SBU 1 and SBU 3. These lower whiskers are the real problems; customers tend to remember negative results longer. If Kano’s model of CSAT can be used, the lower whiskers fall in the zone of asymptotically crashing dissatisfaction.

> The key message of CSAT Box Plots is not in the central values but in the lower whiskers.

![](img/2f042205c6c0e14747f198ed8f9c9f40_85_0.png)

**Figure 4.5** Customer satisfaction analysis across SBUs using box plots.

### BOX 4.3 THE BOX OF THE BOX PLOT

The box plot has a lean structure. It is remarkably simple and uncluttered. The earliest version of the box plot was a straight line. Tukey added the box. The box achieves its purpose by dominating the plot. This is an intended domination. The box has the median and contains 50% of central evidence. The first glance makes us recognize the box and other details are subdued; the box emerges as the primary message. This helps managers to grasp the essential behavior of processes sans the secondary details. Dispersion beyond the box is considered secondary. Outliers are tertiary. Moreover, the box is plain and unpopulated. It is just an outline drawing. For quick decisions regarding budgeting, the box is all we need to consider. For systematic process management, we consider the whiskers. For strategic risk management and problem solving, we consider the outliers. The structure of the box plot helps with this progression of management decisions.

### CSAT Analysis across Attributes

The chart provides a very easy comparison that we can quickly navigate through. Performances in ENGG and TIME have earned the lowest scores. The lower whisker in ENGG touches the floor and provides a red alert to the organization. COMM and PRICE have earned the best scores, assuring customer delight from within the “box” area. If we take the target as 4, then RESP and QUAL still need improvement. The box plots provided very useful information graphically.

### Review Questions

- 1. What are the elements in a box plot?
- 2. What are fences?
- 3. How is the length of a whisker calculated?
- 4. How are the hinges calculated?
- 5. How robust are the rules used in detecting outliers in the box plot?

### Exercises

- 1. Draw a box plot using the data provided in Data 4.1, using the macros provided in Refs. [4] and [5], and interpret the same. You can also download free Excel box plot plotters from the web.
- 2. Draw a box plot of lines of code developed by yourself or various objects. See how the box plot helps in statistical thinking.

3. Draw a box plot of defects based on the following module data. Interpret your findings.
26
23
21
18
18
18
14
14
13
13
12
12

4. Compare the following two sets of rework efforts during testing using two box plots. Interpret your graphs.

| Set 1 | Set 2 |
|-------|-------|
| 12    | 10    |
| 12    | 10    |
| 0     | 9     |
| 5     | 9     |
| 7     | 9     |
| 8     | 7     |
| 9     | 7     |
| 0     | 7     |
|       | 7     |
|       | 6     |
|       | 6     |
|       | 6     |
|       | 5     |
|       | 4     |
|       | 4     |
|       | 4     |
|       | 4     |

### References

- 1. K. W. Haemer, Range-bar charts, *American Statistician*, 2(2), 23, 1948.
- 2. M. E. Spear, *Charting Statistics*, McGraw-Hill Book Company, Inc., New York, 1952.
- 3. K. Potter, *Methods for presenting statistical information: the box plot*, in *In Visualization of Large and Un-structured Data Sets*, GI-Edition Lecture Notes in Informatics (LNI), H. Hagens, A. Kerren and P. Dannenmann (eds.), vol. S-4, pp. 97–106, 2006.
- 4. J. W. Tukey, *Exploratory Data Analysis*, Addison Wesley, Sydney, 1977.
- 5. A. Amir and J. Sundara Pandian, *Complete Business Statistics*, McGraw-Hill, London, 2008.
- 6. A. Bakker, R. Biehler and C. Konold, *Should Young Students Learn about Box Plots?* Curricular Development in Statistics Education, Sweden, 2004.
- 7. R. McGill, J. W. Tukey and W. A. Larsen, Variation of box plots, *American Statistician*, 32(1), 12–16, 1978.
- 8. C. Choonpradub and D. McNeil, Can the box plot be improved? *Songklanakarin Journal of Science and Technology*, 27(3), 649–657, 2005.

## METRICS
II

Deriving metrics from data is the key to observation and understanding. Metrics endow people with objective observations and deeper understanding. In Section II of this book, Chapter 5 is devoted to deriving metrics from data to gain this advantage.

Common metrics for all life cycle phases are not an effective approach. Compartmentalizing metrics helps. A simple way of doing this is to separately discuss development metrics, maintenance metrics, and test metrics. Chapters 6, 7, and 8 are devoted to these three categories of metrics.

The advent of agile methods has redefined the way life cycles are managed and measured. Chapter 9 addresses agile metrics.

## Chapter 5

## Deriving Metrics

## Creating Meaning in Data

Direct observations are also called *base measures* or *raw data*. Such data are either entered in the computer by people or recorded automatically by machines. Automated data collection is gaining currency. When people enter data, they have a chance to see what they are keying in and validate the data. Data caught by machines are not immediately seen by people; such automatic data are visited during report generation or process analysis.

Derived measures are computed from base measures. Derived measures are known by several names. Two of these names are significant: key performance indicators and metrics; we use the term metrics. Errors in base measure propagate into metrics. In a broader sense, metrics also constitute data. However, metrics carry richer information than base measures. We create meaning in data by creating metrics.

### Deriving Metrics as a Key Performance Indicator

Measurement is essentially a mapping process. The primitive man counted sheep by mapping his cattle, one to one, to a bundle of sticks. If a sheep is missing, it will show up as a mismatch. Word was not yet invented, but there was mapping all the same. A similar mapping is performed for function point counting; measurement is seen as a “counting process,” a new name for mapping. The mapping phase in measurement is well described in the COSMIC function point manual. With the help of language, we have given a name for what is counted—software size. With the help of number theory, we assign a numerical value applying rules.

In a similar manner, we count defects in software. Here the mapping is obvious. The discovery of defect is conducted by a testing process. Each defect is given

a name or an identification number. The total number of defects in a given module is counted from the defect log.

Size is a base measure. Defect count is another base measure. The ratio of defects to size is called defect density. It is a derived measure, a composite derived from two independent base measures. It denotes product quality.

Productivity is another example for a derived measure.

Measures are directly mapped values. Metrics are meaningful indicators constructed against requirements.

![](img/2f042205c6c0e14747f198ed8f9c9f40_92_0.png)

A “measure” refers to directly mapped value.
A “metric” refers to a meaningful indicator.

Technically speaking, size is a measure, and complexity is a metric. Arrival time is a measure, and delay in the arrival is a metric.

Metrics carry more meaning than measures. Hence, metrics are “meaningful indicators.”

### Estimation and Metrics

A few metrics such as effort variance and schedule variance are based on estimated and observed values. For instance, the metric effort variance is defined as follows:

Effort variance % = 100 × (Actual effort − Estimated effort) / Estimated effort

This metric truly and directly reflects any uncertainty in estimation.

![](img/2f042205c6c0e14747f198ed8f9c9f40_92_1.png)

Accurate measurement combines with ambiguous estimation to produce ambiguous metrics.

Measurement capability and estimation system support each other. They are similar in so much as both are observations. Metrics measure the past and the present; estimation measures the future.

### Paradigms for Metrics

![](img/2f042205c6c0e14747f198ed8f9c9f40_92_2.png)

> What’s measured improves.
> 
> Peter F. Drucker
