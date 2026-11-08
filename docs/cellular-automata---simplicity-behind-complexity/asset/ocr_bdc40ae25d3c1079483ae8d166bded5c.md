analysis are available for the weightings at the current point in time and can be used in the simulation model (see equation (1)).

|  | gas | water | canal | electricity | district heating |
|---|---:|---:|---:|---:|---:|
| 1888 | 24% | 37% | 39% | 0% | - |
| 1918 | 25% | 24% | 27% | 24% | - |
| 1945 | 26% | 23% | 26% | 24% | - |
| 1971 | 25% | 25% | 25% | 25% | 18% |
| 2001 | 25% | 25% | 25% | 25% | 15% |

Table 2. Weightings of the indicators for technical infrastructure.

# 4.5 Formal model

For the formal representation of the model we agree on the following conventions. A cell of the CA is indicated with $H = \{1, 2, ..., H_N\}$. The domain of the variable population density per cell $D^H$ is normalised, i.e. scaled on the interval between 0 and 1 ($D^H = [0, 1]$). In the same way the domains of the supply variables per cell are normalised and indicated as follows: District heating $F^H = [0, 1]$, gas $G^H = [0, 1]$, sewage $K^H = [0, 1]$, water $W^H = [0, 1]$, electricity $S^H = [0, 1]$, public transportation system $O^H = [0, 1]$. From a summary of the supply variables the values of the supply potential field $VH = [0, 1]$ result:

$V^H(t+1)=\omega_1\cdot(\omega_F\cdot F^H(t)+\omega_G\cdot G^H(t)+\omega_K\cdot K^H(t)+\omega_W\cdot W^H(t)+\omega_S\cdot S^H(t))+\omega_O\cdot O^H(t).$  (1)

The factor $\omega$ indicates the factor of a supply variable on the supply potential field $V^H$. The values of a supply variable for a cell $H$ at time step $t$ are calculated by linear interpolation of the collected data at the specified points in time and are taken as exogenous influence variables for the model. The variable for the population potential field is indicated with $P^H = [0, 1]$. The potential values are calculated with the following equation:

$P^H(t+1)=\frac{1}{5}\left(\left(\sum_{B\subseteq U(H)}P^B(t)\right)+D^H(t)\right).$  (2)

The index $B$ indicates a cell in the subset $U(H)$, which consists of the four directly neighbouring cells of a considered cell $H$ without the considered cell $H$ itself. The potential field is recalculated after each time step. The rates for positive $R_p$ and negative $R_n$ population growth results from the sums of the differences of the population densities of the individual cells between two points of time:

$r^H=M^H(T+1)-M^H(T).$  (3)

The points of time of the data assessment are declared with $T=\{1888, 1918, 1945, 1971, 2001\}$. The time steps between these points in time are indicated with $t$. In our case a time step covers one month. In contrast to the normalised population density $D$, the absolute population of a cell is indicated with $M^H$. The absolute change of a cell’s population density between the points in time of data collection is declared with $r^H$. The growth rates $R$ at a time step $t$ depend on the scaling of model time, which is defined by the parameter $c$: