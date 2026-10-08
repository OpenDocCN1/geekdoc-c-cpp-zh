![](bbox=[0.223, 0.096, 0.773, 0.333])

**FIGURE 7.10** The largest losses in each 10-day block

![](bbox=[0.193, 0.377, 0.733, 0.603])

**FIGURE 7.11** Losses over a threshold

idea behind the POT method is to choose a numerical threshold for which every loss over that threshold is considered an extreme loss. The number of data points over the threshold can be used to characterise (or fit) a probability distribution i.e. in this case it is known as the generalised Pareto¹¹³ distribution (GPD). Figure 7.11 shows an example of a typical threshold in which only those losses exceeding $90 000 will be considered extreme relative relative to the value of the portfolio.

We have already seen in Chapter 4 how to consider a probability distribution in terms of a CDF i.e.

$F(x) = P(X \le x)$

(7.10)