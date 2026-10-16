# More Attempts on Gompertzian Software Reliability Growth Model (SRGM)

The Gompertz curve is easily one of the widely used models. There are several examples of application of Gompertz to predict software reliability. There have been different adaptations, and different interpretations, each adding to the insight into the Gompertz curve.

The following interpretations of the Gompertz equation by its different users and the values of model constants are noteworthy.

# Stringfellow and Andrews

Stringfellow and Andrews [3] built a Gompertzian SRGM shown in Figure 21.5. They fitted a model with B = 0.001 and C = 0.74. The model was built from failure data collected from a large medical record system, consisting of 188 software components. The low value of B suggests delayed discovery and initially slow progress in testing.

The criteria used by Stringfellow and Andrews in model evaluation are simple and effective:

+   - **Curve fit:** How well a curve fits is given by a Goel–Okumoto (GO) *F* test: the *R*² value.
+   - **Prediction stability:** A prediction is stable if the prediction in a given week is within 10% of the prediction in the previous week.
+   - **Predictive ability:** Error of predictive ability is measured in terms of error (estimate–actual) and relative error (error/actual).

> Stringfellow and Andrews noted that “Gompertz performed better for Release 1 but not for Release 2 and Release 3.”

![](bbox=[0.225, 0.656, 0.775, 0.869])

**Figure 21.5** Stringfellow’s version of Gompertz reliability growth model.