situation in Sidoarjo hot mudflow disaster that the road structure is straight road, one-way direction, and has some of traffic lanes, as well as there is no traffic light over there. With regard to the unpredictable disturbance properties, it has constant speed and same direction with vehicle on unidirectional road. Besides that the disaster comes from the one of the ends of the road. These conditions are appropriated with the real condition of Sidoarjo hot mudflow.

![](bbox=[0.25, 0.192, 0.709, 0.503])

Fig. 1. Diagram block of evacuation simulation in the micro traffic

The other subsystem: vehicle generation, it is determined by a random number generation. It provides positions and speeds of all vehicles. Furthermore, we determine the driving behaviour. This study uses modified driving behaviour of Nagel-Schreckenberg proposed by using traffic Cellular Automata (Nagel, K. & Schreckenberg, M., 1992). We add two parameters in their model those are lane-changing and car-following. All the parameters of driving behaviour used in the proposed simulation are acceleration, braking, probability of speed, lane-changing, car-following, and agent. The overall simulation flow with the parameters used is shown in Fig. 1.

As the simulation results, we evaluated performance of the proposed driving behaviour (driving behaviour with agent) by compare it to the driving behaviour based on Nagel-Schreckenberg (without agent) for vehicle evacuation simulation from the affected disaster area of Sidoarjo. Thus, the simulation with and without agent cars is shown in this section.

# ## 4.2 Simulation procedure

The steps of proposed simulation model are preparation of road structure, vehicle generation, interpretation of unpredictable disturbance, and driving behaviour.

# ### 4.2.1 Preparation of road structure

The assumed road structure is shown in Fig.2. The realistic situation of main road structure is very close to mud containment walls (dikes) and the road shape is straight line. High