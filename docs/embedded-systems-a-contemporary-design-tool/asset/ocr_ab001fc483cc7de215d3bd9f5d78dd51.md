![](bbox=[0.26, 0.08, 0.73, 0.34])

# ### 9.19.5.7.1 LIMITATIONS

The model is at too low a level to easily support specification. Generally, formal specification languages such as Esterel, SystemC, VHDL, Verilog, or State Charts are more effective.

# ### 9.19.5.8 Co-Design FSM

The second such model is called the _Co-Design FSM_. Its design is intended to address issues with the synchronous model underlying concurrent FSMs. Such a model implies that all comprising state machines must change state at same time. However, software implemented in a single processor environment requires interleaving actions in time; we cannot have parallel activity. The Co-Design FSM addresses issues of timing and coordination.

Similar to the EFSM, the CFSM model is expressed as a network of FSMs with a communication mechanism that is used to orchestrate the operation of the model. State changes in the comprising FSMs are asynchronous with respect to each other. Thus, the system is globally asynchronous. The time to compute a next state change can be different in each machine and can be unbound in the limit if the implementation is not known.

The communication mechanism between machines is based upon timed events rather than simple integers like the EFSM. An event is defined by the triple given in Eq. (9.6):

Event = {N, V, T} (9.6): N – The name of the event. V – The value T – A positive integer denoting the _time_ of occurrence

Event transfer uses an unacknowledged protocol: the receiver does not acknowledge receipt of the event. Two kinds of events defined:

+   * **trigger** • Trigger events that provide the basic synchronization mechanism in a CFSM. They are used one time, which is called a destructive read, and cause a state transition in the target machine.

+   * **pure value** • Pure Value events that cannot cause a state change directly but can be used to select from alternate possibilities involving the same set of trigger events.