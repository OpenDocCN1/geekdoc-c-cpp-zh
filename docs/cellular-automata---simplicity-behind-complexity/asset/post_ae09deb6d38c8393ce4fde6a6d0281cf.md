
- http://www.sma.df.gob.mx/sma/links/download/archivos/ie06_criterio_pvw23oct08.pdf

- Stauffer, D. (2001). Cellular Automata: Applications. In: *Vector and Parallel Processing-VECPAR 2000*, J. Palma, J. Dongarra & V. Hernández (Eds.), *Lecture Notes in Computer Science*, Vol. 1981/2001, (2001), 199-206, ISSN: 0302-9743. Springer Berlin/Heidelberg.

- Toffoli, T. (1984). Cellular automata as an alternative to (rather than an approximation of) differential equations in modeling physics, *Physica D*, 10, 1, (January 1984) 117-127, ISSN: 0167-2789.

- von Neumann, J. (1951). The general and logical theory of automata. In: *Cerebral Mechanisms in Behaviour: The Hixon Symposium*, L.A. Jeffress (Ed.), (1951), John Wiley, New York. (Reprinted in J. von Neumann, *Collected Works*, A. H. Taub (Ed.), Vol. 5, (1963), 288–328, Pergamon Press, New York)

- von Neumann, J. (1966). *Theory of Self-Reproducing Automata*, Edited and completed by A.W. Burks. University of Illinois Press, ISBN: 0252727339 (ISBN13: 9780252727337), Urbana, Illinois.

- Vilar, L. C. Q. & de Souza, A. M. C. (1994). Cellular automata models for general traffic conditions on a line, *Physica A: Statistical Mechanics and its Applications*, Vol. 211, Issue 1, (October, 1994), 84-92, ISSN: 0378-4371.

- Wagner, P.; Nagel, K. & Wolf, D. E. (1997). Realistic multi-lane traffic rules for cellular automata, *Physica A: Statistical Mechanics and its Applications*, Vol. 234, Issue 3-4, (January 1997), 687-698, ISSN: 0378-4371.

- Wang, B. H.; Kwong, Y.R. & Hui, P. M. (1998a). Statistical mechanical approach to Fukui-Ishibashi traffic flow models, *Physical Review E*, Vol. 57, Issue 3, (March, 1998), 2568–2573, ISSN: 1539-3755.

- Wang, L.; Wang, B. H. & Hu, B. (2001). A cellular automaton traffic flow model between the Fukui-Ishibashi and Nagel-Schreckenberg models, *Physical Review E*, Vol. 63, Issue 5, (April, 2001), [5 pages]: 056117, ISSN: 1539-3755.

- Wang, B. H., Wang, L. & Hui, P. M. (1997). One-Dimensional Fukui-Ishibashi Traffic Flow Model, *Journal of the Physical Society of Japan*, Vol. 66, No. 11, (November 1997) 3683-3684, ISSN: 0031-9015.

- Wang, B. H.; Wang, L.; Hui, P. M. & Hu, B. (1998b). Analytical results for the steady state of traffic flow models with stochastic delay, *Physical Review E*, Vol. 58, Issue 3, (September 1998), 2876-2882, ISSN: 1539-3755.

- Wolfram, S. (1984). Universality and Complexity in Cellular Automata, *Physica D: Nonlinear Phenomena*, Vol. 10, Issues 1-2, (January, 1984), 1-35, ISSN: 0167-2789.

- Wolfram, S. (1986a). Cellular Automaton Fluids I. Basic Theory, *Journal of Statistical Physics*, Vol. 45, Issues 3-4, (November 1986), 471-526, ISSN: 0022-4715.

- Wolfram, S. (1986b). *Theory and Applications of Cellular Automata*. World Scientific, Singapore.

- Wolfram, S. (1994). *Cellular Automata and Complexity: Collected Papers*. Addison-Wesley, Reading, Massachusetts.

- Wolfram, S. (2002). *A New Kind of Science*. Wolfram Media, Inc, 2002.

- Zannetti, P. (1990). *Air Pollution Modelling. Theories, Computational Methods and Available Software*, Computational Mechanics Publications, ISBN: 0442308051, Southampton, Boston, New York.

## Cellular Automata for Traffic Modelling and Simulations in a Situation of Evacuation from Disaster Areas

Kohei Arai, Tri Harsono and Achmad Basuki

*Saga University*  
*Japan*

### 1. Introduction

The traffic flow studies using microscopic simulations (micro traffic model) have leapt with the occurrence of the advancement of computer technology in the last one and a half decades, as shown in (Nagel, K. & Schreckenberg, M., 1992); (Nagel, K., 1996); (Bando, M., et al, 1995).

