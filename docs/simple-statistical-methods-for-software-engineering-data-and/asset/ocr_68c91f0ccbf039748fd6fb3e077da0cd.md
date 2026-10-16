# Chapter 10

# Pattern Extraction
Using Histogram

The histogram is easily the most commonly used statistical method. It is used to detect frequency patterns in data.

A histogram is a way to count the number of data points in data intervals. First, the data range that extends from the minimum to maximum value is divided into a certain number of equal intervals. Then we count the number of data points in each interval and tabulate the counts in a table called tally. The frequency table is converted into a bar graph known as a histogram. An example of data creating a tally, constructing a histogram, and deriving a frequency diagram as well as an ogive from the histogram is illustrated in Appendix 10.1.

A histogram of requirements volatility is shown in Figure 10.1. This histogram is similar to the one obtained by Kulk and Verhoef [1], who studied requirements volatility in 84 IT projects comprising 16,500 function points. Requirement changes do vary beyond the traditional limit of 10%.

What draws our attention first in the histogram is its peak. Stable processes have strong peaks. The peak represents the mode of the process. The core process is denoted by the body of the histogram. Almost the entire process results are seen in the core. Outside the core, we can see outliers. Unlike in the box plot, outliers are distinguished by contrasts in the pattern and not by any rules. This histogram is symmetrical. Many metrics exhibit nearly symmetrical shapes; effort variance and schedule variance are well-known examples.

Not every histogram is symmetrical. For example, the histogram of complexity of object oriented structures, measured as weighted methods per class, is shown in Figure 10.2, modeled after the finding of Rosenberg [2].