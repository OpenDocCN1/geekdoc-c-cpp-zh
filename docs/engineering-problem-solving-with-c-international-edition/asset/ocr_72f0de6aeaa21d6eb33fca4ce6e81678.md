3. Suppose Problem 2 asked you to compute the time value that corresponds to the temperature 110°F. What complicates this problem? How many time values correspond to the temperature 110°F? Find each of the corresponding time values using linear interpolation. (You may want to refer to Figure 2.5, which contains a plot of these data with the temperature data on the x-axis and the time values on the y-axis.)

![](bbox=[0.25, 0.18, 0.88, 0.38])

FIGURE 2.5 Time values.

# 2.7 Problem Solving Applied: Freezing Temperature of Seawater

Salinity

In this section, we use the new statements presented in this chapter along with linear interpolation to solve a problem related to the salinity of seawater.

The salinity of seawater is a measure of the amount of dissolved material in the seawater. Seawater is primarily water with about 3.5% dissolved materials (salts, metals, and gases) from volcanic eruptions and the weathering of rocks. The salinity of seawater is a measure of the amount of dissolved material in the seawater. Chlorine represents about 55% of the constituents in seawater, while sodium represents about 30.6%. The remaining primary constituents are sulfate (7.7%), magnesium (3.7%), calcium (1.2%), and potassium (1.1%). Salinity varies from one location to another in the ocean, but typically falls in the range of 33 to 38 parts per thousand (ppt), or a percentage of 3.3 to 3.8.

Salinity is often measured using an instrument that measures the electrical conductivity of the water; the more dissolved materials in the water, the better it conducts electricity. Measurements of salinity are especially important in colder regions because the temperature at which seawater freezes is dependent upon its salinity. The higher the salinity, the lower the temperature at which the seawater freezes. The following table [7] contains a set of salinity measurements and corresponding freezing temperatures:

| Salinity (ppt) | Freezing Temperature (°F) |
|---|---|
| 0 (fresh water) | 32 |
| 10 | 31.1 |
| 20 | 30.1 |
| 24.7 | 29.6 |
| 30 | 29.1 |
| 35 | 28.6 |