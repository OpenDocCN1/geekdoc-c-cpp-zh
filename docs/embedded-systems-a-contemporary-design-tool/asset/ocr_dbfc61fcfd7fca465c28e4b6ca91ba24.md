![](bbox=[0.26, 0.08, 0.64, 0.36])

# ## 9.19.5.12 Kahn Process Network

The Kahn Process Network model is similar in structure to the Extended and Co-Design FSMs. The structure comprises a networked collection of processes. The processes, like finite automata, perform a mapping from input sequence to output sequence. The model supports distributed control and distributed memory.

The processes run autonomously and communicate via tokens through unbounded FIFOs. Like a CFSM, tokens can only be written or read once. Writes are nonblocking and Reads are blocking. Processes synchronize through a blocking Read operation. A process is either executing, following an Execute command, or communicating, following a Send or Get command, and the behavior is deterministic.

# ## 9.19.5.13 Control Flow – Data Flow – CDFG Graphs

Control and data flow graphs provide another means to express control and data flow in a system. We have explored them already under our discussion on structured design. The basic organization comprises control and data nodes. Control nodes interconnect to capture the expected control flow operations such as sequences, branches, concurrent operations, and loops. Each is linked to a data flow block.

The data flow block encapsulates a set of data computations. Each computation sequence is expressed as a directed acyclic graph. A data node expresses an arithmetic, logical, relational operation, or a read or write to or from memory or an external port.

# ## 9.20 CO-SYNTHESIS

Material based upon Mahapatra at Texas A&M Lavagno et al.

As we saw in an earlier diagram, partitioning, simulation, and synthesis work in concert. In addition, at the end of the day, they must implement the system that we are designing. We will now look at the synthesis component.