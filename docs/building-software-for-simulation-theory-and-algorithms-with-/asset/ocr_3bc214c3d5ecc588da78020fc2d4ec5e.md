transition function

$$\delta_{ex,m}(((p,\sigma),q),q) = (p+q-1,t_m)$$

ejects the completed part, stores the incoming parts, and begins operating on a new part.

The model of the assembly line has two copies of the machine model; the model of the press is denoted by the subscript $p$ and the drill, by $d$. The subscript $r$ is used for the resultant of the network, and its state is

$$s_r = (((p_p,\sigma_p),e_p),((p_d,\sigma_d),e_d))$$

The drill and press begin without parts in their bins. Their initial states are $(0, 2)$ and $(0, 1)$, respectively. The initial state of the resultant is $(((0, 1), 0), ((0, 2), 0))$, and its elapsed time $e_r$ is zero. For this experiment, the input to the assembly line is

$$x_I((0,0),(3,0)) = \begin{cases} 1 & \text{if } t=(0,0) \\ 2 & \text{if } t=(1,1) \\ \Phi & \text{otherwise} \end{cases}$$

The primitive decomposition of this trajectory has three parts: the empty trajectory $x_\Phi((0,0),(0,0))$, the first input trajectory $x_I((0,0),(1,1))$ with $x_I((0,0)) = 1$, and the second input trajectory $x_2((1,1),(3,0))$ with $x_2((1,1)) = 2$.

Case 5 of Equation 4.7 processes $x_\Phi$ without altering the state or elapsed time, and $x_1$ is processed next. Case 1 of Equation 4.7 changes the state of the system to

$$\delta_{ex,r}((((0,1),0),((0,2),0),0),1) = ((\delta_{ex,m}((0,1),0,1),0),((0,2),0)) \\ = (((1,1),0),((0,2),0))$$

and time advances to $(0, 1)$. The time advance of the assembly line is now

$$ta_r((((1,1),0),((0,2),0))) = \min[1,\infty] = 1$$

Case 4 of Equation 4.7 sets the elapsed time $e$ of the resultant to 1 and advances the trajectory to time $(1, 0)$. The elapsed time is equal to the time advance, but the output of the assembly line is

$$\lambda_r((((1,1),0),((0,2),0))) = \Phi$$