
a site, you can implement a cluster that spans sites. A highly reliable WAN connection will be required. The publisher will be at a central site where most management operations are performed. Each site will have a subscriber server.

The topology you choose will depend on the WAN links, budget, and available administration staff.

**Exam Watch**

Remember that both the multi-site/centralized processing model and the WAN cluster model depend on highly reliable WAN links.

## CERTIFICATION SUMMARY

In this chapter, you learned about the Cisco Unified Communications Architecture and its various components. You began by reviewing the importance of the network infrastructure in a UC implementation. Next, you explored the functions provided by UC endpoints, including hardware and software IP phones. The call processing agents were covered next, and you learned about the differences between CME, CUCM, and the SBCS agents. Finally, you learned about voice mail and other UC features provided in a Cisco environment and the available topologies for VoIP network implementation.

## TWO-MINUTE DRILL

### 640-460: Describe the Components of the Cisco Unified Communications Architecture

- The UC network infrastructure includes the hardware and software used to transport the IP packets through the network to the destination.
- A VoIP network infrastructure must provide reliable delivery of voice packets and network redundancy for availability.
- Network redundancy can be achieved through the implementation of redundant routers.
- Power supply redundancy can be achieved through the use of a UPS system.
- UC endpoints are responsible for the creation of transmitted audio streams and the rendering of received audio streams.
- UC endpoints may be hardware devices, such as Cisco IP phones, or software solutions, such as the Cisco IP Softphone.
- CallManager Express (CME) runs on ISRs and is intended for smaller networks with up to 250 VoIP phones.
- Cisco Unified Communications Manager (CUCM) Business Edition is intended for medium organizations with up to 500 phones.
- CUCM is intended for large organizations with up to 30,000 phones per CUCM cluster.
- The UC500 series is intended for small businesses with from 8 to 48 IP phones.
- Cisco's Unity products provide messaging services for VoIP networks.
- Cisco Unity Express is intended for smaller organizations or branch offices.
- Cisco Unity Connection is intended for larger enterprises and SMBs.
- Cisco Unity is intended only for larger enterprises.
- Interactive voice response (IVR) systems play recorded messages to the caller and allow him or her to respond with keypad presses.
- Auto Attendant features allow callers to direct themselves to departments or extensions through direct-dial features.
- Contact centers include components to provide ACD, CTI, and collaboration features.
- Several topologies are available for VoIP network implementations with Cisco products, including single-site/centralized processing, multi-site/centralized processing, multi-site/distributed processing, and WAN clustering.
- The multi-site/centralized processing and WAN cluster topologies require highly reliable WAN links.

## SELF TEST

The following questions will help you measure your understanding of the material presented in this chapter. Read all the choices carefully because there might be more than one correct answer. Choose all correct answers for each question.

### 640-460: Describe the Components of the Cisco Unified Communications Architecture

- 1. You must implement a call processing agent that supports up to 15 phones. Which one of the following agents, implemented as a single device or server, will meet your needs without excessive costs?
    - A. CME
    - B. CUCM Business Edition
    - C. UC500
    - D. CUCM

- 2. You must implement a call processing agent that supports up to 4,300 phones. Which one of the following agents will meet your needs without excessive costs?
    - A. CME 4.2
    - B. UC500
    - C. CUCM
    - D. CME 4.3

- 3. What is the maximum number of phones supported by a UC500 series router running Cisco UC?
    - A. 8
    - B. 16
    - C. 32
    - D. 48

- 4. Which of the following are general categories of IP phones available from Cisco? (Choose two.)
    - A. Analog
    - B. Hardware
    - C. Software
    - D. Token Ring

- 5. What devices can be used to provide power supply redundancy for the infrastructure devices in a UC architecture?
    - A. UPS
    - B. CME
    - C. CUCM
    - D. Cisco Presence

- 6. What Cisco product provides the ability to have conference calls that simulate face-to-face meetings?
    - A. Cisco Unified Presence
    - B. Cisco Unity Express
    - C. Cisco TelePresence
    - D. CME

- 7. In what form factor does the Cisco Unity Express with flash come?
    - A. NM
    - B. AIM
    - C. MCS
    - D. PVDM

