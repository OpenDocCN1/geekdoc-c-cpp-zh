![](bbox=[0.26, 0.08, 0.74, 0.26])

Figure 5.1 The UML Use Case Diagram

**Data Processor** The data is collected at very high speed from a number of measurement points; as a result, hardware co-processing capability is probably going to be necessary. That entity is included as a second actor and is labeled *Data Processor*. A possible use case diagram for the data acquisition system is given in Figure 5.2.

![](bbox=[0.26, 0.44, 0.74, 0.63])

Figure 5.2 Use Case Diagram for a Simple Data Acquisition System

# 5.4.1 Writing a Use Case

+   normal activity, exceptional conditions measure volts

The use case diagram captures a graphical representation of the public interface to the module or system. Associated with each use case is a textual description of what actions the actor is to perform and how the system is expected to respond. Such a description can be decomposed into two pieces: the normal activity of the use case and how exceptional conditions are to be handled.

Let's examine the *measure volts* use case for the data acquisition system. We specify how the user is to select the task, any options associated with the task, and how exceptions are handled as is done in Figure 5.3. Do not forget: a use case description is not intended to be *War and Peace*.