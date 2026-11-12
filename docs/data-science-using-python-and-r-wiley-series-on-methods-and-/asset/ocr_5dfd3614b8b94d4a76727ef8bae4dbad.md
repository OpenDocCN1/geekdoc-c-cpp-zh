Overall Model Cost\(_{Model2}\)
= FP \cdot Cost\(_{fp}\) + TP \cdot Cost\(_{tp}\)
= 2451 \cdot $10 + 1322 \cdot -$40
= -$28,370

Then, the model profit per customer for each model is given as:

Profit per Customer\(_{Model1} = \frac{-Overall Model Cost_{Model1}}{GT} = \frac{\$17,350}{11,554} = \$1.5016\)

Profit per Customer\(_{Model2} = \frac{-Overall Model Cost_{Model2}}{GT} = \frac{\$28,370}{11,554} = \$2.4554\)

In other words, we increased the retailer’s profits by almost 64%, simply from accounting for the unequal error costs!

# 7.9 DATA-DRIVEN ERROR COSTS

In this era of big data, businesses should leverage the information in their existing databases in order to help uncover the optimal predictive models. In other words, as an alternative to assigning error costs because “these cost values seem right to our consultant” or “that’s how we have always modeled them,” we would instead be well advised to listen to the data and learn from the data itself what the error costs should be. Let us illustrate the power of data-driven error costs by continuing our example.

Recall that our only nonzero costs were \(Cost_{fp} = \$10\) and \(Cost_{tp} = -\$40\). Fortunately, however, we have access to data that would give us a better idea of \(Cost_{tp}\), namely the predicted Sales per Visit. This predictor provides the average amount of money spent per visit for each customer. So, if we calculate the mean Sales per Visit across all customers, we could use this as a better estimate of how much the customers would come and spend, on average. Our previous estimate was $40. But the mean Sales per Visit for all records in the training data set is $113.58. Our data-driven or data-driven cost for true positives is therefore updated to \(Cost_{tp} = -\$113.58\). Unfortunately, there is no analogous data for us to better estimate \(Cost_{fp} = \$10\), which therefore remains at $10. This gives us the revised cost matrix in Table 7.8.

TABLE 7.8 Data-driven cost matrix for the clothing store problem

| | Predicted Category |
|---|---|---|
| | 0 | 1 |
| Actual category | | |
| 0 | Cost\(_{tp}\) = $50 | Cost\(_{fp}\) = $10 |
| 1 | Cost\(_{fn}\) = $50 | Cost\(_{tp}\) = -$113.58 |