
## TABLE 26.1

WRF Model Configuration for Present Study

| Dynamics | Non-Hydrostatic |
|---|---|
| Spatial coverage | (16°N-28°N, 78°E-94°E) |
| Number of grid points | (198×165) |
| Map projection | Mercator |
| Horizontal grid distribution | Arakawa C-grid |
| Integration time step | 54 sec |
| Initial and boundary conditions | Three-dimensional real data (FNL:1°×1°) |
| Vertical coordinate | Terrain-following sigma coordinate |
| Time integration | 3rd-order Runge–Kutta |
| Spatial differencing scheme | 6th-order differencing |
| Surface layer parameterization | Thermal diffusion scheme |
| Planetary boundary layer | Yonsei University Scheme |
| Cumulus parameterization schemes | Betts–Miller–Janjic scheme |
| Microphysics | WSM class 6 scheme |
| Land surface option | Noah land surface option |
| Radiation scheme | • RRTM for long wave
• Dudhia for short wave |

## TABLE 26.2

Observation Data Sets Used in 3DVAR Assimilation System

| Serial No. | Name of Data Set | Description |
|---|---|---|
| 1 | SOUND | Upper-air observation from RS/RW |
| 2 | SONDE_SFC | Radiosonde at surface |
| 3 | SYNOP | Surface observations from land station |
| 4 | GEOAMV | Geo-stationary atmospheric motion vectors |
| 5 | PILOT | Wind profiles from optical theodolite |
| 6 | METAR | Aerodrome routine meteorological report |
| 7 | SHIPS | Surface observation from a sea station |
| 8 | BUOY | Drifting and moored buoy observations |

3DVAR-based analyses are provided as model initial conditions to simulate the heavy rainfall event during August 9–12, 2016.

## 26.5.1.1 Verification of Wind, Temperature, and Specific Humidity Against GTS Observations

A statistical verification is carried out to assess the performance of 3DVAR during the analysis time 00 UTC August 9 2016. Root mean square (RMSE) of zonal (u) component of wind, meridional (v) component of wind, temperature (T), and specific humidity (q) of 3DV experiment is verified against the GTS observations used in the 3DVAR assimilation cycle. Figure 26.2 shows the averaged RMSE of difference between observations (O) and first guess (B) before assimilation i.e. (O−B) as well as the difference between observations (O) and analysis (A) i.e. (O−A) after assimilation of GTS observations for the meteorological variables. It is clearly seen that mean RMSE of (O−B) is higher than the RMSE of (O−A) for

![](img/81c56bc4b2fca1951aff5e0ab85b66be_408_0.png)

**FIGURE 26.2**  
Averaged root mean square of O–A and O–B for wind (m/s), temperature (°K), and specific humidity (g/kg).

all the variables, which suggests a better agreement of the analysis fields to the observations than first guess. This infers that the GTS observations are correctly assimilated and produced better analyses for ARW modeling system.

## 26.5.1.2 Impact on Initial Vorticity Field

Vorticity is an important parameter for weather and climate modeling. Due to the horizontal shear of the wind field, vorticity is developed around the system and provides circulation in the flow. The relative vorticity along with streamlines at different pressure levels (850 and 500 hPa) from the CNTL and 3DV analyses valid at 00 UTC August 9 2016 is depicted in Figure 26.3(a–b and c–d) respectively. From the figures, it is seen that both the analyses at 850 hPa are showing strong relative vorticity around the MD over head of BoB. However, the magnitude of the vorticity (10–20 × 10⁻⁵) is higher in the 3DV analysis (Figure 26.3(b)) as compared to the analysis from CNTL (Figure 26.3(a)). Similar features are also observed; the relative vorticity is more around 10–15 × 10⁻⁵ in the 3DV analysis (Figure 26.3(d)) at 500 hPa pressure level as compared to CNTL (Figure 26.3(c)). Overall, the stronger vorticity features with well-organized convergence zone around the MD are found in 3DV analysis as compared to CNTL analysis.

## 26.5.2 Impact on Model Simulation

## 26.5.2.1 Vertical Cross Section of Moisture Fluxes

