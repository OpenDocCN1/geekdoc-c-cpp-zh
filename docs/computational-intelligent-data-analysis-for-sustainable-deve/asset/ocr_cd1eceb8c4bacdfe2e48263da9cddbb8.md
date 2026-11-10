![](bbox=[0.06, 0.082, 0.882, 0.34])

FIGURE 4.3 Temperature prediction in Brazil: Variables chosen through cross-validation.

ensures that only few locations get non-zero weights, and even among these locations, only a few variables are selected. Figure 4.3 shows the locations and features that were consistently selected for the task of temperature prediction in Brazil.

# 4.6 SEASONAL CLIMATE FORECASTING

Seasonal climate forecasts are those beyond the time frame of standard weather forecasts (e.g., 2 weeks) out to a season or two ahead (up to 6 months). Fundamental questions concern what is (and is not) predictable and exactly how predictable it is. Addressing these questions also often gives a good indication of how to make a prediction in practice. These are difficult questions because much in the climate system is unpredictable and the observational record is short. Methods from data mining and machine learning applied to observations and data from numerical climate prediction models provide promising approaches. Key issues include finding components of the climate state-space that are predictable, and constructing useful associations between observations and corresponding predictions from numerical models.

# 4.6.1 What Is the Basis for Seasonal Forecasting?

The chaotic nature of the atmosphere and the associated sensitivity of numerical weather forecasts to their initial conditions is described by the well-known “butterfly effect”—that the flap of a butterfly’s wings in Brazil could set off a tornado in Texas. Small errors in the initial state