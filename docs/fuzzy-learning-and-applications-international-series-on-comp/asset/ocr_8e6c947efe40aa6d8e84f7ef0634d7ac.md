M(γ^c) = 1 ∀γ^c ∈ Γ^c (8.17)

M(γ*) ≥ [α · μ(γ*)] ∀γ* ∈ Γ* (8.18)

where [l] is defined as the smallest integer number greater or equal than the real number l and where α is the FMS performance index required [31] [34]. As can be seen, condition (8.17) fixes the number of tokens in each command circuit equal to 1. Condition (8.18) fixes a lower bound for the number of tokens in each elementary circuit, which is not a command circuit.

Finding a solution to such a problem usually involves the solution of an integer linear problem where at least as many constraints as the elementary circuits in the Event Graph have to be considered. Actually, this represents a major drawback of such an approach, since it requires the explicit enumeration of all such circuits. In [27–29] one of the authors presented an alternative to these algorithms, based on use of a Hopfield neural network. In the following the neural solution will be clearly described.

# FMS Performance Optimization: Solution by the Hopfield Network

The solution of the FMS performance optimization problem, by the Hopfield neural model, may be achieved by the following steps:

Step1: Modelling the FMS by Event Graphs. The FMS is first modelled by means of Event Graphs. As said previously, modelling an FMS by Event Graphs is very easy and consists of representing each FMS resource (buffer, machine, robot, etc.) by a place and each activity performed by a resource by a transition, to which the time required to complete the activity is associated.

Step 2: Mapping the Event Graph onto the Neural Model. Once the FMS has been modelled by the Event Graph, it is transformed into a Hopfield neural model. This is achieved by making each place, P_i, in the Event Graph correspond to the neuron, O_i, in the neural network. The value (1 or 0) of the output of each neuron O_i models the presence or absence of a token in the place P_i modelled: if the output O_i is 1 the place P_i corresponding to the neuron contains a token, if O_i is 0 the place P_i contains no tokens. It is clear that the proposed coding of the neural output is based on the necessary assumption that each place in the Event Graph contains at most one token. This does not represent a limit, as it is demonstrated in [34] that it is always possible to modify a generic Event Graph into an equivalent one in which each place possesses at most one token. The mapping between the Event Graph modelling the FMS