Convection plays an important role in the development of meteorological systems. To diagnose the effect of assimilation of observations in the model simulation, the moisture convection of horizontal moisture flux and vertical moisture flux are analyzed during the life span of the MD (00 UTC 09 to 12 UTC August 11 2016). The time-pressure cross section of horizontal and vertical moisture fluxes from CNTL and 3DV simulations is depicted in Figure 26.4(a–b and c–d) respectively. During the depression stage (09 UTC 9 to

![](img/81c56bc4b2fca1951aff5e0ab85b66be_409_0.png)

![](img/81c56bc4b2fca1951aff5e0ab85b66be_409_1.png)

![](img/81c56bc4b2fca1951aff5e0ab85b66be_409_2.png)

![](img/81c56bc4b2fca1951aff5e0ab85b66be_409_3.png)

![](img/81c56bc4b2fca1951aff5e0ab85b66be_409_4.png)

# FIGURE 26.3

Vorticity (shaded; × 10⁻⁵) and streamlines at 850 hPa pressure level from (a) CNTL and (b) 3DV experiments valid at 00 UTC August 9 2016 (model initial time). (c–d) are the same as (a–b) but at 500 hPa pressure level.

00 UTC August 10 2016), the horizontal moisture flux obtained from the 3DV experiment (Figure 26.4(b)) shows higher positive fluxes (14×10⁻³ g kg⁻¹s⁻¹) extended up to 750 hPa as compared to the CNTL (Figure 26.4(a); 6×10⁻³ g kg⁻¹s⁻¹). It is also seen that the 3DV experiment simulated the maximum horizontal moisture flux (30–36×10⁻³ g kg⁻¹s⁻¹) extended upto 500 hPa during deep depression stage (03 UTC 10 to 03 UTC August 11 2016). The horizontal moisture flux is gradually decreased afterwards. The simulated horizontal moisture fluxes from the CNTL experiment also followed the same trend as was noticed in the 3DV experiment during different stages of the MD. However, the CNTL experiment is able to simulate the maximum horizontal moisture flux around 28–30×10⁻³ g kg⁻¹s⁻¹ extended upto 550 hPa during the deep depression stage of the MD. At the same time, the vertical moisture fluxes extended from the lower to the upper atmosphere in both the simulations (Figure 26.4(c) and(d)) during the deep depression stage of the MD. But the maximum value of vertical moisture flux (20×10⁻³ g kg⁻¹s⁻¹) is simulated by the 3DV simulation (Figure 26.4(c)) as compared to the CNTL simulation (Figure 26.4(d); 7×10⁻³ g kg⁻¹s⁻¹).

## 26.5.2.2 Intensity Prediction

The time series of intensity in terms of 10-m maximum sustainable wind (MSW) and absolute error (AE) of MSW along with gain skill (%) of 3DV with respect to CNTL simulation is illustrated in Figure 26.5(a) and (b). The AE of MSW is calculated against the IMD

![](img/81c56bc4b2fca1951aff5e0ab85b66be_410_0.png)

![](img/81c56bc4b2fca1951aff5e0ab85b66be_410_1.png)

![](img/81c56bc4b2fca1951aff5e0ab85b66be_410_2.png)

![](img/81c56bc4b2fca1951aff5e0ab85b66be_410_3.png)

# FIGURE 26.4

Time-pressure cross section of model simulated horizontal moisture flux (×10⁻³ g.kg⁻¹s⁻¹) at the point (22.2°N and 88.6°E) of (a) CNTL and (b) 3DV. (c–d) are the same as (a–b) but for vertical moisture flux.

![](img/81c56bc4b2fca1951aff5e0ab85b66be_410_4.png)

![](img/81c56bc4b2fca1951aff5e0ab85b66be_410_5.png)

# FIGURE 26.5

(a) Time series of maximum sustained wind 10 m and (b) Absolute error of maximum sustained wind 10 m.

observations. It is observed from Figure 26.5(a )that no simulations are able to capture the observed trend of MSW. However, the magnitude of the MSW is reasonably well simulated by the 3DV experiment throughout the forecast hours as compared to the CNTL simulation. From Figure 26.5(b), the AE (m/s) of MSW is significantly reduced in the 3DV simulation compared to the CNTL simulation throughout the forecast period. The mean gain skill of 3DV is about 22% with respect to the CNTL. Thus, 3DV simulation predicted the intensity better in comparison to the CNTL simulation.

## 26.5.2.3 Model Simulated Rainfall

A comparative study of location specific 24 hours accumulated observed from IMD and model-simulated rainfall (cm) is depicted in Figure 26.6(a) and (b) for Day 1 and Day 2 valid at 03 UTC of August 10 and 11 2016 respectively. It is clearly seen that the observed amount of rainfall over the maximum number of stations is well simulated in the 3DV experiment as compared to the CNTL for both the days. During the Day 1 forecast, the 3DV experiment overestimated the rainfall over the station at Salebhatta. Similarly, on Day 2 the CNTL experiment also overpredicted the rainfall over the station at Kalna.

## 26.6 Conclusions

The high-resolution state-of-the-art mesoscale model WRF and 3DVAR analysis systems with single domain (9 km horizontal resolution) are considered to simulate a heavy rainfall event (August 9–12 2016) associated with the MD during the summer monsoon season along the east coast of India. To this purpose, two numerical experiments, i.e CNTL without data assimilation where FNL analyses are provided as IC and BCs to the model and 3DV by assimilating observations from GTS through 3DVAR, are carried out to evaluate the impact of high-resolution analysis. The broad conclusions of this chapter are given below.

The performance of the 3DVAR analysis system is examined during the initial time through various statistical verifications, i.e innovation error of background (O–B) and analysis (O–A) for the meteorological variables, i.e u-wind, v-wind, temperature, and

![](img/81c56bc4b2fca1951aff5e0ab85b66be_411_0.png)

FIGURE 26.6
24 hrs observed and model simulated rainfall (cm) over different stations (a) Day 1 and (b) Day 2 valid at 03 UTC of August 10 and 11, 2016 respectively.
