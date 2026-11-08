
## Studies on Population Dynamics Using Cellular Automata

Rosana Motta Jafelice¹ and Patrícia Nunes da Silva²  
¹Federal University of Uberlândia  
Faculty of Mathematics  
²State University of Rio de Janeiro  
Department of Mathematical Analysis - IME  
Brazil

## 1. Introduction

In this chapter, we present three cellular automata that simulate the behavior of the population dynamics of three biological systems. They are shaped like a torus in which populations coexist artificially. The first one deals with artificially-living fish divided into two groups: sharks (predators) and fish that are part of their food chain (preys) (Edelstein-Keshet, 1988; Renning, 1999-2000). The second model introduces a simulation of the HIV evolution in the blood stream of positive individuals with no antiretroviral therapy (Jafelice et al., 2009). The last model extends the previous one and considers the HIV dynamics in individuals subject to medical treatment and the monitoring of the medication potency and treatment adhesion (Jafelice et al., 2009). For this purpose, a cellular automata approach coupled with fuzzy set theory is developed to study the HIV evolution. When modeling a physical or biological system there are many decisions to make. One of them is related to the kind of approach to take into account. In the “bottom-up” approach the complex behavior of a system emerges from the interaction of basic components. One might ask if it is possible to describe the behavior of complex systems in this way. As a matter of fact, Banks (1971) makes an interesting remark about how physicists were happy to believe the universe is composed of an enormous number of just three basic components: protons, electrons and neutrons. Modeling biological phenomena by realistic models generally leads to large system of nonlinear integro- and partial differential equations. One alternative approach is to consider cellular automata (CA) models. The usefulness of the CA models relies on simplicity and uniformity of their cells and also on their potential to model complex systems. The main idea behind cellular automata models is to consider each position (or region) of a spatial domain as a cell to which is attributed a certain state. The state of each cell is modified according to its own state and the states of its neighbor cells. These states are correlated through a number of simple rules that imitates the biological and physical laws that guide the system behavior (Ermentrout & Edelstein-Keshet, 1993). An important aspect in modelling population dynamics is to take into account the effect of the spatial distribution of population on their dynamics. The CA models can capture this effect (e.g. Czaran 1998; Lee et al. 1995).

## 2. Cellular automata of prey-predator model: Sharks and fish

In this section we discuss a cellular automaton for a predator-prey model proposed by David Wiseman at the University of Western Ontario (see Dewdney 1984). The planet Wa-Tor¹ is a grid shaped like a torus in which coexist artificially fish and sharks. In this planet most of the time fish and sharks move randomly. Fish and sharks can propagate when they have reached the appropriate age. Differently from sharks, fish have a plentiful supply of plankton and sharks have to eat fish in a specific maximal period, otherwise they would starve to death. Thus, the simulation is of a dynamic system of predator-prey type. In his two-dimensional CA, Dewdney (1984) considered a von Neumann neighborhood. That is, each cell is connected with itself and with its four orthogonal neighbors. He compared his results with the theoretical predator-prey relation given by the Lotka-Volterra equations and also with the sizes of the populations of the Canadian lynx and snowshoe hare recorded by the Hudson’s Bay Company over almost fifty years. Our results were obtained using a two-dimensional CA with a Moore neighborhood. That is, each cell is connected with itself, with its four orthogonal neighbors and with its four diagonal neighbors. In both cases, just the earlier states of the cell and its neighbors determine the next time step. These kind of automata closely resembles an evolution equation such as partial differential or integral equations. Our results were compared to the Lotka-Volterra classic model (Edelstein-Keshet, 1988; Murray, 1990) and also with the empirical data from the Hudson’s Bay Company.

### 2.1 Realistic example of predator-prey: Hare and lynx at Hudson’s Bay

In 1850, the Hudson’s Bay Company used to get from trappers pelts of hares and lynxes. The number of hares and lynxes that got into traps were recorded and used by researchers to study competitive interactions models (see Bummel 1974; Stenseth et al. 1998). It is known that the number of the captured animals is proportional to their population, so researchers found populations statistics for those both species for over a large period. Data on the Canadian hare-lynx system based on the hare and lynx fur records of the Hudson’s Bay Company may be found at Elton & Nicholson (1942), Gilpin (1973) and Hewitt (1921). Both populations do not exist independently from one another, because lynxes feed basically from hares. All the records of pelts for each year were analyzed by the ecologist Charles Elton (Elton, 1924) and are presented in the Fig. 1. The figure shows a regular oscillation over ten years in the numbers of both species. They change over 50 fold and up to 100 folds, over the cycle, what makes the amplitude of the oscillation huge. In the next subsections we will see that the classical model presents regular curves and a phase plane that is a perfect cycle while our cellular automaton will present a cycle which will be closer to the Fig. 2. The phase plane graph of a period of thirty years, initiated in 1875, was obtained from the populations data presented in the Fig. 1.

![](img/55ff3770fcfe64effe3c90a4d4692fa6_120_0.png)

Fig. 1. Hares and lynxes population as a function of time (Renning, 1999-2000).

![](img/55ff3770fcfe64effe3c90a4d4692fa6_120_1.png)

Fig. 2. Detail of the phase plane plot of the data presented in Fig. 1 (Murray, 1990).

### 2.2 Classic predator-prey model

The population fluctuations of predators and prey challenged many researchers. What causes the changes in reproduction and survival? Besides the three main factors: food, predation, and social interactions, many other factors might affect these cycles. For instance, Zhang et al. (2007) used partial cross correlation and stepwise multiple regression methods to analyze the effect of climate on the Hudson’s Bay Company’s hare-lynx system (1847-1903). Their results showed that El Niño/Southern Oscillation has small effects on rates of increase in hare and lynx populations. Krebs et al. (2001) were interested in how changes on food can influence the hare cycle while Stenseth et al. (1999) observed that lynx population dynamics are consistent with a regional structure caused by climatic features.

In order to formulate the interaction between preys and predators, a deterministic model (that became a classic model) was used². It is given by the differential equations system:

```
$$\begin{aligned}
\frac{dx}{dt} &= ax - \alpha xy \\
\frac{dy}{dt} &= -by + \beta xy
\end{aligned} \tag{1}$$
```

In this model, the state variables x and y are, respectively, the number of preys and predators in each instant t. The parameters are:

- $a$: preys relative growth rate;
- $\alpha$: predation rate (probability of a predator to kill the prey in each time they encounter);
- $b$: predators mortality rate in the absence of preys;
- $\beta$: preys conversion rate into predators.

Solving the differential equations with the parameters $a = 0.1$, $\alpha = 0.01$, $b = 0.05$ and $\beta = 0.001$, we obtain the graph of the Fig. 3 and the phase plane, Fig. 4.

² See Wangersky (1978) for a review on Lotka-Volterra population models.
