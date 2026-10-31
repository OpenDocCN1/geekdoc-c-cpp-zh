Transition rules can have the same types of actions associated with them as regular inference agent rules. In addition, actions can be specified for execution when a state is entered and when the state is exited. One possible type of action is the starting or stopping of another state machine.

# Timeouts

States can have timeouts associated with them. The timer starts when the state is entered. If the timer expires before the state is exited, the specified actions are taken and the state machine transitions to a specified state.

Despite the fact that the state machine starts the timer, the timer itself is not part of the state machine. Each timer is an object that is, by default, operated in cache-only mode and saved to the backing store (if so configured).

One of the inference agents in the cluster (determined automatically) operates a scheduler. The scheduler periodically checks the timers to see which have expired and executes the state machine logic associated with the timeout. Note that this timeout event does not go through a preprocessor, yet locking may still be required to safely execute the logic. To support this, state machine timeout callbacks can be registered that perform the same role as a preprocessor function. When locking (or other preprocessor functionality) is required for the timeout event, you must define and register the necessary function. The _TIBCO BusinessEvents Data Modeling Developer’s Guide_ provides the details.

# Starting and Stopping State Machines

Each concept can have a main state machine associated with it. By default, this machine is configured to automatically start when the concept is created. By exception, the machine can be started using the catalog function `startStateMachine()`.

For more information on state machines, please consult the _TIBCO BusinessEvents Data Modeling Developer’s Guide_.