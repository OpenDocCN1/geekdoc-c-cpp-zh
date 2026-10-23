
networks and especially over mobile GPRS/UMTS networks. Originally, communication infrastructures were not designed to fulfill the requirements of the mentioned M2M communication scenarios.

The Kapsch Smart Energy Management System for metering and building automation offers a future-proof, open, and manufacturer-independent solution, which fits the needs of all the groups involved: from end consumers, building owners, and facility managers to network operators and energy suppliers. In this context, functionalities that support a detailed analysis of alternative smart metering scenarios are highly requested. In order to support such functionalities, simulations of various parts of a mobile network such as cell, backbone, and data storage have to be conducted. The major purpose of such a simulation is to check whether a network configuration can support a set of given user requirements. In order to simulate the dynamics of a mobile network, we treat each part of the mobile network, which is to be simulated, as a state machine with a predefined number of states. For example, in one particular state a component might be active whereas in another one this is not the case. Another example is a network configuration that may change from state to state in order to handle different communication requirements.

If a simulation fails (the requirements cannot be fulfilled by the mobile network), a working reconfiguration of the given system has to be delivered. In particular, adding too many M2M devices to a cell configuration might lead to an unacceptable reduction of service availability, which can only be handled by changing the default value of the parameters in the cell (for instance, by increasing the number of serving frequencies) or by extending the communication network via adding new mobile phone cells.¹ A cell configuration contains one base station, a number of metering devices, and a base load value.

The major contributions of the chapter are the following: (1) we provide important insights into the principles of knowledge-based reconfiguration in the domain of M2M communication networks, and (2) we discuss major business cases that are related to the application of (re) configuration technologies in the context of mobile phone networks and M2M applications.

The remainder of this chapter is organized as follows. In Section 19.2 we discuss in more detail the major requirements regarding the support of M2M communication scenarios. Afterward, we introduce an application scenario and give an overview of the SIMOA approach (Section 19.3). In Section 19.4 we discuss relevant business cases that are related to the application of SIMOA technologies. With Section 19.5 we conclude this chapter.

## 19.2 Domain Requirements

Unlike today’s mobile networks, the future GPRS (General Packet Radio Service) networks used in Automatic Meter Management (AMM) communication have to support the following requirements:

- The GPRS networks have to be highly reliable and extensible.
- There must be a large IP address pool available.
- There is a required data amount specified for AMM communication.

¹ When adding a new mobile phone cell to a network, in fact, a new base station is added to the system and the transfer data is redistributed to the cells.

- The amount of data communicated via a GPRS network varies depending on the AMM readout frequency² and the used communication protocols, such as the DLMS/COSEM or the IEC61107 protocol.

These requirements are of great importance for the configuration process. The user should be able to add a large number of devices in the network and the device type is either already defined in the knowledge base or a new type can be additionally defined. The last two requirements limit the space of possible reconfigurations by means of constraints stated over the data amount transferred in the network.

Figure 19.1 illustrates a simplified cell from a smart grid,³ taking into consideration the GPRS data communication on the one side and the electric power transmission from the power generation station to smart meters on the other side (depicted in gray). Note that SIMOA simulation and (re) configuration focuses on GPRS data communication settings.

As depicted in Figure 19.1, IP-enabled meters (Point-to-Point (P2P) individually addressable smart meters), which are connected directly to the WAN (Wide Area Network) using GPRS, communicate with the AMM application, without requiring data concentrators⁴ in the field. The meters connected to data concentrators are called PLC (Power Line Carrier) meters. The usage of P2P meters becomes inevitable when the connection distance between a meter and a data concentrator is too large (more than 300 meters). In the simulation process we have to take into account the following variants of M2M terminals in a specific cell: (1) only P2P meters, (2) only data concentrators with PLC meters, and (3) both P2P meters and data concentrators with PLC meters.

In Figure 19.1, the Smart Grid (GPRS) cell comprises the following parts:

