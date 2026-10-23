+   - The amount of data communicated via a GPRS network varies depending on the AMM readout frequency² and the used communication protocols, such as the DLMS/COSEM or the IEC61107 protocol.

These requirements are of great importance for the configuration process. The user should be able to add a large number of devices in the network and the device type is either already defined in the knowledge base or a new type can be additionally defined. The last two requirements limit the space of possible reconfigurations by means of constraints stated over the data amount transferred in the network.

Figure 19.1 illustrates a simplified cell from a smart grid,³ taking into consideration the GPRS data communication on the one side and the electric power transmission from the power generation station to smart meters on the other side (depicted in gray). Note that SIMOA simulation and (re) configuration focuses on GPRS data communication settings.

As depicted in Figure 19.1, IP-enabled meters (Point-to-Point (P2P) individually addressable smart meters), which are connected directly to the WAN (Wide Area Network) using GPRS, communicate with the AMM application, without requiring data concentrators⁴ in the field. The meters connected to data concentrators are called PLC (Power Line Carrier) meters. The usage of P2P meters becomes inevitable when the connection distance between a meter and a data concentrator is too large (more than 300 meters). In the simulation process we have to take into account the following variants of M2M terminals in a specific cell: (1) only P2P meters, (2) only data concentrators with PLC meters, and (3) both P2P meters and data concentrators with PLC meters.

In Figure 19.1, the Smart Grid (GPRS) cell comprises the following parts:

+   - Base Transceiver Station (BTS): Facilitates the wireless communication between user equipment (mobile phones, smart meters, etc.) and the network. The BTS has the equipment for encrypting and decrypting communications, spectrum filtering tools, antennas, and so on. Typically a BTS has several transceivers (TRXs) that allow it to serve several different frequencies and allocates a number of time slots for the M2M communication in the cell.

+   - P2P meters and Data Concentrators: These are described by configurable attributes that represent fixed or variable data amounts (derived from the chosen transfer protocols), network topology (determined by the distance between BTS and data concentrators/P2P meters), and in the case of data concentrators, the number of PCL meters connected to them.

+   - GPRS base load represented by the Mobile phone in Figure 19.1 and which represents all the non-smart-metering traffic in the cell.

It is worth noting that the structure of mobile phone networks varies and that communication requirements depend on the M2M application scenario. A typical AMM scenario is, for instance, the transfer

² The AMM readout frequency refers to the meter reading interval; i.e., for instance, an electricity meter can record the power consumption every 15 minutes.

³ A smart grid is a power transmission network, which makes use of supplier and consumer information and communication infrastructure to improve the overall network performance in terms of efficiency, reliability, and sustainability in an automated way.

⁴ A data concentrator is a device that is connected with several smart meters via a wire. In this case, all connected smart meters communicate to the AMM application over the data concentrator. Data concentrators are used, for example, in buildings with a large number of apartments where the costs for the additional wiring is low.