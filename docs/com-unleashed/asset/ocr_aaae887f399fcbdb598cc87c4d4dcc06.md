> > Now much you tell me, and yet more I perceive.
> >
> > —Melian the Maia

This chapter describes the various parts of an MSMQ enterprise and how to configure and manage them. You’ll get a chance to look at the tools used to create, destroy, monitor, and configure queues. You’ll also examine the applications and components that depend on queues.

Because I discuss provisional programming issues here as well, I should point out that there are two basic approaches to building MSMQ applications, the MSMQ API and the MSMQ ActiveX Components. You can choose one or the other or mix and match. The API provides the lowest-level support, exposing all the various MSMQ services and requiring a little more code in most cases. The ActiveX approach is designed to be generic enough to service any development environment and provides sufficient power with a simplified, object-oriented COM programming model. Throughout this chapter, when I refer to programming issues, I will provide descriptions of both environments.

A basic MSMQ exchange involves three parties:

+   - The sending application
+   - The target queue
+   - The receiving application

Client applications use MSMQ by sending messages to the queues that the MSMQ servers monitor. If the target queue is not local to the sender, the sender’s local servers are responsible for forwarding the message through the MSMQ enterprise. The message is passed from queue to queue until it finally reaches its destination. The message body format is arbitrary from the perspective of MSMQ, but must obviously be understood by the end points sending and receiving the messages. Queues act as intermediaries, enabling the applications involved to run at different points in time and on any system within a distributed MSMQ enterprise. The decoupling effect provided by the queues makes the client and server elements of an MSMQ system very independent. Most operations occur asynchronously, enabling applications to adopt a fire-and-forget mentality when sending messages.

# MSMQ Objects and Properties

An MSMQ system is defined in terms of several key object types:

+   - Messages
+   - Queues
+   - Machines