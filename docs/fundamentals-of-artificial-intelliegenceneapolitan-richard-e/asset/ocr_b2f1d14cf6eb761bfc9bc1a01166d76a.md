![](bbox=[0.13, 0.08, 0.86, 0.35])

Figure 8.11 The decision tree in Figure 8.10 with the actual outcomes augmented by QALEs.

Example 8.8 This example is an elaboration of the previous one. Actually, Streptococcus infection can lead to rheumatic heart disease (RHD), which is less likely if the patient is treated. Specifically, if we treat a patient with Streptococcus infection, the probability of rheumatic heart disease is .000013, while if we do not treat the patient, the probability is .000063. Rheumatic heart disease would be for life. So Amit needs to take all this into account. First, he must determine time trade-off quality adjustments both for having rheumatic heart disease alone and for having it along with a sore throat. Suppose he determines the following:

1 year with RHD is equivalent to .15 well years.
1 year with sore throat and RHD is equivalent to .1 well years.

We then have

```
QALE(60 years, RHD, 3 sore throat days) = .15 (60 - 3/365) + .1 (3/365)
= 8.999589
```

```
QALE(60 years, RHD, 4 sore throat days) = .15 (60 - 4/365) + .1 (4/365)
= 8.999452.
```

We have already computed QALEs for 3 or 4 days with only a sore throat in the previous example. Figure 8.12 shows the resultant decision tree. We solve that decision tree next.

```
EU(RHD_1) = (.000013)(8.999569) + (.999987)(59.999178)
= 59.998515
```