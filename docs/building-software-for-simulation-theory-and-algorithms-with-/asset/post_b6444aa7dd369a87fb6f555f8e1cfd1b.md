
model is defined by

$X_N$ = set of input to network  
$Y_N$ = set of output from network  
$D$ = set of components  
$I = \{I_d \mid d \in D \cup \{N\}\}$ family of sets of influencers  
$Z = \{z_{d,d'} \mid d' \in I_d \text{ and } d \in D \cup \{N\}\}$ set of coupling functions where  
$\quad z_{N,d}: X_N^b \to X_d^b$  
$\quad z_{d,N}: Y_d^b \to Y_N^b$  
$\quad z_{d',d}: Y_{d'}^b \to X_d^b$

Also recall that the sets $I_d$ of influencers define sets $E_d$ of influences (see Section 3.2.4), by

$E_d = \{d' \mid d \in I_{d'}\}$

and that this set is used in the construction of the simulator.

## 4.2.2 The Resultant of a Network Model

The resultant of a network of discrete event models is an atomic model whose set of states, transition functions, and output function are defined by its interconnected components. To simplify notation that would otherwise be very messy, the construction undertaken here assumes that all of the network's components are atomic models (this is the same approach taken by Zeigler [157]). Section 3.2.2 describes the recursive descent into the network that completes the reduction procedure.

The sets of input and output of the resultant are the sets $X_N$ and $Y_N$ of the network. The set $S_r$ of states of the resultant is the cross product of the sets of total states of its components so that

$S_r = \times_{d \in D} Q_d \qquad (4.12)$

and the time advance function $ta_r$ of the resultant is

$ta_r(s_r) = \min_{d \in D} ta_d(s_d) - e_d \qquad (4.13)$

which gives the least time remaining until the next autonomous action in the network.

The imminent components are those that will next undergo an autonomous event; they constitute the set

$$IMM = \{d \mid ta_d(s_d) - e_d = ta_r(s_r)\}$$ (4.14)

The subset $IMM \cap I_N$, which are attached to output of the network, contribute their output events to the network's output; its output function is

$$\lambda_r(s_r) = \cup_{d \in IMM \cap I_N} z_{d,N}(\lambda_d(s_d))$$ (4.15)

The transition functions of the resultant are more complicated. Before a new state is computed for a component, the inputs to it must be known. These are found in almost exactly the same way as in a discrete time network, but only the imminent models produce output. The set of components $IMM \cap (I_d - \{N\})$ provide input to $d$ at an internal or confluent transition of the resultant, and the input provided by these is

$$x_d^b = \cup_{d' \in IMM \cap (I_d - \{N\})} z_{d',d}(\lambda_{d'}(s_{d'}))$$ (4.16)

This bag of values does not include contributions from input to the network, but it does include all of the input to a component that originates with its siblings.

At an internal transition of the resultant, there is no input to the network. Therefore, Equation 4.16 is sufficient for calculating inputs to the components, and the internal transition function is defined by

$$\delta_{int,r}(s_r) = ((s'_1, e'_1), (s'_2, e'_2), \ldots, (s'_n, e'_n))$$ (4.17)

where

$$(s'_j, e'_j) = \begin{cases} (s_j, e_j + ta_j(s_j)) & \text{if } x_j^b = \emptyset \land j \notin IMM \\ (\delta_{int,j}(s_j), 0) & \text{if } x_j^b = \emptyset \land j \in IMM \\ (\delta_{ext,j}(s_j, e_j + ta_j(s_j), x_j^b), 0) & \text{if } x_j^b \neq \emptyset \land j \notin IMM \\ (\delta_{con,j}(s_j, x_j^b), 0) & \text{if } x_j^b \neq \emptyset \land j \in IMM \end{cases}$$

The internal transition function alters the state of the resultant by altering the states of its components, and for each component there are four possible outcomes. In the first case, no event occurs at the component and only its elapsed time is advanced. The other three cases change the state of the component according to its disposition: an internal event if it is imminent, an external event if it receives input, and a confluent event if both of these conditions apply.

At an external transition of the resultant there are no imminent models and only the input $x^b$ to the resultant can induce a change of state in its components. The external transition function of the resultant moves its input to the appropriate sets of components and changes their states with their external transition functions. All of the other components sit idly, merely having their elapsed time advanced. The external transition function is defined by

$$\delta_{ext,r}(s_r,e,x_r^b)=((s'_1,e'_1),(s'_2,e'_2),\ldots,(s'_n,e'_n)) \tag{4.18}$$

where

$$
(s'_j,e'_j)=
\begin{cases}
(s_j,e_j+e) & \text{if } N\notin I_j\lor Z_{N,j}(x_r^b)=\varnothing\\
(\delta_{ext,j}(s_j,e_j+e,Z_{N,j}(x_r^b)),0) & \text{otherwise}
\end{cases}
$$

The first case applies to a component that receives no input from the network, and the second case applies to all other components.

The confluent transition function is nearly identical to the internal transition function, but includes a special provision for components that are influenced by the network. For this purpose, the set of functions $\zeta_j(x^b)$ are defined, one for each component, to give its collective input received from its siblings, and the network. For each $j\in D$, $\zeta_j$ accepts a bag of input $x^b$ to the network and gives the bag of input to $j$ as

