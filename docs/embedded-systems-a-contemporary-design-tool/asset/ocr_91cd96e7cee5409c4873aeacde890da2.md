![](bbox=[0.283, 0.083, 0.582, 0.256])

When needed, such keys need to be transferred to RAM where they can be used to support outside world information exchange. Like the data transfer from a passport when checking onto an aircraft, the Secure ROM to RAM transfer occurs in clear text. If the transfer is affected over a system bus in clear text, then during that time data compromise is possible. To mitigate such a possibility, the RAM should be implemented in the SOC. A similarly secure boot loader should ensure that the system executes a clean boot of all of the proper and legitimate firmware and that any attempts to alter or defeat the boot loader should be blocked.

The keys stored in the ROM can also be encrypted. However, the keys to the encryption of the secret keys now have to be held somewhere and protected and the problem repeats. Limited and controlled access to the SOC and enclosed memories and a task assigned to the memory management unit (MMU) can help; however, the probability that ultimately someone can defeat the protection exists. The goal should be to make that process as difficult and complex as possible.

In Chapter 14, we discuss a power management technique called Power Gating, in which the power to designated subsystems is lowered or turned off during passive periods to aide in reducing system power consumption. Care must be taken when using such a technique. If the trust zone is included in the set of subsystems for which the power can be controlled, then it becomes vulnerable to side channel attacks. If the technique is employed, then the trust zone, at the minimum, should be segregated and managed by a separate system in a manner similar to that discussed earlier in this chapter under fail operational capability.

# 8.23.5 Firewall

# denial of service attack

Taking an external view of an embedded system, a denial-of-service attack is an attack on a system initiated with the intent of diverting or preventing it from performing its intended job. Such an attack typically commences by flooding targeted machine or resource with superfluous requests, potentially from a wide variety of sources, in an attempt to overload the system and prevent some or all legitimate requests from being fulfilled.

# firewall

A basic firewall, illustrated in Figure 8.45, is a tool that can help to handle and mitigate such attacks. In the context of embedded systems, the firewall is considered to be host-based and comprises a layer of software on the system that monitors and controls traffic into and out of the system.

Fundamentally, in this context, the firewall is a router or set of routers and a filter that act, in concert, as a gatekeeper to screen network traffic between the Internet and a trusted and secure local site. The device utilizes a set of security rules to manage and control traffic into or out of the secured device.