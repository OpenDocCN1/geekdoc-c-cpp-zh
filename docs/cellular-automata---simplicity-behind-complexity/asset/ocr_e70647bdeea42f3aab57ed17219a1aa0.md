# 3. CA model of urban growth in Riyadh, Saudi Arabia

The first case study will assess the likely impact of several new towns and satellite centres around the city of Riyadh, Saudi Arabia. Due to the discovery of oil, Riyadh has experienced significant growth over the last 60 years. The population of Riyadh has increased from 25,000 in the 1930s to 2.5 million by the early 1990s. The current rate of population growth is around 8.1% per annum and the city is expected to reach 10 million people by 2020. The spatial expansion of the city has also seen dramatic changes, growing from a geographical extent of less than 1 km² in the 1920s to over 1,150 km² by 2004 (ADA, 2004).

To manage this high rate of urban growth and change, the Saudi Arabian government has instigated a series of master plans for Riyadh. The main aim of these plans is to re-structure and direct urban expansion to achieve sustainable development in the future (ADA, 2004). To ensure that the master plan will have beneficial effects on the urban fabric and population of the city, policy makers require a planning support tool that has the capability of simulating the complexities of managed urban growth over the next 15 years. The model outlined by Al-Ahmadi et al. (2009a,c) has been developed with this requirement in mind.

# 3.1 CA model details

The model, referred to as the Fuzzy Cellular Automata Urban Growth Model (FCAUGM), is a stochastically constrained CA. The model creates a new urban cell ij at time t+1 if the cell’s development possibility (DP) score is greater than or equal to a transition threshold parameter, λ, as follows:

$$\text{If } DP_{ij}^{t} \geq \lambda \text{ Then } S_{ij}^{t+1}=\text{Urban},\ \text{Otherwise}=\text{Non-Urban} \tag{1}$$

where $S_{ij}^{t}$ is the state of a cell ij at time t+1; $DP_{ij}^{t}$ is the development possibility of a cell ij at time t; and λ is the transition threshold between 0 and 1, which is determined through calibration.

The model defines the state of a cell $S_{ij}^{t+1}$ at t+1 as a function of its development possibility (DP) at time t, which is a function of both the development suitability (DS) of a cell ij at time t, and a stochastic disturbance factor (SDF):

$$S_{ij}^{t+1}=f(DP_{ij}^{t})=(DS_{ij}^{t}*SDF)=(DS_{ij}^{t}*[1+\ln(\gamma^{\alpha})]) \tag{2}$$

where $DS_{ij}^{t}$ is the development suitability of a cell ij at time t; γ is a uniform random variable within the range [0,1]; and α is the dispersion parameter which controls the size of the stochastic perturbation. The development suitability, $DS_{ij}^{t}$, of a cell ij is a function of four driving forces which potentially contribute and affect the spatial patterns of urban growth:

$$DS_{ij}^{t}=f(TSF_{ij}^{t},UAAF_{ij}^{t},TCF_{ij}^{t},PPRF_{ij}^{t}) \tag{3}$$

where $TSF_{ij}^{t}$ is the transport support factor of a cell ij at time t; $UAAF_{ij}^{t}$ is the urban agglomeration and attractiveness factor; $TCF_{ij}^{t}$ is the topographical constraint factor; and $PPRF_{ij}^{t}$ is the planning policies and regulation factor. The four driving forces of urban growth (TSF, UAAR, TCF and PPRF) are themselves functions of fuzzy input variables as shown below:

$$TSF_{ij}^{t}=f(ALR_{ij}^{t},AMR_{ij}^{t},AMJR_{ij}^{t}) \tag{4}$$