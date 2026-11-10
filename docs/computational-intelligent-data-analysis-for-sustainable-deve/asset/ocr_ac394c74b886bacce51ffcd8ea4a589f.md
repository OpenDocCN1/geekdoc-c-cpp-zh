![](bbox=[0.12, 0.1, 0.95, 0.42])

**FIGURE 10.5** (See color insert.) Red circles show location of anemometers on rooftop of Museum of Science, Boston, Massachusetts.

we have approximately 2 years’ worth of data collected at a frequency of 1 sample/second with 10-minute averages stored in a separate database.

To derive the wind resource assessment, we train using data from the first year. These data are split into three datasets that we call D₃, D₆, and D₈. The split D₃ has data for 3 months. The split D₆ has 3 additional months, for a total of 6; and D₈ has yet 2 more months, for a total of 8. We further divide each dataset and the second year’s dataset into twelve directional bins of equal size, starting at compass point north (0°). We assume that a linear regression model can be used to identify the wind direction at the Museum of Science. The second year’s dataset becomes our “ground truth”—the true wind resource assessment of the site—and allows us to evaluate and compare the different techniques. We estimate a Weibull distribution model of it for this purpose. As a measure of predictive accuracy, we compare the final estimated Weibull distribution to the ground truth distribution using Kullback-Leibler divergence. The lower this value, the more accurate the prediction:

D<sub>Y||Ŷ</sub> = KL(P<sub>Y</sub>(y) || P<sub>Ŷ</sub>(ŷ))    (10.22)

KL divergence derives the distance between two probability distributions: