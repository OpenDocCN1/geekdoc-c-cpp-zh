a destination address is used. In contrast, remote devices will often include both the source and destination address. In the model, local devices are assumed to be in close proximity to the core system, while remote devices are often at much greater distances and tend to be network based. In the next chapter, we will begin with the local device model followed by a similar study of the remote model.

# 15.6 SUMMARY

In this chapter, we have studied how an embedded application can communicate and coordinate with the external world. We extended the interprocess and communication model developed earlier by adding a transport mechanism component. We studied the meaning of information, control and synchronization, and addressing in the context of the external world. In the next chapter, we will continue to refine the model by developing and examining the local and remote components

in greater detail from the points of view of a shared variable and a message-based interpretation of the information exchange. The objective is to establish the basic infrastructure and various implementation architectures for both models. The subsequent two chapters will study several real-world examples of each rendering of the model.

# 15.7 REVIEW QUESTIONS

# Communication with the Outside World

+   15.1 Identify the kinds of devices that an embedded application may be required to exchange information with.
+   15.2 What are some of the considerations that must be taken when designing and implementing an interface to an external world device?
+   15.3 In an earlier chapter, an intertask communication model was developed based on the answers to three questions. What are those questions, and why are they important?
+   15.4 How is the earlier model of information exchange inside of the processor extended to accommodate a similar information exchange with the outside world?

# The Transport Mechanism

+   15.5 What are the three major kinds of message exchange with external world devices?

+   15.6 What are the major architectural topographies that may be utilized to effect an interconnection with external world devices?

# Control, Synchronization, and Sharing

+   15.7 The control and synchronization of an external world exchange are characterized by what three aspects?

# Information Flow

+   15.8 Identify the three kinds of information flow between the source and destination of an external world exchange.
+   15.9 Identify and discuss the differing amounts of information that may be moved during each segment of an exchange.
+   15.10 What is the purpose of a software algorithm called a device driver in the context of an external world exchange?
+   15.11 Where is the device driver typically located in an embedded application?

# 15.8 THOUGHT QUESTIONS

# Communication with the Outside World

+   15.1 Identify or discuss possible problems that might arise when data or signals must be exchanged with the outside world compared to a similar exchange inside of the processor.
+   15.2 Identify and discuss how the source and destination of an exchange with the outside world might be recognized during an exchange with the outside world.

+   15.3 Identify and discuss how control and synchronization of the exchange between source and destination might be implemented to effect an exchange with the outside world.

# The Transport Mechanism

+   15.4 Identify and discuss possible transport mechanisms that might be used during the exchange between source and destination.