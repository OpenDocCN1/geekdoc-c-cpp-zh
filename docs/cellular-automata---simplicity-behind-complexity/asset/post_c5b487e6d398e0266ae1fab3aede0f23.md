
### 3.5 Mobility and diffusion factors

The circulation part of the transport model is written in the pair of equations (20). For deriving the mobility and diffusion factors one can consider that the system has reached a stationary situation where $J_p(t=0) \simeq 0$ and $J_r(t=0) \simeq 0$, then:

$$\frac{D_p}{\mu_p} \simeq \rho_0\left|\frac{dV}{d\rho_0}\right|; \qquad \frac{D_r}{\mu_r} \simeq \rho_0\left|\frac{dV}{d\rho_0}\right| \tag{23}$$

As the urban potential $V$ is approximated by Thomas-Fermi, one gets a generalized expression of $D_p/\mu_p$ as a function of space⁵:

$$\frac{D_p}{\mu_p} \simeq \frac{2\,\varepsilon_p(x,y)\left|1-(d r/d\rho_p)\,\rho_p/m_p\right|}{3\,\rho_p\left|1-(r/\rho_p)\,m_p/m_r\right|^{1/3}} \tag{24}$$

where $\varepsilon_p(x,y) = (\tilde{a}_p^2/2m_p)(3\pi\rho_p(x,y))^{2/3}$ can be considered the isolated contribution of $\rho_0(x,y)$ to Fermi's level. The former applies for genuine stationary conditions, but for a quasi stationary frame there should be a limiting trend as follows:

$$\frac{D_p}{\mu_p} \simeq \frac{D_r}{\mu_r} \simeq \frac{2}{3}\,\varepsilon_p(x,y)/\rho_p \tag{25}$$

Once the $D/\mu$ quotient has been specified for each pixel, a numerical value of each parameter can be found by estimating mobility factors, as in solid state theory:

$$\mu_p = q_p\,\tau_p/m_p; \qquad \mu_r = q_r\,\tau_r/m_r \tag{26}$$

The characteristic time parameters $\tau_p$ and $\tau_r$ can be interpreted as the average free time periods *between relocations* of inhabitants and re-persons. In the case of $\tau_p$, its value is representative of the average time invested daily per inhabitant in terms of displacements (in one direction) for different activities, which for the case study was about 25 min in 1990⁶.

An average measure of $D/\mu$ quotient is given by Einstein’s equation $D_p/\mu_p = D_r/\mu_r = kT/q_p\,[J/(m^2)]$, being for the case study $\mu_{p0}=1.15\,10^{-04}$, $\mu_r=2.59\,10^{-05}$ for the effective mobility factors $[J\cdot m^2/(s\cdot kg)]$ and $D_{p0}=5.91\,10^{-5}$, $D_{r0}=1.51\,10^{-5}$ for the effective diffusion factors $[m^2/s]$. For this case the average values of the parameters are taken as the city average “thermal” expansion, gives a relative surface expansion of 1.65. Since this is practically $(1+\beta_0)$, where $\beta_0 \simeq 0.65$ is the city average quality factor, it gives a net relative expansion of $\beta_0$ per inhabitant in excess, which is in accordance to the fact that excess concentration will be rearranged trying to conserve the former average quality factor.

The mobility and diffusion factors link the daily commutation regime to the expansion regime, in a way that the city structure depends directly on the average relocation time period and vice versa.

⁵ Mobility and diffusion factors vary in space and hence do not follow the analogous relationship to Einstein’s equation $D/\mu = kT/q$. For an explanation on Einstein’s equation see for example Kittel C., 1995.

⁶ Weighted sum of invested time in bus and car journeys not including Luján de Cuyo.

### 3.6 Implementation and testing of the model

The general scheme of calculation associated to the model consists of an iterative process of $n$ periods (annual periods have been used for the case study), in which, as from an initial spatiotemporal uncertainty, associated to the initial state, limits the model space and time resolution and might even cause its instability. It includes the combined effect of errors due to the gathering, sampling and conditioning of demographic and cadastral data, which on the other hand are not strictly co-temporal. For the case study the uncertainty was lower than 1.4 years and a space uncertainty not larger than one pixel (350 × 350 m²). This model has been tested for the case study in quasi stationary conditions. Initial data correspond to Great Mendoza in 1990/1, with the associated characteristic constants previously discussed. Parameters have been kept constant throughout all periods. The results of a simulation for five years show a good correspondence with growth and distribution trends seen in such decade. From the maps one can clearly distinguish how equidensity areas evolve (fig. 6). Only considering the spatial aspects observed here, one can already recognize the principal types of effects that could be expected in mid-term evolutions in any city, as for instance the one conveyed by the seven transition rules of the Batty-Torrens model (Batty M., Torrens P., 2001). It is particularly interesting the depletion effect (sometimes called “donut” effect) seen in the main centre of the city, which here arises naturally as a consequence of resources and inhabitants’ competitive growth and diffusion. This qualitative correspondence to the principal trends of evolution of Great Mendoza during the last decade acquires more importance when considering it together with the reasonable overall temporal behaviour of state variables.

