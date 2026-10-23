unique abstract and concise representation of the environment, as discussed in the Sec. 3.1.

# 3.1.6. Selection network

The Selection Network associates each element q of the pattern vector with a set of three parameters (k_o^q, k_a^q, k_p^q). At the first occurrence of the pattern q, they are randomly chosen in the range [0,1] with the constraint that: k_o^q + k_a^q + k_p^q = 1. Then, the parameters are modified under the effect of the learning process acting at the efferent (i.e. output) stage of the Representation layer as explained in the following. After completing the learning process and once the Turing pattern q(t) has been generated at each time step t, the corresponding modulation parameters are selected and the behavior that emerges is the weighted sum of the actions suggested by the basic behaviors at that time: A_F(t) = k_o^q · A_o(t) + k_a^q · A_a(t) + k_p^q · A_p(t).

# 3.1.7. Motivation layer and learning process

The association between Turing patterns and modulation parameters is learned through a reward-based reinforcement learning implemented by a simplified Motor Map (MM) [12, 87], whereas the fitness of each action is evaluated by means of a Reward Function (RF), defined as follows:

RF(t) = Σ_i h_i · RF_i(t) (5)

where RF_i represents the degree of satisfaction related to the basic behavior i where i = o, a, p, indicating optomotor, avoidance and phonotaxis reflex, respectively:

RF_o(t) = r_o(|A_F(t − 1)|)
RF_a(t) = Σ_i r_i(e^{d_i(t)}) (6)
RF_p(t) = r_p(|p(t)|)

Here A_F(t) is the action performed at time t, d_i(t) is the distance between the robot and the obstacle detected by the sensor i (i = Front(F), Right(R), Left(L)) and p(t) is the phase between the robot orientation and direction robot-target. The goodness of the behavior can be evaluated at each step via the function DRF(t) = RF(t) − RF(t − 1). A positive (negative) value for DRF(t) indicates a successful (unsuccessful) behavior. Successful behaviors are followed by reinforcement,

![](bbox=[0.07, 0.08, 0.48, 0.33])

![](bbox=[0.07, 0.38, 0.48, 0.58])

Fig. 9. (a) Initial basins of attraction for the 39 patterns and (b) final shape of the basins of attraction for the 15 patterns obtained with the introduction of the learned sensing neurons. The patterns emerged varying initial conditions for top-right corner cell (x-axis) and bottom-left corner cell (y-axis) of a 4 × 4 lattice in the range [−1, 1].

converting the binary scheme of the pattern (i.e. sequence of black and white cells) into an integer value. This code is stored in a Pattern Vector at the first occurrence. Each element of the pattern vector contains the Pattern Code and the step of its last occurrence (Occurrence Lag). Once the external stimuli have been preprocessed, we reset the CNN, set again the initial conditions of the selected cells through the new outputs of the SNs (Fig. 8(b) and let the CNN re-evolve and generate a Turing pattern.

The use of Turing patterns as steady states of a dynamical system implies a form of sensor fusion, i.e. we synthesize heterogeneous sensory information into a single attractor. At each step, the information coming from sensors is fused to form a