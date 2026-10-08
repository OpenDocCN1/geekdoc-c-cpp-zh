
# Exam Preparation Tasks

## Review All the Key Topics

Review the most important topics in the chapter, noted with the key topics icon in the outer margin of the page. Table 9-4 describes these key topics and identifies the page number on which each is found.

Table 9-4 Key Topics for Chapter 9

| Key Topic Element | Description | Page Number |
| --- | --- | --- |
| Topic | IP Phone registration process | 240 |
| Topic | IP Phone configuration requirements in CUCM | 244 |
| Topic | End Users versus Application Users | 254 |
| Topic | LDAP Integration | 258 |

This chapter includes the following topics:

- Call Flows in CUCM: This section describes how signaling and audio traffic flow in a CUCM system.
- CAC and AAR: This section explains CAC and the use of AAR.
- Call-Routing Components: This section discusses the sources, destinations, and interaction of the various call-routing components in CUCM.
- Class of Control: This section discusses the capabilities and configuration of Class of Control elements in CUCM.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_297_0.png)

# Understanding CUCM Dial-Plan Elements and Interactions

Chapter 9, “Managing Endpoints and End Users in CUCM,” discussed the administration of IP Telephony endpoints and in Cisco Unified Communications Manager (CUCM). This chapter reviews the components, behaviors, and interactions of the CUCM dial-plan.

## ## Do I Know This Already? Quiz

The “Do I Know This Already?” quiz allows you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation Tasks” section for review. If you are in doubt, read the entire chapter. Table 10-1 outlines the major headings in this chapter and the corresponding “Do I Know This Already?” quiz questions. You can find the answers in Appendix A, “Answers Appendix.”

10-1 Understanding CUCM Dial-Plan Components
| Foundation Topics Section | Questions Covered in This Section |
| --- | --- |
| CUCM Call Flows | 1–3, 6–9 |
| CAC and AAR | 4–5 |
| Class of Control | 10–12 |

- 1. Which two of the following are reasons to eliminate IP phone reliance on DNS?
   a. Elimination of additional licenses for Cisco Unified DNS Server
   b. Elimination of single point of failure
   c. Reduce delay caused by name resolution lookups
   d. Eliminate delays caused by ARP resolution
- 2. Which of the following is true regarding call flows in CUCM? (Choose two.)
   a. Signaling traffic using RTP is sent directly to the CUCM from the IP phone.
   b. Signaling traffic using SCCP/SIP is sent directly to the CUCM from the IP phone.
   c. Voice bearer stream traffic flows through the CUCM server to maintain QoS priority.
   d. Voice bearer stream traffic flows direct from phone to phone.

# 3. Which of the following is true of SRST?

   a. SRST allows IP phones in a branch to be controlled by the local router in the event that WAN failure causes a loss of connectivity to the CUCM.
   b. SRST performs dynamic gateway services, allowing keepalives and signaling to be sent over the backup PSTN link.
   c. The NM-SRST module is supported on the 2900 and 3900 series ISR platforms only.
   d. SRST is a legacy feature; the replacement feature set is called Service Advertisement Framework.

# 4. Call Admission control serves what purpose?

   a. Limiting user access to toll calls (for example, preventing unauthorized long-distance calling).
   b. Throttling the number of concurrent call attempts to prevent Code Yellow events.
   c. Rerouting calls received from the PSTN in the event of WAN failure.
   d. Tracing malicious calls received from the PSTN to verify their origin.
   e. Preventing oversubscription of IP WAN bandwidth by dropping calls that exceed the configured voice queue size.

# 5. Which of the following is the only event that will trigger AAR?

   a. WAN failure
   b. CFUR rejection
   c. SRST registration
   d. Local Route Group failure
   e. CAC call rejection
   f. International Talk Like a Pirate Day

# 6. Which of the following is the correct order of configuration of call-routing components?

   a. Device, Route Group, Route List, Route Pattern
   b. Route Pattern, Route List, Route Group, Device
   c. Route Pattern, Route Group, Route List, Device
   d. Route Group, Device, Route Pattern, Route List

# 7. Which of the following Route Patterns is the closest match for the dialed number 98675308?

   a. 9.1[2-9]XXXXXX
   b. 9.[2-9]XXXXXX
   c. 9.@
   d. 9.8[6|7][6|7]XXXX
   e. 9.8XXXXXX
   f. 9.86[|0123456789]5308

# 8. Which two of the following signaling methods provide digit-by-digit analysis? (Choose two.)

   a. SIP en-bloc
   b. MGCP en-bloc
   c. SIP using rules
   d. CUCM using rules
   e. SCCP
   f. SIP

9. Which of the following are call-routing algorithms?

   a. First-in, First-out
   b. Broadcast
   c. Directed
   d. Longest
   e. Circular

10. Which of the following is true?

   a. No partitions exist by default.
   b. One partition exists by default.
   c. Only the default has access.
   d. All CSSs have access to the default.

11. Which statement is correct regarding Search Spaces?

   a. If CSS is applied to the phone, it overrides the line.
   b. If CSS is applied to the line, it invalidates the phone.
   c. If CSS is applied to the phone, it is the configuration.
   d. If CSS is applied to the line, it cannot be used.

12. What happens when DNS is not used?

   a. 2112 rings.
   b. The caller gets an error message.
   c. The attendant answers.
   d. None of the above correct.

# Foundation Topics

## CUCM Call Flows

Chapter 6, "Understanding CME Dial-Plan," discussed how Unified Communications Manager Express (CME) selects call-routing targets. The dial-plan in Cisco Unified Communications Manager (CUCM) is more complex because it uses remote components as gateways to route calls. CUCM is intended to scale to large-enterprise environments, and consequently has greater call-routing complexity and redundancy. This chapter introduces and discusses signaling and voice traffic flow in different scenarios, the components of the call-routing system, redundancy, and restriction.

## Call Flow in CUCM if DNS Is Used

Generally speaking, Domain Name System (DNS) is not recommended for use with IP phones. If DNS is used, the phones must complete a DNS lookup to learn the IP address of the CUCM server before any signaling can occur. At best, doing so introduces delays; at worst, it allows the possibility of a misconfiguration or failure of the DNS system that could cause the phones to stop working.
When the DNS lookup has completed successfully, the call flow consists of signaling (either SCCP or SIP) between the phone and the CUCM, and the voice bearer streams (using Real-Time Transport Protocol (RTP)) between the phones. Note that the phones do not signal each other, nor does any voice traffic flow through the CUCM. Figure 10-1 illustrates call flow when DNS is used by the phones.

> Note: The exception to the last statement is if the CUCM is hosting a voice conference; in that case, the voice streams from all conference participants flow into the CUCM and the combined streams (minus the listener's own stream) flow out of the CUCM back to the participants.

## Call Flow in CUCM if DNS Is Not Used

Eliminating IP phone reliance on DNS is recommended to eliminate unnecessary delay and potential points of failure. If DNS is not used, the call flow is simple, except that the initial DNS lookup is eliminated, there remains only the signaling flow between the phones and the CUCM, and the voice bearer streams directly between the phones. Figure 10-2 illustrates call flow without DNS in by.

The elimination of DNS reliance is simple to configure. The default installation of CUCM lists the name in the database field used by the phone configuration file to identify the CUCM server(s) the phone should use for registration. To change the value in this field, follow these steps:

- 1. In CUCM Administration, navigate to System > Server.
