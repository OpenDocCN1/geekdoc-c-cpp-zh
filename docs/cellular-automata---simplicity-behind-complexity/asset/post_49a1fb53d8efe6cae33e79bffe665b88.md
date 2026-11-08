
![](img/55ff3770fcfe64effe3c90a4d4692fa6_220_0.png)

Fig. 7. The roadway where the traffic survey was conducted

Back to the speed of the trucks/trailers, we show their speeds compared by the speed of all kind of the cars by time to time consecutively in 190 hours (eight days). We find that on the same measurement time, speeds of the trucks/trailers dominantly are lower than that of speed all kind of the cars (see in Fig. 10), number of lower speeds for the truck/trailer is around 81%.

| Speed Interval | Truck | All | Speed Interval | Truck | All |
|---|---:|---:|---|---:|---:|
| 1-5 | 13 | 11 | 36-40 | 52 | 43 |
| 6-10 | 2 | 4 | 41-45 | 35 | 51 |
| 11-15 | 1 | 1 | 46-50 | 2 | 20 |
| 16-20 | 3 | 2 | 51-55 | 0 | 0 |
| 21-25 | 19 | 10 | 56-60 | 0 | 0 |
| 26-30 | 27 | 24 | 61-65 | 0 | 0 |
| 31-35 | 36 | 24 | 66-70 | 0 | 0 |
|  |  |  | Total | 190 | 190 |

Table 2. Distribution of speed for the truck/trailer and all kind of the cars

![](img/55ff3770fcfe64effe3c90a4d4692fa6_221_0.png)

Fig. 8. Distribution of speed for the truck/trailer and all kind of cars

| Speed Interval | Bus | Public | Private | All | Speed Interval | Bus | Public | Private | All |
|---|---:|---:|---:|---:|---|---:|---:|---:|---:|
| 1-5 | 11 | 11 | 12 | 11 | 36-40 | 51 | 40 | 30 | 43 |
| 6-10 | 4 | 4 | 3 | 4 | 41-45 | 37 | 39 | 36 | 51 |
| 11-15 | 2 | 1 | 1 | 1 | 46-50 | 24 | 27 | 31 | 20 |
| 16-20 | 3 | 1 | 2 | 2 | 51-55 | 1 | 3 | 21 | 0 |
| 21-25 | 4 | 7 | 11 | 10 | 56-60 | 0 | 1 | 3 | 0 |
| 26-30 | 28 | 25 | 20 | 24 | 61-65 | 0 | 0 | 0 | 0 |
| 31-35 | 24 | 31 | 19 | 24 | 66-70 | 1 | 0 | 1 | 0 |
|  |  |  |  |  | Total | 190 | 190 | 190 | 190 |

Table 3. Distributions of speed for the bus; public transport; private car; and all kind of the cars

![](img/55ff3770fcfe64effe3c90a4d4692fa6_221_1.png)

Fig. 9. Distributions of speed for the bus; public transport; private car; and all kind of the cars

model. The number of diligent driver is probabilistically determined, while the agent driver is determined by integer. Both diligent driver and agent driver are reflected by the addition of speed in the car-following model. A diligent driver has the additional speed $c'=[0:\min(\bar{v},v)]$ while an agent has $c=[0:\max(v)]$. We know that velocity $v$ of each car is given by the function of the headway to the vehicle in front. By adding the additional speed to the diligent driver and agent driver then we have the velocity $v$,

$$v=\begin{cases}v_{(i,j)}'(t)=v_{(i,j)}(t)+[0:\min(\bar{v},v)] & \text{for diligent driver}\\v_{(i,j)}'(t)=v_{(i,j)}(t)+[0:\max(v)] & \text{for agent driver}\end{cases} \tag{31}$$

By referring (Maerivoet, S. & De Moor, B., 2005 B), we make the implementation of lane-changing model in the modified car-following NaSch model. Implicitly, we have used it in the section 4.2.4.1. There are two sub-steps on the lane-changing section that is consecutively executed at each time step. First, the lane-changing model is executed, exchanging vehicles between laterally adjacent lanes; second, all vehicles are moved forward by applying the modified car-following part of the NaSch model’s rules. We make the steps of lane-changing as follows:

- 1. Lane-changing model

For two lanes of traffic, we proposed as follows:
Determine probability of lane changing $P_{lc}$ and $a=[0:v]$ for

$$g_{s_{(i-1,j)}}(t-1)>\alpha\land\lambda_{(i,j-2,j)}(t-1)=0\\\Rightarrow x_{(i,j-2,j)}(t)\leftarrow x_{(i-1,j)}(t-1) \tag{32}$$

and

$$g_{s_{(i-2,j)}}(t-1)>\alpha\land\lambda_{(i+1,j)}(t-1)=0\\\Rightarrow x_{(i,j+1)}(t)\leftarrow x_{(i,j)}(t-1) \tag{33}$$

The rules in Equation (32) and Equation (33) describe that if in a lane, the driver is not possible to move his car forward (there is car ahead) and he sees that there is any safety space in another lane with the number of space is up to the speed v then he changes the lane. If the car was already stayed in the new lane, then he has the speed less than or equal to the current speed $v$. It implies any deceleration experienced by the car when moving to the other lane by probability $P_{lc}$. Adjustment the number of probability $P_{lc}$ obtains how many cars will change their lane when the condition is fulfilled.

- 2. Vehicle movement

For a diligent driver, his vehicle movement is:

