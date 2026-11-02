
```cpp
input.insert(x2);
// Print the time and input
cout << "xx C" << sim->getTime() << "\t" <<
    x1.bit << " " << x2.bit << "\t\n";
// Advance the simulation
sim->computeNextState(input);
}
// Clean up and exit
delete sim; delete l; delete m;
return 0;
}
```

Now we must define input trajectories in terms of clock, rather than machine, cycles. When written in terms of ticks of the clock, the previous input $x_1[0, 10) = 1110011100$ becomes

$x'_1[0, 30) = 111\ 111\ 111\ 000\ 000\ 111\ 111\ 111\ 000\ 000$

and the input $x_2[0, 10)$ becomes

$x'_2[0, 30) = 000\ 000\ 000\ 000\ 000\ 000\ 000\ 000\ 000\ 000$

If we feed these trajectories into the new simulator, the output is

|  |  |  |  |  |  |  |
|---|---:|---:|---:|---|---:|---:|
| xx | C0 | 1 | 0 | yy | C0 | 0 |
| xx | C1 | 1 | 0 | yy | C1 | 0 |
| xx | C2 | 1 | 0 | yy | C2 | 1 |
| xx | C3 | 1 | 0 | yy | C3 | 1 |
| xx | C4 | 1 | 0 | yy | C4 | 1 |
| xx | C5 | 1 | 0 | yy | C5 | 0 |
| xx | C6 | 1 | 0 | yy | C6 | 0 |
| xx | C7 | 1 | 0 | yy | C7 | 0 |
| xx | C8 | 1 | 0 | yy | C8 | 1 |
| xx | C9 | 0 | 0 | yy | C9 | 1 |
| xx | C10 | 0 | 0 | yy | C10 | 1 |
| xx | C11 | 0 | 0 | yy | C11 | 1 |
| xx | C12 | 0 | 0 | yy | C12 | 1 |
| xx | C13 | 0 | 0 | yy | C13 | 1 |
| xx | C14 | 0 | 0 | yy | C14 | 1 |
| xx | C15 | 1 | 0 | yy | C15 | 1 |
| xx | C16 | 1 | 0 | yy | C16 | 1 |
| xx | C17 | 1 | 0 | yy | C17 | 0 |
| xx | C18 | 1 | 0 | yy | C18 | 0 |
| xx | C19 | 1 | 0 | yy | C19 | 0 |
| xx | C20 | 1 | 0 | yy | C20 | 1 |
| xx | C21 | 1 | 0 | yy | C21 | 1 |

xx C22 1 0      yy C22 1
xx C23 1 0      yy C23 0
xx C24 0 0      yy C24 0
xx C25 0 0      yy C25 0
xx C26 0 0      yy C26 0
xx C27 0 0      yy C27 0
xx C28 0 0      yy C28 0
xx C29 0 0      yy C29 0

This y (i.e., the value at every third line) and the y from the previous simulation are the same. Now, let us modify $x'_2$ so that its value changes in the middle of every machine cycle. This could simulate the improper operation of some component in the system, noise in the circuit, or some other undesirable condition. Keeping $x'[0, 30)$ the same, we change $x'_2[0, 30)$ into

$$x'_2[0, 30) = 010\ 010\ 010\ 010\ 010\ 010\ 010\ 010\ 010\ 010$$

and feeding this into the simulation produces

xx C0  1 0      yy C0  0
xx C1  1 1      yy C1  0
xx C2  1 0      yy C2  1
xx C3  1 1      yy C3  0
xx C4  1 0      yy C4  1
xx C5  1 1      yy C5  1
xx C6  1 0      yy C6  1
xx C7  1 1      yy C7  1
xx C8  1 0      yy C8  0
xx C9  0 1      yy C9  1
xx C10 0 0      yy C10 0
xx C11 0 1      yy C11 1
xx C12 0 0      yy C12 1
xx C13 0 1      yy C13 1
xx C14 0 0      yy C14 1
xx C15 1 1      yy C15 0
xx C16 1 0      yy C17 1
xx C17 1 1      yy C17 1
xx C18 1 0      yy C18 1
xx C19 1 1      yy C19 1
xx C20 1 0      yy C20 0
xx C21 1 1      yy C21 1
xx C22 1 0      yy C22 0
xx C23 1 1      yy C23 0
xx C24 0 0      yy C24 0
xx C25 0 1      yy C25 0
xx C26 0 0      yy C26 0
xx C27 0 1      yy C27 1

xx C28 0 0      yy C28 0
xx C29 0 1      yy C29 1

Looking at every third line, the corresponding output of the logical machine is y[0, 10) = 1101110001, which is clearly not what is expected from Equation 3.22 and the inputs x_1 and x_2 if they are obtained by looking at every third value in x′_1 and x′_2. Timing matters, a fact plainly demonstrated by our simulation.

