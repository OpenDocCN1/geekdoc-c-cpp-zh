
## Major and Minor Offenses for 1999

![](img/644775a10ad87164013616d709050cee_364_0.png)

FIGURE 11.1 All crimes, major and minor, are plotted on an overlay of census tracts in Philadelphia county during the year 1999. Geographic features of the city such as rivers, parks, bridges, etc., are immediately visible.

### 11.2.1 Conditioning the Data

Behavioral information must be transformed into variables that can be manipulated numerically. While time and place readily lend themselves to such analysis, the type of crime being reported must be inferred from its police description. While the first part of the dataset contains theft-related crimes only, for richer 1999 data, crimes are aggregated into six broader categories by parsing police descriptions for keywords as described in Table 11.2. Aggregation ensures that there are sufficient numbers of events to populate time series, while still making use of nearly 75% of the data available in that year.

We measure crime densities with two different methods of spatial aggregation. In the first, a lattice is laid over a map of the city, and crimes are aggregated to the nearest grid point. In general, any mesh size can be used, but our analysis suggests that a grid producing 50 to 100 locations across the city provides good noise reduction without obscuring patterns.

![](img/644775a10ad87164013616d709050cee_365_0.png)

![](img/644775a10ad87164013616d709050cee_365_1.png)

FIGURE 11.2 A time series plot of citywide theft-related crimes at different time scales. The top figure shows daily theft crimes for the year 1999 where individual events such as holidays are visible. The bottom figure aggregates further into monthly counts, revealing seasonal trends such as increases in thefts during the hot summer months.

The flexible mesh grid allows us to use larger spatial bins for rarer crime types, such as those that are drug related. The second spatial aggregation used were the 381 census tracts from the 2000 U.S. Census for the City of Philadelphia. Census tracts have the nice feature of scaling inversely with population density; thus, areas of the city with small numbers of people (and similarly small amounts of crime) will not be washed out by much higher crime counts in the more dense city center. In addition to convenient scaling properties, the use of census tracts also allows us to incorporate various socioeconomic and demographic data that might be related to crime. Finally, census tracts provide an immediately recognizable unit of analysis for policy makers.

Percentage Breakdown of Crime Type

![](img/644775a10ad87164013616d709050cee_366_0.png)

FIGURE 11.3  A percentage breakdown of different crimes based on incident reports.

**TABLE 11.2  Categorical Groupings of Different Crime Types for the 1999 Data**

| Category | Offenses Included | Crimes (%) |
|---|---:|
| All | All reported offenses | 211,606 (100%) |
| Automobile | Auto theft, major traffic | 16,005 (7.6%) |
| Theft | Burglary, robbery, auto | 80,290 (38%) |
| Violent | Assault, homicide, gun | 29,908 (14%) |
| Vandalism | Vandalism, graffiti | 17,880 (8.5%) |
| Drug | Possession, sale, DUI | 11,642 (5.5%) |

For each spatial unit, be it on a grid or census tract, a time series is constructed for each category of crime for which data are available. With nearly 10 years of data available, time scales from hours to years are examined. These time series are normalized to have zero mean and unit variance to make use of various statistical tests and to capture changes in crime rates rather than the absolute number of incidents. Overall, the time series produced are mostly stable and stationary, having roughly constant mean and variance. Those that have obvious serial correlations are removed from analysis.

## 11.3 METHODS

Using the conditioned data, we develop analytical tools to achieve the following:

- 1. Identify both spatial and temporal relationships.
- 2. Select an appropriate scale on which to examine these relationships.
- 3. Interpret the sources of any correlation structure.

To address these goals, we combine time-series analysis with results from random matrix theory to quantify the magnitude and significance of correlation in the data. In the process, we draw upon knowledge of similar problems found in neuroscience (correlating spike-train data) and financial economics (finding signal in noisy time-series data) [5, 9, 12, 13, 18].

Although many methods for detecting correlation in space and time exist, the nature of criminal acts and the type of data being used lent itself to the particular tools used in this chapter. For example, while we are looking for correlations in space, it is important that techniques are able to detect nonlocal correlations, whereas two neighborhoods, on opposite sides of the city, have similar crime profiles because of socioeconomic reasons. With this in mind, we rule out models that can capture only local diffusion. Multivariate auto-regressive (MVAR) models that regress time series of a particular location onto other locations and across many lag periods can detect such a structure, but given the extremely large number of spatial locations and the length of time series, these models quickly become large and intractable [11, 23].

We also would like our analysis to speak of specific details of the correlation structure rather than just the distribution of crimes in space or time. While models concerned with speciation in heterogeneous landscapes may provide insight into properties of the distribution of phenomena or events in nonlinear environments (population density, socioeconomic factors, etc.), they have more difficulty telling stories of particular realizations of these distributions in the real geographic space of a city.

Finally, there is also the problem of noise. Our dataset, while large, is very noisy, and any tools and methods used must be able to find and separate signal with confidence. The methodology that follows has the advantage of providing both analytic and computational null models. Random matrix theory presents analytic results for the limiting distributions and statistics of covariance matrices, while artificial crime data can reliably be simulated using a Poisson process in order to achieve a computational null model. With these considerations in mind, the following algorithms and methodology were combined to satisfy our modeling and statistical requirements.

### 11.3.1 Basic Analysis and Statistics

We begin by using basic data analysis techniques and statistics to better understand the data. In general, crime is not distributed uniformly across the city. Instead, the spatial structure is consistent with descriptions of crime “hotspots.” These hotspots are small regions within the city that regularly experience high levels of crime. Characterizing the nonuniform spatial distribution of crime is important when attempting to find relationships between types of crime. For example, Figure 11.4 shows the center of drug-related crimes occupies northwestern Philadelphia, while theft is more prevalent in downtown Philadelphia. We wish to use quantitative tools to measure interactions between these locations.

![](img/644775a10ad87164013616d709050cee_368_0.png)

FIGURE 11.4 The left plot shows the density of drug-related crimes for the year 1999. Hotspots are located mostly in central Philadelphia, whereas many theft-related crimes (on the left) are mostly located in the southern areas of the city.

![](img/644775a10ad87164013616d709050cee_369_0.png)

FIGURE 11.4 (continued) The left plot shows the density of drug-related crimes for the year 1999. Hotspots are located mostly in central Philadelphia, whereas many theft-related crimes (on the left) are mostly located in the southern areas of the city.

In the time domain, we can identify general periodicities within the data through basic Fourier analysis. Ignoring space for a moment, we consider the city in its entirety, creating a time series of citywide crime sampled hourly (Figure 11.5). From these methods we can quantify distinct seasonal trends. Cycles exist from hourly to yearly scales. These periodicities visually coincide with time series showing increases in crime during hot summer months, or decreases in certain types of crime on weekends that produce weekly trends. Cycles on smaller scales such as days may come from differences in day and night crime rates and hourly frequencies may be due to police procedure. This analysis, however, is blind to any measure of auto- or cross-correlation that may occur between locations within the city.

Running basic regressions on these citywide time series shows a number of interesting results. Regressing citywide drug offenses on day of the week, for example, reveals significant correlation. Considering only the day of the week, we are able to account for nearly 60% of the variance in daily drug offenses (Table 11.3). With Sunday being the omitted group, coefficients on dummy variables corresponding to Monday through Saturday
