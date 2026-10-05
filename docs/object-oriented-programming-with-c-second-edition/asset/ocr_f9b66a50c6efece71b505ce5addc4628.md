# Functional Modelling

Activities or actions in the state diagrams of classes can be modeled as processes on the data flow diagram. Objects and attribute values of an object diagram can be modeled as flows on a data flow diagram.

Parameters of events from the dynamic model appear as input and output values of processes. The data flow diagram can be constructed by inserting processes between corresponding input and output values.

Processes in the top-level data flow diagram may be quite complex. Create a simplified and detailed lower-level data flow diagram for each process. If this level still contains complicated processes, repeat the process until you reach a data flow diagram with very simple processes.

Finally, write a textual description of each lowest-level process. The description emphasizes the objective of the process and not how the process would get implemented. Identify model actors and internal storage.

# D.4 System Design

System design is the high-level strategy for solving a problem and building a solution. The system is organized into sub-systems. Sub-systems are allocated to hardware and software components. Major conceptual and policy decisions that govern the detail for the design are also taken. The overall organization of the system is called the system architecture. During system design, overall high-level implementation decisions are made. This is followed by similar decisions for successively lower levels.

# Breaking the System into Sub-systems

A system is divided into sub-systems based on the similarity of services. A service is a set of functions that have a common objective.

Each sub-system provides a well-defined well-abstracted interface. The interface can be exchanged with the sub-system. It does not specify how the sub-system is implemented internally. Thus, the internal design of each sub-system can be created and modified while other sub-systems that interact with it remain unchanged.

# Layers

A system can be divided into sub-systems and these sub-systems can be horizontally layered on top of another. Each layer is built to provide services to the ones above it. Thus each layer provides the basis of designing the one above it. Layers are thus strongly coupled.

# Partitions

Sub-systems can be vertically placed next to each other as partitions (also see Figure D.20). Partitions are independent or weakly-coupled sub-systems.

A combination of layers and partitions can be used to divide a system.

We should also identify which activities may execute concurrently and which are mutually exclusive. The latter set of activities can be put together in a single thread of control.