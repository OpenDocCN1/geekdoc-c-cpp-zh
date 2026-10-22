![](bbox=[0.22, 0.08, 0.82, 0.38])

# Figure 3.1 Mix Multiagent Model

+   - Internal Objects: data structures shared by all the processes that can be launched by the agent to carry out service requests or to achieve goals.
+   - Control: specification of how service requests are handled by the agent.

The network model defines two distinct agent types: network agents that offer network management services and application agents that offer their own services depending on their particular roles. The model is structured in three levels: interface, message and transport layer. The first one offers an API with both C++ and Java that supplies with communication facilities between agents by means of message passing. The second level services are offered to manage both addresses and the intentionality and body of the message. The transport level offers basic functionalities for sending and receiving messages over TCP/IP. The basic architecture is depicted in figure 3.1.

# 3.2.6 MAST: the Tool for Developing Multi-Agent Systems

MAST [30] is a toolbox for developing distributed processing information systems in an agent oriented fashion. It gives a mechanism to specify individual agents, with both offered and needed services and particular goals. It also incorporates agent group definition, tools for knowledge representation and exchange, and coordination mechanisms between agents.

# Defining Agents with MAST

ADL(Agent Definition Language) [43, pg. 39-47] is a declarative language integrated into MAST for defining the externals of an agent. Internals of agents shall depend on each particular implementation. Two agents which