$$\zeta_j(x^b)=
\begin{cases}
x_j^b & \text{if } N\notin I_j\\
x_j^b\cup Z_{N,j}(x^b) & \text{if } N\in I_j
\end{cases} \tag{4.19}$$

The $x_j^b$ in this equation is defined by Equation 4.16. The definition of the confluent transition function is

$$\delta_{con,r}(s_r,x_r^b)=((s'_1,e'_1),(s'_2,e'_2),\ldots,(s'_n,e'_n)) \tag{4.20}$$

where

$$
(s'_j,e'_j)=
\begin{cases}
(s_j,e_j+ta_r(s_r)) & \text{if } \zeta_j(x_r^b)=\varnothing\land j\notin IMM\\
(\delta_{int,j}(s_j),0) & \text{if } \zeta_j(x_r^b)=\varnothing\land j\in IMM\\
(\delta_{ext,j}(s_j,e_j+ta_r(s_r),\zeta_j(x_r^b)),0) & \text{if } \zeta_j(x_r^b)\neq\varnothing\land j\notin IMM\\
(\delta_{con,j}(s_j,\zeta_j(x_r^b)),0) & \text{if } \zeta_j(x_r^b)\neq\varnothing\land j\in IMM
\end{cases}
$$

This is identical to Equation 4.17 except that the bag of input to each component contributes information from the network.

## 4.2.3 An Example of a Network Model and Its Resultant

This example consists of two machines for working metal. A press flattens small, metal balls into disks. It has a bin to hold balls that are waiting to be pressed. A drill

![](img/df6085a1b35edf9c9ea818a5c66ccad9_140_0.png)

puts a hole in the center of each disk, and it also has a bin to hold disks waiting to be drilled. The press flattens a ball in one second, but the drill needs two seconds to do its job. These machines are connected as shown in Figure 4.4. The algebraic description of this network is easily deduced from the diagram (see Section 3.2.1).

Input to and output from the network and its components are natural numbers that describe a quantity of parts: balls and disks with and without holes. Using the subscript $m$ to denote a machine model and $t_m$ the machining time, we can express the set of states of a machine as

$$S_m = \mathbb{N} \times R_0^\infty$$

where $(p, \sigma) \in S_m$ describes the number $p$ of parts for the machine to process and the time $\sigma$ remaining to process the first of those parts. The time advance is

$$ta_m((p, \sigma)) = \begin{cases} \sigma & \text{if } p > 0 \\ \infty & \text{otherwise} \end{cases}$$

and when this time expires, the internal transition function

$$\delta_{int,m}((p, \sigma)) = (p - 1, t_m)$$

removes the part from the machine and the output function

$$\lambda_m((p, \sigma)) = 1$$

makes the part available to the next machine in the assembly line. On receiving a number $q$ of parts, the external transition function

$$\delta_{ext,m}((p, \sigma), e, q) = \begin{cases} (p + q, \sigma - e) & \text{if } p > 0 \\ (p + q, t_m) & \text{if } p = 0 \end{cases}$$

places the parts into the bin and begins operating on one of them if the bin was empty. When new parts arrive and a part is completed simultaneously, the confluent transition function

$$\delta_{con,m}(((p,\sigma),q),q) = (p+q-1,t_m)$$

ejects the completed part, stores the incoming parts, and begins operating on a new part.

The model of the assembly line has two copies of the machine model; the model of the press is denoted by the subscript $p$ and the drill, by $d$. The subscript $r$ is used for the resultant of the network, and its state is

$$s_r = (((p_p,\sigma_p),e_p),((p_d,\sigma_d),e_d))$$

The drill and press begin without parts in their bins. Their initial states are $(0, 2)$ and $(0, 1)$, respectively. The initial state of the resultant is $(((0, 1), 0), ((0, 2), 0))$, and its elapsed time $e_r$ is zero. For this experiment, the input to the assembly line is

$$x_I((0,0),(3,0)) = \begin{cases} 1 & \text{if } t=(0,0) \\ 2 & \text{if } t=(1,1) \\ \Phi & \text{otherwise} \end{cases}$$

The primitive decomposition of this trajectory has three parts: the empty trajectory $x_\Phi((0,0),(0,0))$, the first input trajectory $x_I((0,0),(1,1))$ with $x_I((0,0)) = 1$, and the second input trajectory $x_2((1,1),(3,0))$ with $x_2((1,1)) = 2$.

Case 5 of Equation 4.7 processes $x_\Phi$ without altering the state or elapsed time, and $x_1$ is processed next. Case 1 of Equation 4.7 changes the state of the system to

$$\delta_{ext,r}((((0,1),0),((0,2),0),0),1) = ((\delta_{ext,m}((0,1),0,1),0),((0,2),0)) \\ = (((1,1),0),((0,2),0))$$

and time advances to $(0, 1)$. The time advance of the assembly line is now

$$ta_r((((1,1),0),((0,2),0))) = \min[1,\infty] = 1$$

Case 4 of Equation 4.7 sets the elapsed time $e$ of the resultant to 1 and advances the trajectory to time $(1, 0)$. The elapsed time is equal to the time advance, but the output of the assembly line is

$$\lambda_r((((1,1),0),((0,2),0))) = \Phi$$
