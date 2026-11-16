![](bbox=[0.1, 0.08, 0.85, 0.46])

Figure 8.12 A decision tree modeling Amit's decision concerning being treated for streptococcal infection when rheumatic heart disease is considered.

$EU(Treat) = EU(A) = (.999997)(59.998515) + (.000003)(0) = 59.998335$

$EU(Do not treat) = EU(RHD_2) = (.000063)(8.999452) + (.999937)(59.998904) = 59.995691$

$EU(D) = max(59.998335, 59.995691) = 59.998335.$

So now the decision is to treat, but again just barely.

You may argue that, in the previous two examples, the difference in the expected utilities is negligible because the number of significant digits needed to express it is far more than the number of significant digits in Amit's assessments. This argument is reasonable. However, the utilities of the decisions are so close because the probabilities of both anaphylaxis death and rheumatic heart disease are so small. In general, this situation is not always the case. It is left as an exercise to rework the previous example with the probability of rheumatic heart disease being .13 instead of .000063.