- Base Transceiver Station (BTS): Facilitates the wireless communication between user equipment (mobile phones, smart meters, etc.) and the network. The BTS has the equipment for encrypting and decrypting communications, spectrum filtering tools, antennas, and so on. Typically a BTS has several transceivers (TRXs) that allow it to serve several different frequencies and allocates a number of time slots for the M2M communication in the cell.

- P2P meters and Data Concentrators: These are described by configurable attributes that represent fixed or variable data amounts (derived from the chosen transfer protocols), network topology (determined by the distance between BTS and data concentrators/P2P meters), and in the case of data concentrators, the number of PCL meters connected to them.

- GPRS base load represented by the Mobile phone in Figure 19.1 and which represents all the non-smart-metering traffic in the cell.

It is worth noting that the structure of mobile phone networks varies and that communication requirements depend on the M2M application scenario. A typical AMM scenario is, for instance, the transfer

² The AMM readout frequency refers to the meter reading interval; i.e., for instance, an electricity meter can record the power consumption every 15 minutes.

³ A smart grid is a power transmission network, which makes use of supplier and consumer information and communication infrastructure to improve the overall network performance in terms of efficiency, reliability, and sustainability in an automated way.

⁴ A data concentrator is a device that is connected with several smart meters via a wire. In this case, all connected smart meters communicate to the AMM application over the data concentrator. Data concentrators are used, for example, in buildings with a large number of apartments where the costs for the additional wiring is low.

Hence, a solution for showing that a communication network fulfills the requirements of M2M application scenarios and taking counter measures in case of detected shortcomings has to be flexible and adaptable.

## 19.3 SIMOA Approach

From the application domain we are able to derive the requirements for a tool that provides change operations for the given mobile network taking into account future usage scenarios. The future usage scenarios are determined by the communication needs of M2M applications (see, for example, the two scenarios discussed in the previous section). In the following, we discuss tool requirements with regard to the knowledge representation language, simulation features, reconfiguration, and optimization functionalities.

- *Language.* In order to support the discussed scenarios, we need information about the structure and behavior of mobile networks and related usage scenarios. Due to the huge variety of networks and usage scenarios, a modeling language has to be provided for formalizing the information. This language has to allow for stating the structure of a system and the behavior of its components. Temporal aspects, such as changes in network access over time, have to be captured as well. Moreover, in case of optimization requirements, the language has to provide means for stating optimality criteria.
- *Simulation.* The first step to evaluate whether an available mobile network is capable of handling all requests imposed by a future M2M application is to simulate the network behavior using the M2M communication requirements. Example requirements might be maximum delays of replies of remote machines on messages sent or the required amount of data to be sent at the same time. If the simulation returns that the network cannot handle certain requirements of the M2M application, someone is interested in finding a reconfiguration of the network that allows for fulfilling the requirements. The simulation itself should be based on the introduced modeling language. In the area of dynamic systems modeling and simulation, we mention Matlab/Simulink and Modelica. Although both of them are complex languages, capable of modeling a great variety of components, they are less appropriate for (re) configuration purposes, because they cannot handle underconstrained problems where a variety of solutions is possible.
- *Reconfiguration.* Changing an existing network for fulfilling communication scenarios imposed by M2M applications can be done on several levels. Certain parameters of mobile phone cells can be changed in order to provide more channels. New cells can be added to the network, thus changing the network topology. In our application all such possible changes should be reported. The same modeling language that is used for simulation should also be used for providing configuration information.
- *Optimization.* Since there is very likely more than one reconfiguration for handling future communication requirements, an optimal solution would be of great interest. Depending on who the user is, different optimality criteria are to be fulfilled. For instance, a mobile operator would prefer the reconfiguration that offers the best quality of service, whereas a customer would pick the solution with least costs for communication. Therefore, a requirement is that various optimality criteria can be specified and that it is possible to search for reconfigurations fulfilling the optimality criteria.
