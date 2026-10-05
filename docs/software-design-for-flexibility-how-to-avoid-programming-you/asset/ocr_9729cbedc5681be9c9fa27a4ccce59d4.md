+   1 Constraint propagation was introduced by David Waltz in his doctoral thesis on the interpretation of line drawings [125]. Gerald Jay Sussman and Richard Stallman developed electrical circuit analysis tools based on constraint propagation [119, 114]. Eugene Feuder [39] transformed the constraint-programming ideas into a major intellectual endeavor, with its own journal [24]. Guy Steele's PhD thesis [116] showed how one could construct a programming language based on constraints.

+   2 See [127], page 71.

+   3 There is also a “reason” for the value, indicated by the list beginning with because. In this case the value in the Vega-parallax-distance cell was derived by division of the contents of the AU cell by the colors of the t in the propagator by c:parallax<->distance. The directional division propagator p / was part of the constraint propagator c*, which was itself part of the c:parallax->distance constraint propagator. These reasons can get very verbose. We will omit the “because” part of the results of inquire when they are not helpful.By chasing these reasons recursively one can get a very verbose explanation of the derivation of a value. These reasons are the justifications discussed in section 6.4.2.

+   4 We are lying here! Actually the measurement of Gatewood and Jonge [43] is a bit different. The center of their measurement was 130 milliseconds rather than the 131 that we quote here. We fudged this to make it possible to illustrate a computational point bit later.

+   5 Actually there are some problems with the Hipparcos data. Specifically, the distances measured by Hipparcos to some very bright clusters, such as the Pleiades, are apparently not consistent with better measurements made by very long baseline radio interferometry. This discrepancy does not damage Hipparcos measurements.

+   6 This is why we fudged Gatewood and de Jonge's measurement. Their result would not overlap with the Hipparcos result if we