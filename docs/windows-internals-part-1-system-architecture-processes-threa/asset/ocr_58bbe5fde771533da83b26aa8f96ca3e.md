+   - Object manager filtering Security software can remove certain access rights granted to processes and threads to defend your utilities against certain operations. (These are discussed in Chapter 8 in Part 2.)

+   - NDIS Lightweight Filters (LWF) and Windows Filtering Platform (WFP) filters Security software can intercept socket operations (accept, listen, connect, so and on) and even the packets themselves. With LWF, security vendors have access to the raw Ethernet frame data that is going from the network card (NIC) to the OS.

+   - Event Tracking for Windows (ETW) Through ETW, many types of operations have interesting security properties can be consumed by a user-mode component, which can then react to data in real-time. In some cases, specific ETW registrations are available to anti-malware-protected processes under NDA with Microsoft and participation in security programs, which give access to a greater set of tracing data. (ETW is discussed in Chapter 8 in Part 2.)

# HyperGuard

On systems that run with virtualization-based security (described earlier in this chapter in the section "Virtualization-based security”), it is no longer true that attackers with kernel-mode privileges are essentially-running at the same security boundary as a defense/prevention mechanism. In fact, such attackers would operate at VTL 0, while a mechanism could be implemented in VTL 1. In the Anniversary Update of Windows 10 (version 1607), such a mechanism does exist, which is appropriately named HyperGuard. HyperGuard has a few interesting properties that set it apart from PatchGuard:

+   - It does not to rely on obfuscation. The symbol functions and names that implement HyperGuard are available for anyone to see, and the code is not obfuscated. Complete static analysis is possible. This is because HyperGuard is a true security boundary.

+   - It does not operate to non-deterministically because this would provide no advantage due to the preceding property. In fact, by operating deterministically, HyperGuard can crash the system at the precise time when unwanted behavior is detected. This crash data will contain clear and actionable data for the administrator (and Microsoft’s analysis teams), such as the kernel stack, which will show the code that performed the undesirable behavior.

+   - Due to the preceding property, it can detect a wide variety of attacks, because the malicious code does not have the chance to restore a value to its correct value during a precise time window, which is an unfortunate side-effect of PatchGuard’s non-determinism.

HyperGuard is also used to extend PatchGuard’s capabilities in certain ways, and to strengthen its ability to run undetected by attackers trying to disable it. When HyperGuard detects an inconsistency, it too will crash the system, albeit with a different code: 0x18C (HYPERGUARD_VIOLATION). As before, it might be valuable to understand, at a generic level, what kind of HyperGuard will detect, which you can see in Table 7-24.