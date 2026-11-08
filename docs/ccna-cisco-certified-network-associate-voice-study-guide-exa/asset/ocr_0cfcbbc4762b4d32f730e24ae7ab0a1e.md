+   - As a last resort, you can return the Unity Express module to the factory defaults with the restore factory default command. The module must be offline in order to execute the factory restore process.
+   - If the factory defaults are restored, all data and configuration settings are removed.

# 640-460: Explain Basic Maintenance and Troubleshooting Methods for UC500

+   - The UC500 series offers a command prompt interface similar to the standard IOS; however, it has limited functionality.
+   - Telnet can be used to access the CLI of a UC500 series device through the standard switch ports on the device.
+   - The most common way to access and troubleshoot the UC500 series is through the web-based interface or the Cisco Configuration Assistant (CCA). Both methods offer a GUI interface for configuration verification and status review.

# 640-460: Describe How QoS Addresses Voice Quality Issues

+   - The class of service (CoS) QoS solution allows for eight classes.
+   - Classes 0 through 5 are used for data. Classes 6 and 7 are used only by routing protocols.
+   - VoIP data typically receives class 5 markings.
+   - The three stages of QoS processing are traffic classification, traffic marking, and traffic queuing.
+   - Cisco’s auto-QoS feature uses Low Latency Queuing (LLQ) for VoIP traffic.
+   - The auto qos voip command is used to configure Cisco auto-QoS.
+   - Three options exist for the auto qos voip command: cisco-phone, cisco-softphone, and trust.
+   - The cisco-phone option limits the QoS markings to those applied by a Cisco IP phone.
+   - The cisco-softphone option allows the Cisco software-based IP phone on a PC to apply QoS markings.
+   - The trust option accepts all QoS marking sources and is usually used only within the infrastructure devices in the distribution and core layers.