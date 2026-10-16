![](bbox=[0.12, 0.15, 0.88, 0.42])

# Figure 19.5 Historical Weibull model of steel strength.

The fitted curve is shown in Figure 19.5.

The highlight of the model lies in introducing a location parameter that is necessary, in this case, where data have a large minimum value.

# Software Reliability Studies

Defect discovery during the life cycle follows a Weibull curve. The curve mathematically extends to beyond the release date. The tail area depends on discovery rates before release and is governed by the Weibull equation. Figure 19.6 shows a two-parameter Weibull PDF with a shape parameter of 2 and a scale parameter of 20 days, a defect discovery curve, with release date marked; the tail beyond release denotes residual defects.

Figure 19.7 is the cumulative distribution function (CDF) of the same Weibull, but the interpretation is interestingly different.

The y-axis represents the percentage of defects found and is likened to product reliability at any release point. Using this model, we can predict reliability at delivery.

Both Figures 19.4 and 19.5 provide approximate but useful judgments about defect discovery.

> Above all they provide valuable clues to answer the question, to release the product or test it further?

An experienced manager can make objective decisions using these graphical clues. Some organizations have attempted to declare the CDF value at release date as software reliability and use this numerical value to certify the product.

Vouk [8] reported the use of Weibull models in the early testing (e.g., unit testing and integration testing phases) of a very large telecommunication system. It is