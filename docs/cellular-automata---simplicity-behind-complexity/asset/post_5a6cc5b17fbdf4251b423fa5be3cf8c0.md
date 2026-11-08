
![](img/55ff3770fcfe64effe3c90a4d4692fa6_22_0.png)

![](img/55ff3770fcfe64effe3c90a4d4692fa6_22_1.png)

Fig. 5. a) Frequency histogram comparing the total number of Evergreen cells located at a certain distance from a main road (A), with the number of Evergreen cells that have changed from Evergreen to Built-up areas when considering their distance to a main road (B); b) Frequency histogram displaying the percentage of cells that have changed from Evergreen to Built-up areas when considering their distance to a main road; the dashed curve represents the cumulative occurrence of the cells located at a certain distance from a main road

![](img/55ff3770fcfe64effe3c90a4d4692fa6_23_0.png)

Fig. 6. Frequency histogram displaying the percentage of cells that have changed from Evergreen to Built-up when considering the number of Built-up cells within 300 m of these cells and graphical interface designed for the selection of the range of values to be considered in the conditional transition rules

| Cell state | Distance to a main road (m) | Number of Evergreen cells located within the first neighborhood ring [0 to 300) m | Number of Built-up cells located within the second neighborhood ring [300 to 540) m | Number of Agriculture cells located within the third neighborhood ring [540 to 1020) m | ..... |
|---|---|---|---|---|---|
| Evergreen | 0 to 427 | 0 to 17 | 0 to 14 | 0 to 168 |  |
|  | 428 to 1408 | 18 to 50 | 15 to 59 | 169 to 258 |  |
|  | 51 to 74 | 60 to 92 |  | 259 to 377 |  |

Table 2. Ranges of values identified from the frequency histogram to be used for determining the conditional transition rules

To convert the conditional rules into mathematical rules, the mean and standard deviation of the previously defined ranges of values are computed. These values become the coefficients of the parameters of the mathematical transition rules. In this model, the coefficients of each transition rule do not lead to a probability of change, but rather to a Resemblance Index (RI) that quantitatively describes the similarity between the neighborhood content of a cell at the time of the simulation and the neighborhood contents that have been used to generate the values of the parameters of the transition rule. If they are very similar, it is likely that the cell should change state for the corresponding type of land use.

RI is inspired by the Minimum Distance to Class Mean remote sensing image classification algorithm (Richards, 2006). This algorithm calculates the mean point in the parameter space for pixels of known classes and then assigns unknown pixels to the class that is arithmetically closest. It is computed for every transition rule using Equation 1.

$RI = \sum_{i=1}^{m} \frac{|n_i - \bar{x}_i|}{\sigma_i}$  (1)

where m is the number of layers (corresponding to the number of driving factors plus the number of land-use classes multiplied by the number of neighborhood rings), nᵢ is the value in layer i, x̄ᵢ is the mean value for layer i in the transition rule and σᵢ is the standard deviation for layer i in the transition rule. If the standard deviation is zero for layer i, then

$\frac{|n_i - \bar{x}_i|}{\sigma_i} = 0$ if $n_i = \bar{x}_i$ or otherwise equals positive infinity.

Accordingly, RI ∈ ℝ⁺ and the smaller RI is, the more similar is the cell neighborhood configuration to the ones used to define the transition rule. The mathematical rules offer greater flexibility compared to the conditional rules as they reflect significant values for each type of land-use change and are more adaptable to the neighborhood composition than the conditional rules identified from specific observations in the historical dataset.

Table 3 presents some values representing the coefficients of the conditional and mathematical rules, respectively for three neighborhood configurations. The Min and Max columns are associated to the conditional transition rule, while the Mean and Standard deviation columns are related to the mathematical transition rule. An example of a mathematical rule defined from these values is,

$RI(\text{rule1, Evergreen to Agriculture}) = \frac{|D.\ main\ road - 259.38|}{173.05} + \frac{|D.\ city\ center - 6272.57|}{1568.91} + \frac{|D.\ river - 3465.61|}{310.77} + \frac{|Ground\ slope - 3.23|}{1.79} + \frac{|N0\_Water - 0.17|}{0.44} + \frac{|N0\_Evergreen - 10.71|}{5.25} + \frac{|N0\_Deciduous - 3.13|}{3.42} + \frac{|N0\_Agriculture - 81.84|}{5.75} + \frac{|N0\_Rangeland / Parkland - 0.04|}{0.29} + \frac{|N0\_Built-up - 0.08|}{0.35} + \{0\ \text{if}\ N0\_Clear-cut = 0; \infty\ \text{otherwise}\} + \frac{|N1\_Water - 0.44|}{0.86} + \frac{|N1\_Evergreen - 19.24|}{10.0} + \frac{|N1\_Deciduous - 4.75|}{3.9} + \frac{|N1\_Agriculture - 170.93|}{11.51} + \frac{|N1\_Rangeland / Parkland - 0.28|}{0.86} + \frac{|N1\_Built-up - 0.33|}{0.63} + \{0\ \text{if}\ N1\_Clear-cut = 0; \infty\ \text{otherwise}\} + \frac{|N2\_Water - 1.46|}{1.94} + \frac{|N2\_Evergreen - 86.53|}{43.49} + \frac{|N2\_Deciduous - 14.53|}{12.15} + \frac{|N2\_Agriculture - 573.8|}{44.90} + \frac{|N2\_Rangeland / Parkland - 1.51|}{3.76} + \frac{|N2\_Built-up - 2.13|}{4.15} + \frac{|N2\_Clear-cut - 0.02|}{0.14}$

