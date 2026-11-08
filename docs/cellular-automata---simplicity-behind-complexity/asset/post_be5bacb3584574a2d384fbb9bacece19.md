
The GFM assumes that the positive $\Delta v$ does not contribute to the vehicle interaction, while the FVDM suggests that it contributes to vehicle interaction by reducing interaction force because $a[V(\Delta x_n(t)) - v_n]$ is always negative and $\lambda\Theta(\Delta v)\Delta v$ is always positive.

$$
\frac{d^2x_n(t)}{dt^2} = a[V(\Delta x_n(t)) - v_n(t)] + \lambda\Theta(-\Delta v)\Delta v + \lambda\Theta(\Delta v)\Delta v \tag{8}
$$

One of the examples of the application of the FVDM on car motion simulation with traffic signal shows that it can describe the traffic dynamics most exactly so that the FVDM is verified as a reasonable and realistic model. On the other hand, real situations exist in between the FVDM and the GFM. In the FVDM, car accelerates more quickly than the car in the GFM. Therefore, the delay time $\delta t$ in FVDM is smaller than that in GFM as is shown in Table 1. Since the empirical deceleration and acceleration are restricted in between the range from -3 m/s² to 4 m/s² (Helbing, D. & Tilch, B., 1998), the FVDM has too high deceleration.

| Model | Delay time $\delta t$ (s) |
| :--- | :--- |
| OVM ($a = 0.85$ s⁻¹) | 1.6 |
| GFM ($a = 0.41$ s⁻¹) | 2.2 |
| FVDM ($a = 0.41$ s⁻¹) | 1.4 |

Table 1. Delay times of car motions from a traffic signal and disturbance propagation speed at jam density in different models (source: [16])

### 3.1.4 Two Velocity Difference Model (TVDM)

Two velocity difference models (TVDM) for a car-following theory are then proposed taking navigation in modern traffic into account. The property of the model is investigated using linear and nonlinear analysis (Ge, X.H., et al., 2008)

Intelligent Transportation System (ITS) plays an important role in the rapid development of modern traffic. By using such navigation system, drivers can obtain the information that they need. In accordance with the above concept, on the basis of the OVM, taking both $\Delta v_n$ and $\Delta v_{n-1}$ into account, (Ge, X.H., et al, 2008) obtain a more useful model called the two velocity difference model (TVDM), the following dynamics equation is expressed,

$$
\frac{d^2x_n(t)}{dt^2} = a\left[V(\Delta x_n(t)) - \frac{dx_n(t)}{dt}\right] + \lambda G(\Delta v_n, \Delta v_{n-1}) \tag{9}
$$

where $G(\cdot)$ is a generic, monotonically increasing function, and is assumed to be a linear form as,

$$
G(\Delta v_n, \Delta v_{n-1}) = p\Delta v_n + (1-p)\Delta v_{n-1} \tag{10}
$$

where $p$ is a weighting value. The proper value of $p$ could lead to desirable results.

## 3.2 Discrete model: cellular automata model

Cellular Automata (CA) is a model that is discrete in space, time and state variables. The latter property distinguishes CA e.g., from discretised differential equations. Due to the discreteness, CA is extremely efficient in implementations on a computer. CA for traffic has been called traffic cellular automata (TCA). Some of the TCA models, i.e.

- Deterministic model: Wolfram’s rule 184 (CA-184)
- Stochastic model: Nagel-Schreckenberg TCA (STCA)

In 1992, Nagel and Schreckenberg proposed a TCA model that was able to reproduce several characteristics of real-life traffic flows, e.g., the spontaneous emergence of traffic jams (Nagel, K. & Schreckenberg, M., 1992). Their model is called the NaSch TCA, but is more commonly known as the stochastic traffic cellular automaton (STCA). It explicitly includes a stochastic noise term in one of its rules.

The computational model in the STCA is defined on a one-dimensional array of $L$ sites and with open or periodic boundary conditions. Each site may either be occupied by one vehicle or it may be empty. Each vehicle has an integer velocity with values between zero and $v_{\max}$. For an arbitrary configuration, one update of the system consists of the following four consecutive steps, which are performed in parallel for all vehicles.

- **1. Acceleration**
  
  $$v_{(i,j)}(t-1)<v_{\max}\land g_{s(i,j)}(t-1)>v_{(i,j)}(t-1)+1$$
  
  $$v_{(i,j)}(t)\leftarrow v_{(i,j)}(t-1)+1 \tag{11}$$
- **2. Braking**
  
  $$g_{s(i,j)}(t-1)\leq v_{(i,j)}(t)\Rightarrow v_{(i,j)}(t)\leftarrow g_{s(i,j)}(t-1)-1 \tag{12}$$
- **3. Randomization**
  
  $$\xi(t)<p\Rightarrow v_{(i,j)}(t)\leftarrow\max[0,v_{(i,j)}(t)-1] \tag{13}$$
- **4. Vehicle movement**
  
  $$x_{(i,j)}(t)\leftarrow x_{(i,j)}(t-1)+v_{(i,j)}(t) \tag{14}$$

$g_{s(i,j)}(t)$ is the space gap at each time step $t$, or the distance to the next vehicle ahead. $\xi(t)$ is a random number, and $p$ is the stochastic noise parameter or slowdown probability.

