+   15.5.3 Information Flow 727
+   15.5.3.1 Direction of Flow 727
+   15.5.3.2 Magnitude of the Flow 728
+   15.5.3.3 I/O Timing 729
+   15.5.3.4 Software Device Drivers 729
+   15.5.4 Places 729
+   15.6 Summary 730
+   15.7 Review Questions 730
+   15.8 Thought Questions 730

# 16 Working Outside of the Processor I: Refining the Model of Interprocess Communication 733

+   16.1 Communication and Synchronization with the Outside World 733
+   16.2 The Local Device Model 734
+   16.2.1 Control, Synchronization, and Places 735
+   16.2.1.1 A Serial Model 735
+   16.2.1.2 A Parallel Model 736
+   16.2.2 Information — Data 737
+   16.2.3 Transport 737
+   16.3 Implementing the Local Device Model – A First Step 737
+   16.3.1 An Overview 737
+   16.3.1.1 Main Memory Address Space 738
+   16.3.1.2 I/O Ports 738
+   16.3.1.3 Peripheral Processor 739
+   16.3.2 Main Memory Address Space – Memory-Mapped I/O 739
+   16.3.2.1 Address Bus 740
+   16.3.2.2 Data Bus 740
+   16.3.2.3 Control Bus 740
+   16.3.2.4 Read 741
+   16.3.2.5 Write 741
+   16.3.2.6 Bidirectional Bus 742
+   16.3.3 I/O Ports – Program-Controlled I/O 744
+   16.3.4 The Peripheral Processor 744
+   16.4 Implementing the Local Device Model – A Second Step 745
+   16.4.1 Information Interchange – An Event 745
+   16.4.2 Information Interchange – A Shared Variable 746
+   16.4.3 Information Interchange – A Message 746
+   16.5 Implementing an Event-Driven Exchange – Interrupts and Polling 747
+   16.5.1 Polling 747
+   16.5.2 Interrupts 749
+   16.5.2.1 Single Interrupt Line with Single Device 749
+   16.5.2.2 Single Interrupt Line with Multiple Devices 749
+   16.5.2.3 Multiple Interrupt Lines 753
+   16.5.3 Masking Interrupts 754
+   16.6 A Message 755
+   16.6.1 Asynchronous Information Exchange 756
+   16.6.1.1 Strobes 756
+   16.6.1.2 Strobe with Acknowledge 757