on average, the learning time using a p233 was r=1.57 times the time needed for a c366. This experimental number is very close to the ratio between the two operating frequencies of the two different processors of the two classes of PEs!

![](bbox=[0.165, 0.25, 0.785, 0.58])

Figure 1.21 RMNSE error distribution when one p233 is used and the run lasts for 75s.

To evaluate the performance obtainable with GEFREX we need to introduce two new quantities. Let us suppose we are using p p233 and c c366. A useful piece of information is the equivalent computational power P_{p,c} of these PEs, that is, the sum of their relative performances. So, we have:

```
P_{p,c} = p + r × c
(1.24)
```

where r is the relative speed between one p233 and one c366 (r=1.57 in this case).

A possible way of evaluating the speedup would be to fix a learning error and to see how much time is required to reach this error when P_{p,c} varies from 0 to 1. Unfortunately, this is impossible. In fact, PARGEFREX is mainly a GA. Figure 1.21 shows the distribution of the final error when only one p233 is used and the termination criterion is 75s of learning time. The Figure shows the great spread in final error obtainable. If we used CE as termination criterion we would have many problems, above all when fuzzy systems with