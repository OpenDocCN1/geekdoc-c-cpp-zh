It can be seen that Equation 12.1 is just a variant of the proper exponential probability density function (PDF) shown as follows:

```
f(t) = λe^{-λt}    (12.3)
```

The cumulative distribution function (CDF) is as follows:

```
F(t) = 1 - e^{-λt}    (12.4)
```

where t is time and λ is the rate constant. The mean of this distribution is 1/λ. The standard deviation is also equal to 1/λ.

In engineering, exponential distribution is primarily used in reliability applications. In the context of reliability, λ is known as the failure rate or hazard rate. In a chemical engineering example, corrosion rate is represented in exponential form. In an electrical engineering example, electrical charge stored in a capacitor decays exponentially. In a geophysics example, atmospheric pressure decreases exponentially with height.

Equation 12.3 shows that a single parameter completely specifies the PDF, a unique aspect responsible for the simplicity of the equation.

The other model statistics are as follows:

+   The median is (ln 2)/λ.
+   The mode is 0.
+   The skewness is 2.
+   The kurtosis is 9.

The metric% software defects discovered during system testing decreases exponentially with time, as shown in Figure 12.3. Initial test effort discovers more defects, and subsequent tests begin to show lesser results, a common experience in software testing. We assume that risky modules are tested first, as per a well-designed test strategy. Representing defect metrics is a classic application of the exponential model.

Defects found in a testing day are counted and summed up to obtain Figure 12.3. The x-axis of the plot could be test day or even calendar day. We can plot total defects found every week and establish the exponential nature.

In reliability analysis, the median value (ln 2)/λ is called half-life. The mean 1/λ is known as mean time to fail (MTTF). Also, f(t) = e^{-λt} is known as survival function or reliability function. If the MTTF of a bulb is 400 hours, the corresponding f(t) would define the reliability of the bulb. As time goes on, the reliability would decrease, notably after 400 hours, and the reliability of the bulb can be calculated directly from the following expression:

```
Bulb reliability = e^{-(t/400)}
```