where Nx_LandUse is the number of cells of the corresponding land use within neighborhood rings of a cell. All the transition rules are stored in a file, so multiple simulations can be performed without re-calibrating the model.

| Neighborhood ring | Layer | Min | Max | Mean | StdDev |
|---|---|---|---|---|---|
| Cell attributes | Cell state | Evergreen |  |  |  |
|  | Dist. to main road | 0.0 | 780 | 259.38 | 173.05 |
|  | Dist. to city center | 2473.86 | 8696.48 | 6272.57 | 1568.91 |
|  | Dist. to river | 2979.53 | 4048.11 | 3465.61 | 310.77 |
|  | Ground Slope | 0.0 | 7.29 | 3.23 | 1.79 |
| [0-300] m | Nb cells state Water | 0.0 | 2.0 | 0.18 | 0.44 |
|  | Nb cells state Evergreen | 0.0 | 19.0 | 10.71 | 5.25 |
|  | Nb cells state Deciduous | 0.00 | 11.00 | 3.13 | 3.43 |
|  | Nb cells state Agriculture | 66.00 | 93.00 | 81.84 | 5.76 |
|  | Nb cells state Rangeland/Parkland | 0.00 | 2.00 | 0.04 | 0.30 |
|  | Nb cells state Built-up | 0.00 | 2.00 | 0.09 | 0.36 |
|  | Nb cells state Clear-cut | 0.00 | 0.00 | 0.00 | 0.00 |
| [300-540] m | Nb cells state Water | 0.00 | 3.00 | 0.44 | 0.87 |
|  | Nb cells state Evergreen | 0.00 | 32.00 | 19.24 | 10.00 |
|  | Nb cells state Deciduous | 0.00 | 16.00 | 4.76 | 3.91 |
|  | Nb cells state Agriculture | 151.00 | 192.00 | 170.93 | 11.52 |
|  | Nb cells state Rangeland/Parkland | 0.00 | 4.00 | 0.29 | 0.87 |
|  | Nb cells state Built-up | 0.00 | 3.00 | 0.33 | 0.64 |
|  | Nb cells state Clear-cut | 0.00 | 0.00 | 0.00 | 0.00 |
| [540-1020] m | Nb cells state Water | 0.00 | 6.00 | 1.47 | 1.95 |
|  | Nb cells state Evergreen | 2.00 | 205.00 | 86.53 | 43.49 |
|  | Nb cells state Deciduous | 1.00 | 51.00 | 14.53 | 12.16 |
|  | Nb cells state Agriculture | 430.00 | 656.00 | 573.80 | 44.91 |
|  | Nb cells state Rangeland/Parkland | 0.00 | 14.00 | 1.51 | 3.76 |
|  | Nb cells state Built-up | 0.00 | 24.00 | 2.13 | 4.15 |
|  | Nb cells state Clear-cut | 0.00 | 1.00 | 0.02 | 0.15 |

Table 3. Example of data used to establish the conditional and mathematical transition rules

### 2.1.3 Simulation procedure

The simulation procedure includes these main steps.

- The mathematical transition rules previously defined and a land-use map corresponding to the beginning of the simulation are read.
- For each time step, the neighbourhood configuration of every cell is read and the level of correspondence with the parameters of the transition rules is computed.
- With respect to the user-specified constraints and to the influence of each rule, the cells that change state do it according to the rule having the highest level of correspondence.
- To decide which cell should be associated to each type of land-use change, the model recursively sorts the type of land-use changes and for each of them selects the cell having the smallest RI value. Once the required number of cells associated to each type of land-use change is met or when no more cells can be assigned, the model writes the new land-use map and updates the statistics that correspond to the percentage of cells associated to each rule and each type of change.
- If the numbers of cells associated to each rule and each type of land-use change is different than the numbers found from the historical data and previous time steps, a correction is applied at the next time step. For example, if 200 cells are to change from Agriculture to Built-up area but only 150 of them can according to their neighborhood configuration, 50 additional cells will be set to change at the next time step.

Table 4 lists the land-use transitions that were considered during the simulations.

| From | To |
|---|---|
| Evergreen | Agriculture |
| Deciduous | Agriculture |
| Evergreen | Built-up |
| Deciduous | Built-up |
| Agriculture | Built-up |
| Rangeland/Parkland | Built-up |
| Rangeland/Parkland | Agriculture |
| Agriculture | Rangeland/Parkland |

Table 4. Land-use transitions considered during the simulations

Two sets of simulations were run. The first set was to test the model under various conditions. A sensitivity analysis to the cell size and neighborhood configuration was first carried out, followed by a sensitivity of the model to different ranges of values selected from the frequency histograms. Several ways of grouping the data values extracted from the histograms were tested for the calibration of the CA model: 1) the most dominant ranges of values ignoring flat areas, 2) the most dominant range of values concentrated around the mode, 3) the most dominant range of values dispersed away from the mode, and 4) the whole range of values of the histogram. Finally, to assess the importance of the selection of the external driving factors, simulations were conducted using four factors and different combinations of only three external factors.

In each case, the CA was calibrated using the land-use maps of 1985 to 2001, simulations were performed from 2001 to 2006, and the simulated map of 2006 was compared to the reference map of the same year using two similarity measures based on Kappa coefficients. The first measure is the standard Kappa coefficient, which expresses the percentage of
