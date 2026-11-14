could have been used. For example, in the bread rise experiment, the experimenter chose 35, 40 and 45 minutes to study for the levels of rise time. However, the four replicate loaves used for each rise time represent only a sample of the loaves that could have been used in the experiment. For this reason experiments that are used to study variances can be thought of as random sampling experiments or RSE since the factor levels are just a sample of possible levels. For example, consider the data in Table 5.1 patterned after the international survey of apolipoproteins conducted in 1984-85 (see Henderson et al., 1987). Apo A-I is known to help clear cholesterol from arteries. However, the apo genotype yields poor predictive values when screening for clinically defined atherosclerosis. This may be in part due to difficulty in measurement.

Table 5.1 Measured Apo A-I Concentrations by Laboratory Code

| Lab | A | B | C | D |
|---|---|---|---|---|
| 1.195 | 1.155 | 1.021 | 1.163 |
| 1.144 | 1.173 | 1.037 | 1.171 |
| 1.167 | 1.171 | 1.022 | 1.182 |
| 1.249 | 1.175 | 1.064 | 1.184 |
| 1.177 | 1.153 | 1.094 | 1.175 |
| 1.217 | 1.139 | 0.992 | 1.134 |
| 1.187 | 1.185 | 1.072 | 1.169 |
| 1.144 | | | 1.136 |

The purpose of the study was to examine and to quantify the variation among laboratories with respect to their examination of an international reference material for apo A-I and B. Several measurements of the relative concentrations of preparation of the reference material were made by twenty-eight selected laboratories. Table 5.1 shows data from four representative labs. The model for the data can be written as:

\(y_{ij} = \mu + t_i + \epsilon_{ij}, \quad (5.1)\)

where \(y_{ij}\) is the \(j\)th measurement of apo A-I concentration at the \(i\)th laboratory, \(\mu\) is the overall average measured concentration, \(t_i\) is the laboratory effect, and \(\epsilon_{ij}\) is the effect of the \(j\)th measurement in the \(i\)th lab. There was no interest in comparing measured apo A-I concentrations among the specific laboratories in the study since they can be considered a random sample, or representative sample, of several labs around the world. Since the purpose of including several labs was to estimate the component of variance, \(\sigma_t^2\), in measured concentration due to lab, \(t_i\) can be considered a random factor and the experiment can be thought of as a sampling experiment. Note that the Roman letter \(t_i\) was used to represent the random region effect, whereas in model (2.2) in Chapter 2 the Greek letter \(\tau_i\) was used to represent the fixed treatment factor. The replicate measurements of apo A-I made in each lab are only samples of the possible measurements that could be made in that lab. Since multiple measurements were made in each lab in order to estimate \(\sigma^2\),