## 4. Some reflections on population growth and economy

Since the beginning of the last century the world is experiencing an important demographic transition, which will probably impact on economic growth. Many demographers and social scientists are trying to understand the key drivers of such transition as well as its profound implications. A correct understanding can help to predict other important trends at global scale, as the primary energy demand and the carbon emission to the atmosphere, which may be leading to an important climate change.

Inspired by the former works, a set of coupled differential equations has been proposed in Puliafito S. Enrique et al. (2007) to describe the changes of population and gross domestic product, modelled as competing-species as in Lotka-Volterra relations. In fact, if the development and population dynamics of cities could be explained in terms of the above given model, it would be natural then to expect that global population growth and economy also follow a predator-prey type model (eq. 19). Based on that, changes of primary energy consumption and carbon emissions would then be modelled similarly. The estimated results for the temporal evolution of world population, gross domestic product, primary energy consumption and carbon emissions were calculated from year 1850 to year 2150. The calculated scenarios are in good agreement with common world data and projections for the next 100 years.

Economic growth models give population growth a major role, but some show population as detrimental to economic growth and others show population as a major contributor. In fact, population growth has two effects: it increases the number of consumers, and it increases the number of workers devoted to productive activity and research. However, population growth increases the scale of the economy, therefore permitting industries, enterprises, and the entire economy to exploit economies of scale. Models based on technological progress or on generation of new ideas generally conclude that population growth and the size of the population have a positive effect on growth of per capita output.

Carbon emission $c$ is strongly coupled to $g$ and $p$, so that a similar set of differential equations as (30) can be suitable to estimate the annual changes in both variables:

$$
\begin{cases}
1/e\,(de/dt) = \varepsilon_1 f_1/e + \varepsilon_2\, p + \varepsilon_3 \\
1/c\,(dc/dt) = \sigma_1 f_2/c + \sigma_2\, p + \sigma_3
\end{cases}
\qquad (31)
$$

where $f_1=c/g$ and $f_2=c/g$, and $f$ is the same function used for the external excitation of $g$ and $p$ in Eq. (30), for the exogenous model; $\varepsilon_1\, c/g$ (%) is the efficiency improvement through more technological investment, $\varepsilon_2\, p$ (%) is the per capita energy consumption, and $\varepsilon_3$ is the residual increase in energy consumption not explained by the other two coefficients, or the natural increase without an external excitation. Same can be said for the natural rate of changes in the carbon emissions. Some results are also shown in Fig. 7.

## 5. Conclusions

Throughout this chapter we have been exploring some of the fundamentals of CA models and the reasons why these are being so widely applied nowadays, particularly to urban systems and ecology, all of which seem to be connected directly with the fact that the transport equations are common as much to the socioeconomic phenomena as to physics. However, it is not immediate that population dynamics can be described similarly by means of reaction-diffusion equations; on the contrary, perhaps on this outstanding fact rests one of the clues to explain how individual behaviour, usually seen at the "microscopic" scale as mostly stochastic or eventually moved by free-will, can fit into the associated collective behaviour seen at the "macroscopic" scale.

In this sense, by means of the bioautomaton theory we have seen that the discrete character of the device-environment interaction leads to describe stationary individual behaviour in a similar way to what is done in quantum stochastic systems. The most important aspect of this similarity is that the statistical behaviour of a bioautomaton can be represented in average by means of wave functions, in a way that stationary or quasi-stationary solutions regarding group behaviour can result from the superposition of individual wave functions. As a wave function is a measure of the probability of a stationary exchange between each device and its immediate surrounding, periodical spatial structures can emerge in certain conditions; hence, stationary dynamics would be described in terms of transport equations framed within some appropriate band theory.

This theoretical speculation is justified for real ecological systems when we consider that social behaviour and complex and regular spatiotemporal structures emerge under conditions where species reach some critical spatial density, thus giving rise to outstanding interaction mechanisms such as templates, stigmergy and self-organization. This suggests that an ecosystem is not the mere association of interactions as a whole or a collection of highly interactive independent elements, but a rather coherent sum of elementary units composed of living individuals and their nearby space-environment, the latter being regarded as a multidimensional representation of the necessary resources for survival, physical space in itself included.

Within this context, a high-density ecosystem can be compared in some sense to an elastoplastic network and thence treated in a similar way to the solid state of matter; that is, as state transitions in a pseudo-crystalline virtual substrate subjected to a general exclusion.
