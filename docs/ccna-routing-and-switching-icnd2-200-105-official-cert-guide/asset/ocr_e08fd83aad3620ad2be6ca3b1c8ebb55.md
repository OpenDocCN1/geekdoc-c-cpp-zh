# # IPv4 Troubleshooting Tools

**This chapter covers the following exam topics:**

+   - **1.0 Network Fundamentals**
+   - 1.8 Configure, verify, and troubleshoot IPv4 addressing and subnetting
+   - **4.0 Infrastructure Services**
+   - 4.1 Describe DNS lookup operation
+   - 4.2 Troubleshoot client connectivity issues involving DNS
+   - **5.0 Infrastructure Management**
+   - 5.6 Use Cisco IOS tools to troubleshoot and resolve problems
+   - 5.6.a Ping and traceroute with extended option

This appendix is from Chapter 23 of *CCENT/CCNA ICND1 100-105 Official Cert Guide*. Although the ICND2 exam objectives do not explicitly reference the content covered here, the skills and concepts covered are important to have a solid understanding of as a future IT professional. All references to other content in this appendix refer to *CCENT/CCNA ICND1 100-105 Official Cert Guide* and not this book.

The first two chapters here in Part VI of the book made us think more about the entire enterprise IPv4 network. Chapter 21, “Subnet Design,” examined all the subnets in a subnetting plan, so you could look at an enterprise network and know which subnets could be used, beyond what subnets were already in use. Chapter 22, “Variable-Length Subnet Masks,” took that a step further, looking at the entire enterprise IPv4 network when using variable-length subnet masks (VLSM), thinking about what subnets do exist and which ones could exist within the rules of VLSM.

This chapter and the next keep that approach toward the entire enterprise network. However, the topics more from subnetting design to troubleshooting. How do you troubleshoot an IPv4 network? How do you verify correct operation, identify root causes, and fix those various IP routing features? How do you do that in the presence of an IP addressing and subnetting plan, requiring you to apply all that subnetting math from Part IV of this book and from the last few chapters? This chapter and the next start to answer some of those questions.

In particular, this chapter focuses on IP troubleshooting tools, with two in particular: ping and traceroute. Both tools test the IPv4 data plane; that is, the ability of each networking device to route or forward IPv4 packets. A problem with routing is often a symptom but not a root cause, with the root cause then being other problems, like interface failures, routing protocol issues, misconfiguration of various features, and the like.

The chapter ends with a short discussion of two other router tools that can also be useful for troubleshooting: Telnet and Secure Shell (SSH).