Through steps one to four, very general properties of single-lane traffic are modelled on the basis of integer-valued probabilistic cellular automaton rules. Already this simple model shows nontrivial and realistic behaviour. Step 3 is essential in simulating realistic traffic flow; otherwise the dynamics is completely deterministic. It takes into account natural velocity fluctuations due to human behaviour or due to varying external conditions. Without this randomness, every initial configuration of vehicles and corresponding velocities reaches a stationary pattern very quickly, which is shifted backwards (i.e. opposite the vehicle motion) by one site per time step.

## 4. Case study on evacuation from disaster-affected area based on agent-based approach

### 4.1 Situation

There are some subsystems in the proposed micro-traffic agent-based modelling and simulation. First is determining the shape of the road structure. It is conducted for the realistic situation in the Sidoarjo hot mudflow disaster that the road structure is a straight road, one-way direction, and has some traffic lanes, as well as no traffic light there. With regard to the unpredictable disturbance properties, it has constant speed and the same direction as vehicles on the unidirectional road. Besides that, the disaster comes from one of the ends of the road. These conditions are appropriate to the real condition of the Sidoarjo hot mudflow.

![](img/55ff3770fcfe64effe3c90a4d4692fa6_213_0.png)

Fig. 1. Diagram block of evacuation simulation in the micro traffic

The other subsystem, vehicle generation, is determined by random number generation. It provides positions and speeds of all vehicles. Furthermore, we determine the driving behaviour. This study uses modified driving behaviour of Nagel-Schreckenberg proposed by using traffic Cellular Automata (Nagel, K. & Schreckenberg, M., 1992). We add two parameters to their model, namely lane-changing and car-following. All the parameters of driving behaviour used in the proposed simulation are acceleration, braking, probability of speed, lane-changing, car-following, and agent. The overall simulation flow with the parameters used is shown in Fig. 1.

As simulation results, we evaluated the performance of the proposed driving behaviour (driving behaviour with agent) by comparing it with the driving behaviour based on Nagel-Schreckenberg (without agent) for vehicle evacuation simulation from the affected disaster area of Sidoarjo. Thus, the simulation with and without agent cars is shown in this section.

### 4.2 Simulation procedure

The steps of the proposed simulation model are preparation of road structure, vehicle generation, interpretation of unpredictable disturbance, and driving behaviour.

### 4.2.1 Preparation of road structure

The assumed road structure is shown in Fig. 2. The realistic situation of the main road structure is very close to mud containment walls (dikes) and the road shape is a straight line. High

the evacuation control centre and transferred to the agent cars through wireless network connection), they could lead the following cars to the safe areas in the fastest way.

### 4.2.4.1 *Modified Driving Behaviour of Nagel-Schreckenberg*

Regarding Equation (11) to Equation (14), STCA has four steps of driving behaviour rule: acceleration, braking, randomization (slowdown probability), and vehicle movement. Our study modifies it by adding two parameters about lane-changing and car-following. It is based on (Maerivoet, S. & De Moor, B., 2005 B), which stated that the basic implementation of a lane-changing model in traffic cellular automata setting leads to two sub-steps that are consecutively executed at each time step of the cellular automata. We call this modification the modified driving behaviour of Nagel-Schreckenberg.

![](img/55ff3770fcfe64effe3c90a4d4692fa6_215_0.png)

Fig. 3. Driving behaviour with agent

The overall rule of the modified driving behaviour of Nagel-Schreckenberg is as follows:

- **1. Acceleration**
  
  $$v_{(i,j)}(t-1)<v_{\max} \land g_{s(i,j)}(t-1)>v_{(i,j)}(t-1)+1$$
  
  $$v_{(i,j)}(t)\leftarrow v_{(i,j)}(t-1)+1 \tag{16}$$
- **2. Braking**
  
  $$g_{s(i,j)}(t-1)\leq v_{(i,j)}(t)\Rightarrow v_{(i,j)}(t)\leftarrow g_{s(i,j)}(t-1)-1 \tag{17}$$
- **3. Randomization**
  
  $$\xi(t)<p\Rightarrow v_{(i,j)}(t)\leftarrow \max[0,v_{(i,j)}(t)-1] \tag{18}$$
- **4. Vehicle movement**
  
  $$x_{(i,j)}(t)\leftarrow x_{(i,j)}(t-1)+v_{(i,j)}(t) \tag{19}$$
- **5. Lane changing**
  
  Determine probability of lane changing $P_{lc}$ and $a=[0:v]$ for:
  
  $$g_{s(i,j-1)}(t-1)<\sigma\land x_{(i,j-2)}(t-1)=0$$
  
  $$\Rightarrow x_{(i,j-2)}(t)\leftarrow x_{(i,j-1)}(t-1) \tag{20}$$
  
  or
  
  $$g_{s(i,j-2)}(t-1)<\sigma\land x_{(i,j-1)}(t-1)=0$$
  
  $$\Rightarrow x_{(i,j-1)}(t)\leftarrow x_{(i,j-2)}(t-1) \tag{21}$$
- **6. Car following/vehicle movement:** Back to step 4).
