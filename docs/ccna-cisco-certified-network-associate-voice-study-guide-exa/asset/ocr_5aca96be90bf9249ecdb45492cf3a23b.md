+   7. ☑ C is correct. Retransmission is not a viable solution. In voice communications, the data stream must be continuous. For this reason, waiting on retransmitted data is not possible.
+      ☒ A, B, and D are incorrect. QoS, PLC, and jittering the packet loss are all possible solutions, assuming the packet loss is less than 10 percent.

+   8. ☑ C is correct. VoIP actually uses the same network as your computer data.
+      ☒ A, B, and D are incorrect. All of the listed items in answers A, B, and D are valid benefits of VoIP when contrasted with PBX-based solutions.

# # LAB ANSWER

While answers may vary, you will likely implement quality of service (QoS). By implementing QoS, you further optimize the network to allow for voice traffic. It's always important to remember that, when you implement VoIP on a network, the existing network applications and traffic have to allow for the VoIP communications. This may require greater network segmentation, but it will nearly always require the implementation and configuration of QoS solutions.