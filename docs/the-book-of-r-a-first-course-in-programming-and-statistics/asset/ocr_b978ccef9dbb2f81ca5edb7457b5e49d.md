# 13.2 Summary Statistics

Now that you've learned the basic terminology, you're ready to calculate some statistics with R. In this section, you'll look at the most common types of statistics to summarize the different types of variables I've discussed.

# 13.2.1 Centrality: Mean, Median, Mode

Measures of centrality are commonly used to explain large collections of data by describing how numeric observations are centered. One of the most common measures of centrality is of course the arithmetic mean. It's considered to be the "balance point" of a collection of observations.

For a set of n measurements labeled x = [x_1, x_2, ..., x_n], you find the sample mean $ar{x}$ as follows:

```
$$\bar{x} = \frac{x_1 + x_2 + ... + x_n}{n} = \frac{1}{n} \sum_{i=1}^{n} x_i \quad (13.1)$
```

So, for example, if you observe the data 2, 4, 4, 3, 3, 2, 2, 2, 4, the mean is calculated like this:

```
$$\frac{2 + 4 + 4 + 3 + 3 + 2 + 2 + 2 + 4}{8} = 2.825$$
```

The median is the "middle magnitude" of your observations, so if you place your observations from smallest to largest, you can find the median by taking the middle value (if there's an odd number of observations) or finding the mean of the two middle values (if there's an even number of observations). Using the notation for n measurements labeled x = [x_1, x_2, ..., x_n], you find the sample median $m_x$ as follows:

+   Sort the observations from smallest to largest to give the "order statistics" $x_1^{(1)}, x_2^{(2)}, ..., x_n^{(n)}$, where $x_j^{(j)}$ denotes the j-th smallest observation, regardless of observation $i, j, k, ...$.

+   Then, do:

```
$$\m_x = \begin{cases} x_{(rac{n+1}{2})} & \text{if } n \text{ is odd} \ \frac{(x_{(rac{n}{2})} + x_{(rac{n}{2}+1)})}{2} & \text{if } n \text{ is even} \end{cases} \quad (13.2)$
```

For the same data, sorting them from smallest to largest yields 2, 2, 2, 3, 3, 4, 4, 4. With n = 8 observations, you have n/2 = 4. The median is therefore as follows:

```
$$\frac{(x_4^{(4)} + x_5^{(5)})}{2} = \frac{(2 + 3)}{2} = 2.6$$
```

The mode is simply the "most common" observation. This statistic is more used with numeric-discrete data than with numeric-continuous, though it is used with reference to intervals of the data (commonly