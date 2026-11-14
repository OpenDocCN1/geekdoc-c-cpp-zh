# ## 8.12.2.2 Reduced Capability

The next approach gives somewhat reduced capability under failure.

# ### 8.12.2.2.1 Lightweight Redundancy

As an alternative to full operational capability under failure, the design may support a critical subset of the output signals and add additional alarm capability. Such a scheme is called lightweight redundancy. A secondary system with alarm, annunciation, and some control capability accepts a subset of the inputs. The secondary system then calculates a subset of the outputs while monitoring the actions taken by the primary system. If a difference exists in the calculated output values and the primary outputs are out of bounds, a warning is issued.

The intent is to identify gross failures and to focus on fault detection rather than tolerance. The secondary system can provide a subset of critical functionality and outputs as necessary but cannot completely fill in for the main system in the event of failure. The block diagram for such a system appears in Figure 8.10.

![](bbox=[0.283, 0.385, 0.75, 0.545])

Figure 8.10 Lightweight Redundancy.

# ### 8.12.2.2.2 Monitor Only

An alternative to lightweight redundancy, with somewhat less capability, implements a primary system with a separate monitoring function. The monitoring subsystem does not support any of the primary functionality.

The primary system is charged with implementing the necessary actions while the monitor subsystem is responsible for keeping track of what actions need to be taken. The monitor channels also track the physical environment to ensure that the results of the actions are appropriate and correct. The sensing utilized by the monitor subsystem is separate from that of the primary system. The sensors for the primary system are strictly dedicated to that job, although a subset may be directed to the secondary subsystem.

The objective of such an approach is to have the monitor subsystem identify primary system failures and inform the appropriate fault-handling mechanisms. A failure in the monitor subsystem does not affect the primary system except indirectly, that is, the loss of monitoring capabilities and associated responses. Nonetheless, we must still identify and eliminate points of single failure. The two channels exchange messages to ensure proper and continuing operation of each. The block diagram is now refined as illustrated in Figure 8.11.