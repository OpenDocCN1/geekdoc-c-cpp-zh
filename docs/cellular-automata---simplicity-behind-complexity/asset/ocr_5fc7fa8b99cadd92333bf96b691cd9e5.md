time in which the capillaries remain open. This situation may correspond to a large difference between thresholds of the opening and closing of capillaries.

Let’s consider how the above-described functional peculiarities of capillary network influence on the tissues oxygen saturation, Fig.10,a. At the small thresholds difference the tissue oxygen saturation remains approximately constant in the entire range of metabolic activity of tissues. There is a tendency to some increase in the zone of medium metabolic activity with a gradual decrease in the area of high values of metabolic activity.

With increasing the difference of thresholds observes the tendency to increase the tissue oxygen saturation with increase of tissue metabolic activity. This dependency is even more expressed on higher magnitude of thresholds difference.

If the real capillary network has properties similar to those simulated in our investigations, for more severe conditions of organism, the conditions of oxygen delivery to tissues can be improved, due to the activation of the mechanisms of mass transfer, Fig.10,b.

This peculiarity was clearly expressed for low and medium levels of tissue metabolic activity and gradually decreases with increasing of this parameter.

# ## 6. Cellular automaton simulations of arterial and capillary flow interactions

Cardiovascular system (CVS) can be considering as interaction of combination of continual (arterial flow) and discrete (capillary flow) mechanisms (Chernukh & Alexandrov, 1984; Little, 1989; Rushmer, 1976) which interactions have been studied insufficiently at present moment.

The relative regulatory autonomy of peripheral circulatory system can be simulated in more simple way with use of cellular automata models.

We based our investigation assuming that microvascular arterial bed is critically self-organized system, working on the “edge of chaos”. The microvascular arterial network increases or decreases diameter of arterioles and opens or more less capillaries depending on fluctuations of blood flow and pressure.

High sensitivity of capillary network to changes of internal and external conditions as well as a wide range of its oscillatory properties and also experimental data allows to assume that oscillations of peripheral and systemic blood flow can co-interact.

**The purpose** of this part of investigations was to simulate interactions of capillary blood flow and systemic blood flow during the single cycle of heart contraction.

# ### 6.1 Conditions of simulation

+   1. Current level of systemic flow determines the quantity of capillaries, which can work simultaneously in this moment. But cellular automaton opens as much capillaries, as necessary to satisfy the oxygen debt, but not more than permitted.
+   2. A single iteration of CA equals to a time unit.
+   3. The quantity of possibly opened capillary cells is constant during diastole.
+   4. The tissue metabolic activity changes from 0% to 100% with discrete step for every numerical experiment.
+   5. CA opens capillary when average tissue oxygen saturation is lower than “opening threshold”. The number of opened special cells is determined by conditions 1, 3.
+   6. Opened capillary cells closes if an average charge of surrounding tissue cells reaches the value of “closing threshold”.
+   7. The properties of all capillary cells and tissue cells were homogenous throughout CA.