$$x_{(i,j)}(t)\leftarrow x_{(i,j)}(t-1)+v_{(i,j)}(t)+[0:\min(\bar{v},v)] \tag{34}$$

with $g_s(t-1)>v(t-1)$.

While an agent driver:

$$x_{(i,j)}(t) \leftarrow x_{(i,j)}(t-1) + v_{(i,j)}(t) + [0 : \max(v)] \tag{35}$$

with $g_s(t-1) > v(t-1)$.

The rule of vehicle movement in the NaSch model is stated in the Equation (14). In this model the current position of the car x(t) is influenced by the previous position x(t-1) and the current speed v(t). By reflection on the evacuation of vehicle on the suffered road (Sidoarjo Porong roadway), we propose diligent driver into the car-following. He has the speed shown in Equation (31). Besides he has the current speed v(t), he also has the additional speed between zero to min(v̄, v) because diligent driver arranges his speed on the temporal average speed. Thus vehicle movement in the modified car-following NaSch model for a diligent driver has equation that is shown in Equation (34), the current position of the car x(t) is not only influenced by the previous position x(t-1) and the current speed v(t) but also influenced by the diligent driver's additional speed. On the other hand, an agent driver in this study has the speed also expressed in Equation (31), he has the additional speed between zero to max(v) because agent driver arranges his speed to the maximum speed when the condition is available. Vehicle movement in the modified car-following NaSch model for an agent driver has equation that is expressed in Equation (35), the current position of the car x(t) is influenced by the previous position x(t-1), the current speed v(t), and the agent driver's additional speed.

Lane changing causes the position of that car move forward in the new lane so that there is difference between the prior positions of the car (there is no moving forward in last lane) and the current position (moving forward by his speed in the new lane). This event provides the time of the car is faster to arrive in any safety areas. The accumulation of lane-changing will support to the effectiveness of vehicle evacuation. Vehicle movement for diligent driver and agent driver also has the important role to find the effectiveness of vehicle evacuation, especially on the suffered road, Sidoarjo Porong roadway.

A modified car-following NaSch model considering agent driver and diligent driver is presented as follows:

- 1. Acceleration:

$$v_{(i,j)}(t-1) < v_{max} \land gs(i,j)(t-1) > v_{(i,j)}(t-1)+1 \quad \Rightarrow \quad v_{(i,j)}(t) \leftarrow v_{(i,j)}(t-1)+1 \tag{36}$$

- 2. Braking:

$$gs_{(i,j)}(t-1) \le v_{(i,j)}(t) \Rightarrow v_{(i,j)}(t) \leftarrow gs_{(i,j)}(t-1)-1 \tag{37}$$

- 3. Randomization:

$$\xi(t) < p \Rightarrow v_{(i,j)}(t) \leftarrow \max[0, v_{(i,j)}(t)-1] \tag{38}$$

- 4. Vehicle movement: If a diligent driver,

$$x_{(i,j)}(t) = x_{(i,j)}(t-1) + v_{(i,j)}(t) + [0 : \min(\bar{v}, v)] \tag{39}$$

Else if an agent driver,

$$x_{(i,j)}(t) = x_{(i,j)}(t-1) + v_{(i,j)}(t) + [0 : \max(v)] \tag{40}$$

- 5. **Lane-changing:**

Determine probability of lane changing $P_{lc}$ and $a=\{0:v\}$ for:

$$g_{s(i-1,j)}(t-1) > \alpha \land \lambda_{(i,j+?)}(t-1)=0$$
$$\Rightarrow x_{(i,j-2,j+?)}(t) \leftarrow x_{(i-1,j)}(t-1)$$

or

$$g_{s(i-2,j)}(t-1) > \alpha \land \lambda_{(i-1,j+?)}(t-1)=0$$
$$\Rightarrow x_{(i,j+?)}(t) \leftarrow x_{(i-2,j)}(t-1)$$

- 6. **Car-following/ vehicle movement:** back to step 4.

## 6.1 Experimental simulation results

The computational simulation of modified car-following NaSch model is carried out and compared with the results of the NaSch model in the case of evacuation. We observe the evacuation time with respect to the diligent driver and also the agent driver. The maximum speed is set to $v_{max}=5$ and the system size is $L=200$.

### 6.1.1 Fundamental diagram and spatio-temporal structures

Fig. 11 shows the fundamental diagram of modified car-following NaSch model. When the density $k$ is lower than the critical density, the flow rate increases with $k$ and the traffic flow is free. When $k$ is larger than the critical density, the flow rate decreases as $k$ increases and the traffic flow is congested. This situation is in accordance with the traffic flow stated by (Immers, L.H. & Logghe, S., 2002); (Maerivoet, S. & De Moor, B., 2005 A); (Maerivoet, S. & De Moor, B., 2005 B) and (Tampère, C.M.J., 2004). In those references also state that at saturated roads (large density), the flow rate $q$ is saturated (the vehicles are queuing). The condition is different with fundamental diagram resulted by modified car-following NaSch model (Fig. 11). When density is large, saturation of flow rate $q$ does not happen, it is caused by the role of diligent driver and agent driver.

![](img/55ff3770fcfe64effe3c90a4d4692fa6_225_0.png)

Fig. 11. Fundamental diagram of modified car-following NaSch model

Fig. 12 compares the spatio-temporal structures of the NaSch model and the modified car-following NaSch model. One can see that the evacuation time of the modified car-following