The simulation engine built in this section simulates network models from the top, starting with the uppermost network, to the bottom, stopping at the atomic models. After a series of improvements, this top-down simulator would evolve into an implementation of Zeigler's abstract simulators [152, 157]. Top-down architectures, based on the abstract simulators, are widely used and are discussed and refined in a large body of literature (see, e.g., Refs. 26, 51, and 144). This architecture is particularly well suited to component-based simulations (see, e.g., Refs. 23, 24, 64, 127, and 148) and, more recently, Web-based simulations (see, e.g., Refs. 81 and 88).

### 3.3 A SIMULATOR FOR DISCRETE-TIME SYSTEMS

A simple and effective simulator can be built by focusing on the atomic models and relegating the network models to telling the simulator how atomic models are connected. The simulator devised in this section works from the bottom up. Network models are intermediate steps through which events pass as they travel between the atomic components; every operation begins and ends with an atomic model.

The basis for this approach has two parts:

- 1. The state transition function of the resultant of a network is defined by the state transition functions of the atomic components at the leaves of the tree rooted in that network. We can, therefore, skip the construction of resultants for the intermediate networks and work directly with the atomic models at the leaves.
- 2. The sets of influences can be used to compute the set of atomic components, which may be anywhere in the hierarchy of models, that are influenced by any particular atomic component. The calculation starts with an atomic model, ends with a set of atomic models, and is done recursively by employing the sets of influences and coupling functions of each network encountered along the way.

The set A_N of atomic models that are beneath a network model N is found by descending recursively into the network and adding to A_N all of the atomic models that are found. The set A_N is defined by

A_N = {d ∈ D_N | d is atomic} ∪_{N'∈D_N | N' is a network} A_{N'}    (3.32)

If $N$ is the network to be simulated, then $A_N$ is the set of atomic models that the simulator operates on. Assuming that the input $x_d^b$ that should be applied to each model $d \in A_N$ is known, we can compute the state transition function for the network with a simple for loop:

```
for $d \in A_N$ do
    $s_d \leftarrow \delta_d(s_d, x_d^b)$
end
```

The difficult step is to find $x_d^b$. This problem has three parts: (1) taking the output of $d \in A_N$ to the appropriate bags of input for the other models in $A_N$; (2) taking input to the network $N$ to the appropriate bags of input for the atomic models in $A_N$; and (3) taking the output of $d$ to the appropriate bags of output for the network models that are part of the tree rooted at $N$, a step that is required solely for the benefit of an EventListener that may need it.

Consider part 1 first: how, given an output from an atomic model $d$, to find the set of atomic models that $d$ influences and to insert the corresponding values into the bags of input for those models. We start with the models that have the same parent as $d$. The parent is denoted $PARENT(d)$. The atomic components of $PARENT(d)$ that $d$ influences directly are in $E_d$ (see Equation 3.30), and to the bag of input for each atomic model $d' \in E_d$ is added the value $z_{d,d'}(\lambda_d(s_d))$. This takes care of the atomic siblings of $d$. The other $d' \in E_N$ are networks belonging to $PARENT(d)$ or $d'$ is $PARENT(d)$ itself.

If $d'$ is a network belonging to $PARENT(d)$, then we proceed as follows. First we find the components of $d'$ that $d'$ influences; these models are in $D_{d'}$. Then, to the bag of input for each such atomic component $d''$, we add the value $z_{d',d''}(\lambda_{d'}(\lambda_d(s_d)))$. For the network components we simply repeat this procedure: finding the components in $d''$ that $d''$ influences, updating the bags of input for the atomic models, and again repeating this procedure for the network models.

Otherwise $d'$ is $PARENT(d)$ itself (i.e., the network itself). In this case, the preceding paragraph is applied to $PARENT(d')$ [unless, of course, $PARENT(d')$ is the root of the tree of models, in which case the output has left the system and we are done]. In other words, we find the set of components of $PARENT(d')$ that $d'$ influences and proceed as follows. To the bag of input for each such atomic component $d''$ we add the value $z_{d',d''}(\lambda_{d'}(s_{d'}))$. For the network components we repeat the procedure described in this paragraph or in the preceding paragraph as appropriate.

Algorithm 3.6 succinctly describes this recursive procedure. It begins with a model in $A_N$ and adds a value to the bag of input of every model in $A_N$ that can be reached from it. The route procedure is called with the atomic model $d$ that produced the output, the parent of the model $d$, and the output $y = \lambda_d(s_d)$. Associated with every atomic model $d' \in A_N$ (including, of course, $d$) is a bag $x_{d'}^b$ of input that is filled as the calculation proceeds. The coupling functions and sets of influences used by the procedure belong to the network referred to by the parent argument.
