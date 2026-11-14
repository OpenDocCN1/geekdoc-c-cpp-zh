# 18.7 SUMMARY

In this chapter, we studied four different, commonly used network-based input/output designs. For each, we examined the problems that motivated designers to develop the interface, identified the contributions that each has brought about, and cited the strengths and weaknesses of each approach. For each architecture, we examined the transport mechanism, learned how

control and synchronism is affected, and explored how message senders and receivers are identified. We began with the traditional EIA-232 standard asynchronous serial interface and then moved to the synchronous model utilized by the USB. We concluded with the PC bus as a small LAN and the CAN bus, a LAN commonly used in automotive applications.

# 18.8 REVIEW QUESTIONS

# Common Network-Based Architectures

+   18.1 The chapter introduces four common network-based architectures. What are they?

# The EIA-232 Interface

+   18.2 What was the originally intended purpose of the RS-232 (now EIA-232) interface standard?
+   18.3 What are the primary signals that comprise the EIA-232 interface standard? Give a brief description of each and its function in a data exchange.
+   18.4 What do the acronyms DCE and DTE mean?
+   18.5 What is a null modem? Explain how such a device works.
+   18.6 What is the format of an EIA-232 character?
+   18.7 Why is information exchange over the EIA-232 network described as asynchronous?
+   18.8 In an EIA-232 exchange, what is the purpose of the start and stop bits in a data character?
+   18.9 What is meant by the term baud rate?
+   18.10 What are the signaling levels for a logical 0, logical 1, true or ON control signal, and a false or OFF control signal?

# The Universal Serial Bus

+   18.11 What are some of the problems that the designers of the USB are trying to solve?
+   18.12 What are some of the major contributions of the USB?
+   18.13 Does the USB implement interrupts?
+   18.14 What are the major elements of the USB protocol stack? Briefly describe the function of each.
+   18.15 What is the purpose of the host controller? The root hub?
+   18.16 How is the address of a device made known to the USB software?
+   18.17 What is a transfer descriptor?
+   18.18 What kinds of data transfer does USB support?
+   18.19 What is a device descriptor? What is its purpose?
+   18.20 How many kinds of descriptors does the USB support? What is the purpose of each?
+   18.21 How many class descriptors does the USB support?

+   18.22 How many phases comprise a USB transaction? What are they?
+   18.23 Do all USB transactions support guaranteed delivery of data?

# I²C – A Local Area Network

+   18.24 What are the two primary signaling lines on the I²C bus? What is the function of each?
+   18.25 What are some of the problems that the designers of the I²C bus are trying to solve?
+   18.26 What are some of the major contributions of the I²C?
+   18.27 How does the I²C differ architecturally from the USB and EIA-232 busses?
+   18.28 What are the two primary signaling lines on the I²C bus? What is the function of each?
+   18.29 Describe the steps involved in a bus master read operation on the I²C bus.
+   18.30 Describe the steps involved in a bus master write operation on the I²C bus.
+   18.31 Does the I²C bus support multiple masters?
+   18.32 With multiple masters, how is a bus contention situation resolved?

# The Controller Area Network – The CAN Bus

+   18.33 What are some of the more significant differences between the CAN bus and the I²C, USB, and EIA-232 signaling?
+   18.34 What are some of the problems that the designers of the CAN bus were trying to solve?
+   18.35 What are some of the major contributions of the CAN bus?
+   18.36 What are the two primary signaling lines on the CAN bus? What is the function of each?
+   18.37 The CAN bus signaling protocol specifies two states, dominant and recessive. What do these terms mean in this context?
+   18.38 Describe the format for message that is sent over the CAN bus.
+   18.39 How are errors managed on the CAN bus?