The evacuation system in the micro traffic simulation model has been studied and reported a couple of years ago. In the early stage, some examples of micro traffic simulation models related to emergency evacuation are investigated by (Sugiman, T. & Misumi, J., 1988); (Stern, E. & Sinuany-Stern, Z., 1989). The modelling system of emergency evacuation in the traffic stated by (Sheffi, Y., et al., 1982); (Hobeika, A.G. & Jamei, B., 1985); (Cova, T.J. & Church, R.L., 1997) has chosen to estimate evacuation time from an affected area using static analysis tools at macroscopic or microscopic levels.

Another research of emergency evacuation at the micro traffic scale was conducted by (Pidd, M., et al, 1996). They developed a prototype of spatial decision support system that can be used for emergency planners to evaluate contingency plans for evacuation from disaster areas. It does not take the interactions between individual vehicles into consideration.

Two basic components of agent-based modeling, i.e. (1) a model of agents and (2) a model of their environment were introduced by (Deadman, P.J., 1999). An individual agent makes a decision based on the interaction between him and the other agents together with localized knowledge (Teodorovic, D.A., 2003).

How evacuation time can be affected under different evacuation scenarios, such as opening an alternative exit, invoking traffic control, changing the number of vehicles leaving a household was observed based on agent-based simulation techniques (Church, R.L. & Sexton, R., 2002). Neighbourhood evacuation plans in an urbanized wildland interface were described by (Cova, T.J. & Johnson, J.P., 2002) using an agent-based simulation model. They were able to assess spatial effects of a proposed second access road on household evacuation time in a very detailed way.

The effectiveness of simultaneous and staged evacuation strategies using agent-based simulation for three different road network structures was presented by (Chen, X. & Zhan, F.B., 2008). They measured the effectiveness based on total time of evacuation from affected areas.

Aforementioned studies described how to evacuate all residents in the affected area, whereas this study evacuates vehicles on the affected road using agent-based modelling. We conduct micro traffic agent-based modelling and simulation for assessment of evacuation time with and without agents from the affected area of the Sidoarjo hot mudflow situation in East Java, Indonesia, called LUSI, which occurred on 29th of May, 2006. Even now, the mud volcano remains at high flow rates (Rai, 2008).

One of the key elements of evacuation from the mudflow disaster is the road as the main traffic connection surrounding the disaster area, and the dike of the hot mudflow is very close to the road (Indahnesia.com, 2007). The vehicle density on the road is high (Mediacenter, 2007).

Our micro traffic agent-based modelling and simulation, other than with/without agent; road traffic (vehicle density) and road networks; driving behaviour such as lane changing, car-following; and unpredictable disturbance due to a difference between disaster speed and vehicle speed are taken into account. Although the proposed simulation is based on the Nagel-Schreckenberg traffic Cellular Automata (CA) model as shown in (Nagel, K. & Schreckenberg, M., 1992) and (Maerivoet, S. & De Moor, B., 2005), lane changing and car-following parameters are specific to the proposed simulation.

The following section describes an overview of the traffic models followed by car-following models. Then the introduction of the CA model, a major topic of the chapter on evacuation simulation, will be explained. An agent-based approach to the CA traffic model for the case of evacuation is presented. Furthermore, the results of the traffic survey are described. The traffic survey is conducted on the specific roadway situated around the hot mudflow disaster area, Sidoarjo, Indonesia. It is found that there are two different types of driver, i.e. usual driver and diligent one. In the next section, a modified car-following model is investigated by taking the behavior of usual and diligent drivers into account. Finally, concluding remarks and some discussions are described.

### 2. Overview of the traffic models

One important portion of the micro traffic model is Car-Following (CF). Studies of car-following models have been proposed to describe the interaction between drivers and vehicles. CF became an important evaluation parameter for intelligent transportation system strategies since 1990. CF theories are based on the assumption that each driver reacts in some specific way to stimuli from the vehicles in front. A very attractive microscopic traffic model called the Optimal Velocity Model (OVM) is proposed by (Bando, M., et al., 1995). It was based on the idea that each vehicle has an optimal velocity, which depends on the following distance of the preceding vehicle. Despite its simplicity and its few parameters, the OVM can describe many properties of real traffic flows, such as the instability of traffic flow, the evolution of traffic congestion, and the formation of stop-and-go waves. OVM used to be calibrated using empirical data provided by (Helbing, D. & Tilch, B., 1998). They stated that when empirical data were used in OVM, it had weaknesses: the OVM has too high an acceleration and an unrealistic deceleration. (Helbing, D. & Tilch, B., 1998) have overcome these problems by using a Generalized Force Model (GFM).

(Jiang, R., et al., 2001) stated that GFM cannot describe the delay time δt and the kinematic wave speed at jam density ρj properly. They therefore proposed the Full Velocity Difference Model (FVDM). FVDM has too high a deceleration since empirical deceleration and acceleration are restricted between the following regions, from −3 m/s² to 4 m/s².