- 8. What Cisco Unity product is intended only for use within large organizations?
    - A. Cisco Unity
    - B. Cisco Unity Express
    - C. Cisco Unity Connection
    - D. Cisco Unity Enterprise

- 9. Which UC architecture topology demands highly reliable WAN links and always uses a CUCM publisher and subscribers?
    - A. Multi-site/distributed processing
    - B. Multi-site/centralized processing
    - C. WAN cluster
    - D. Single-site/centralized processing

- 10. Which UC architecture topology implements call processing agents at each site in a WAN environment, but does not depend on highly available WAN links?
    - A. Multi-site/distributed processing
    - B. Multi-site/centralized processing
    - C. WAN cluster
    - D. Single-site/centralized processing

- 11. What feature, within a Cisco UC environment, allows callers to direct themselves to an extension or a department?
    - A. Auto Attendant
    - B. Voice mail
    - C. TelePresence
    - D. Presence

- 12. What feature uses recorded messages to prompt the caller for keypad presses?
    - A. IVR
    - B. Auto Attendant
    - C. Presence
    - D. Mobility

- 13. What feature of a Cisco UC environment allows a user to indicate up to four different phones that may receive an incoming call targeted at a single extension or phone number?
    - A. IVR
    - B. Auto Attendant
    - C. Presence
    - D. Mobility

- 14. Which of the following are features typically provided by contact center management software? (Choose all that apply.)
    - A. ACD
    - B. IP routing
    - C. CTI
    - D. Presence

- 15. On what platform does the Cisco CME solution run?
    - A. Media Convergence Servers
    - B. Integrated Services Routers
    - C. Network Modules
    - D. Advanced Interface Modules

## LAB QUESTION

You are configuring a VoIP network and must provide redundancy in the routing infrastructure. Three network segments are to be connected. One segment is using the 10.1.0.0 network block. Another is using the 10.2.0.0 block. The final segment is using the 10.3.0.0 block. Each segment will have approximately 120 IP phones. To ensure redundancy between these networks (meaning that all networks have at least two routers through which they can connect to other networks), how many routers will you require? Explain why you have selected the number of routers specified in your answer.

## SELF TEST ANSWERS

### 640-460: Describe the Components of the Cisco Unified Communications Architecture

- 1. ☑ A is correct. The Cisco Communications Manager Express (CME) can support up to 250 phones, so it will incur the least cost to your organization while providing the needed support for the 15 phones required.

    ☒ B, C, and D are incorrect. CUCM Business Edition supports many more phones than required by the scenario and would incur unnecessary costs. The same is true for CUCM. The UC500 series device could support a maximum of 48 phones and would require three devices to meet the needs in the scenario. A single ISR running CME would be less expensive than three UC500 devices running separate VoIP networks.

- 2. ☑ C is correct. CUCM must be used in this scenario in order to accommodate the large number of phones (4,300) required.

    ☒ A, B, and D are incorrect. Regardless of costs, the CME in any version and the UC500 series devices cannot handle 4,300 phones, as required.

- 3. ☑ D is correct. While the UC500 series devices can support from 8 to 48 phones, the maximum is 48 phones.

    ☒ A, B, and C are incorrect. A UC500 series device can support 8, 16, or 32 phones; however, the maximum number supported is 48.

- 4. ☑ B and C are correct. Cisco offers both hardware- and software-based phones. The hardware-based phones look like traditional analog PBX phones, but work using VoIP protocols. The software-based phone is the Cisco IP SoftPhone, and it runs on a PC and requires a microphone and speakers for functionality.

    ☒ A and D are incorrect. Analog phones are not sold by Cisco; however, Cisco does offer gateways that can connect analog phones to VoIP networks. Token Ring phones are not offered by Cisco. Cisco’s IP phones are Ethernet based.

- 5. ☑ A is correct. An uninterruptible power supply (UPS) may be used to provide power redundancy for infrastructure equipment.

    ☒ B, C, and D are incorrect. The CME and CUCM software solutions require a powered machine to run. The Cisco Unified Presence (not simply Cisco Presence) feature is not a power-provisioning feature.
