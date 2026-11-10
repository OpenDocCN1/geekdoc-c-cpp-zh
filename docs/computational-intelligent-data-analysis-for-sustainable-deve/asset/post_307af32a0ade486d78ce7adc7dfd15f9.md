
- Third, constraint reasoning provides a powerful tool in the hand of a policy decision maker as the generation of alternative scenarios is extremely easy and their comparison and evaluation come with no cost. Adjustments can be performed on-the-fly in case the results do not satisfy policy makers or environmental experts. For example, in the field of energy regional planning, by changing the bounds on the amount of energy each source can provide, we can adjust the plan by considering market trends and also the potential receptivity of the region.

### 12.2.1 A CLP Model

To design a constraint-based model for the regional planning activity, we have to define variables, constraints, and objectives. Variables represent decisions that must be taken. Given a vector of activities $A = (a_1, ..., a_{N_A})$, we associate to each activity a variable $G_i$ that defines its magnitude. The magnitude can be represented either in an absolute way, as the amount of a given activity, or in a relative way, as a percentage with respect to the existing quantity of the same activity. In this chapter we use the absolute representation.

As stated above, we distinguish primary from secondary activities: let $A^P$ be the set of indexes of primary activities and $A^S$ the set of indexes of secondary activities. The distinction is motivated by the fact that some activities are of primary importance in a given plan. Secondary activities are those that support the primary activities by providing the needed infrastructures. The dependencies between primary and secondary activities are considered by the following constraint:

$$\forall j \in A^S \quad G_j = \sum_{i \in A^P} a_{ij} G_i$$

Given a budget $B_{Plan}$ available for a given plan, we have a constraint limiting the overall plan cost as follows:

$$\sum_{i=1}^{N_A} G_i c_i \le B_{Plan} \qquad (12.1)$$

Such a constraint can be imposed either on the overall plan or on parts of it. For example, if the budget is partitioned into chapters, we can impose Equation (12.1) on the activities of a given chapter.

Moreover, given an expected outcome $o_{plan}$ of the plan, we have a constraint ensuring to reach the outcome:

$$\sum_{i=1}^{N_A} G_i o_i \ge o_{plan}$$

For example, in an energy plan, the outcome can be to have more energy available in the region, so $o_{plan}$ could be the increased availability of electrical power (e.g., in kilo-TOE, Tonnes of Oil Equivalent). In such a case, $o_i$ will be the production in kTOE for each unit of activity $a_i$.

Concerning the impacts of the regional plan, we sum up the contributions of all the activities and obtain an estimate of the impact on each environmental pressure:

$$\forall j \in \{1,...,N_p\} \quad p_j = \sum_{i=1}^{N_A} m_j^i G_i \qquad (12.2)$$

In the same way, given the vector of environmental pressures $\mathbf{P} = (p_1, ..., p_{N_p})$, one can estimate their influence on the environmental receptor $r_j$ by means of the matrix $\mathcal{N}$ that relates pressures with receptors:

$$\forall j \in \{1,...,N_r\} \quad r_j = \sum_{i=1}^{N_p} n_j^i p_i \qquad (12.3)$$

Moreover, we can have constraints on receptors and pressures. For example, "greenhouse gas emission" (that is, a negative pressure) should not exceed a given threshold.

Concerning objectives, there are a number of possibilities suggested by planning experts. From an economic perspective, one can decide to minimize the overall cost of the plan (that is, in any way subject to budget constraints). Clearly, in this case the most economic energy sources are preferred, despite their potentially negative environmental effects (which could be anyway constrained). On the other hand, one could maintain a fixed budget and maximize the produced energy. In this case, the most efficient energy sources will be pushed forward. Or the planner might prefer a *green* plan and optimize environmental receptors. For example, one

$$\forall i\in A^P\quad G_{i,0}\leq U_i$$

Finally, the region priorities should be compliant with European guidelines, such as the 20-20-20 initiative that aims at achieving three ambitious targets by 2020: reducing by 20% greenhouse gas emissions, having a 20% share of the final energy consumption produced by renewable sources, and improving by 20% its energy efficiency. For this reason, we can impose constraints on the minimum amount of energy $L_{ren}$ produced by renewable energy sources whose set of activities is referred to as $A^P_{ren}$. The constraint that we can impose is

$$\sum_{i\in A^P_{ren}} G_{i,0}\geq L_{ren}$$

## 12.4 THE REGIONAL ENERGY PLAN 2011–2013

The constraint-based model described in previous sections has been used in the planning of the regional energy plan for 2011–2013. The system is implemented in the Constraint Logic Programming language ECLiPSe [1], and in particular uses its Eplex library [15], which interfaces ECLiPSe with a (mixed-integer) linear programming solver. The computation time is not an issue in this application, and it was hardly measurable on a modern computer.

The regional energy plan had the objective of paving the way to reach the ambitious goal of the 20-20-20 directive, in particular having 20% of energy in 2020 produced by renewable sources. This amount considers not only electric power, but the entire energy balance in the region, including thermal energy and transports.

Transports can use renewable energy by using renewable fuels, such as biogas (methane produced from the fermentation of vegetable or animal wastes) or oil produced from various types of crops. Currently, we do not consider this issue.

Thermal energy can be used, for example, for home heating; renewable sources in this case are thermal solar panels (that produce hot water for domestic use), geothermal pumps (that are used to heat or to refresh houses), and biomass plants (that produce hot water used to heat neighboring houses during winter).

The considered electric power plants that produce energy from renewable sources are hydroelectric plants, photovoltaic plants, thermodynamic solar plants, wind generators and, again, biomass power plants.

For each energy source, the plan should provide the following:

- The installed power, in megawatts
- The total energy produced in a year, in kTOE
- The total cost, in M€.

The ratio between installed power and total produced energy is mainly influenced by the availability of the source: while a biomass plant can (at least in theory) produce energy 24/7, the sun is available only during the day, and the wind only occasionally. For unreliable sources an average for the whole year is taken.

The cost of the plant, instead, depends mainly on the installed power: a solar plant has an installation cost that depends on the square meters of installed panels, which in turn can provide some maximum power (peak power).

It is worth noting that the considered cost is the total cost of the plant for the regional system, which is not the same as the cost for the taxpayers of the Emilia-Romagna region. In fact, the region can enforce policies in many ways, convincing private stakeholders to invest in power production. This can be done with financial leverage, or by giving favorable conditions (either economic or other) to investors. Some power sources are economically profitable, so there is no need for the region to give subsidies. For example, currently in Italy, biomass is economically advantageous for investors, so private entities are proposing projects to build biomass plants. On the other hand, biomass also produces pollutants; they are not always sustainable (see [4] for a discussion) so local committees are rather likely to campaign against the construction of new plants. For these reasons, there is a limit on the number of licenses the region gives to private stakeholders for building biomass-based plants.

Technicians in the region estimated (considering current energy requirements, growth trends, foreseen energy savings) the total energy requirements for 2020; out of this, 20% should be provided by renewable sources. They also proposed for this amount a percentage to be provided during the plan 2011 to 2013: about 177 kTOE of electrical energy and 296 kTOE of thermal energy.

Starting from these data, they developed a plan for electrical energy and one for thermal energy.
