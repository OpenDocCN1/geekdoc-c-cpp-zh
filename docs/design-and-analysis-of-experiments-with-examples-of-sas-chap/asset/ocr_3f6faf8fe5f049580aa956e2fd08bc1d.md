One situation where product arrays are actually more efficient is when the experiment is a split-plot. For example, in the lna tile experiment, the noise factor array consisted of simply measuring the response (number of defective tiles in a sample of 100) once for tiles produced in the inner kiln position and again for tiles produced in the outer kiln position. Therefore no additional experimental effort was required. Only eight batches of clay were mixed and molded, but more information was produced by measuring multiple responses for each run of the control factor array. Split-plot designs are sometimes described as super efficient since the sup-plot factors and interactions between sub-plot and whole-plot factors can be tested with the (usually) smaller sub-plot error term.

A third example of a product array parameter design experiment involves the design of a product. The product is the simple circuit for a temperature controller that uses resistance thermometer \( R_T \). The circuit diagram that is shown in Figure 12.5 was described by Taguchi and Phadke (1985). The

# Figure 12.5 Temperature Controller Circuit

![](bbox=[0.215, 0.415, 0.785, 0.605])

response, or measure of product performance, is the resistance value of \( R_T \) at which the relay turns on. Through circuit relations, the response is given by the rational function

\( R_T = \frac{R_3 R_2 (E_2 R_4 + E_0 R_1)}{R_1 (E_2 R_2 + E_2 R_1 - E_0 R_2)} \). (12.2)

The adjustment factor is \( R_3 \), which is known by the circuit relations. The control factors that a designer can specify are the nominal ratings of the resistors and diodes \( A = R_1, B = R_2 / R_1, C = R_4 / R_1, D = E_0 \) and \( F = E_2 \). The noise factors are deviations from the nominal values of the control factors that would be expected due to manufacturing imperfections and deterioration while the product is in use. The objective was to find the nominal settings of the control factors that minimize the variation in \( R_T \) since the desired value of \( R_T \) can always be obtained by adjusting \( R_3 \). This is an example of the