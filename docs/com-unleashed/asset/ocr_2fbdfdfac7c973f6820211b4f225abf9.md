Queue security features can be created, retrieved, and modified with the first three routines. Queues maintain standard permissions as well as queue-specific permissions such as Peek Message, Receive Message, Send Message, and Receive Journal. Queues also support read and write access to queue permissions and properties. Security context settings are used to manage message authentication through certificates. Servers impersonating another user must make use of the MSMQ security context system to send messages in the impersonation context.

# Message Security

Messages have several security provisions of their own. Messages can be digitally signed with various hash algorithms and encrypted with various encryption techniques.

The message Authentication Level property specifies whether the message requires the receiving queue to authenticate the message using its digital signature. Authentication-enabled messages can have their Hash Algorithm property set to specify a nondefault signing method. MSMQ supplies several signing choices through the MSMQ_CALG enumeration. Messages also provide a Sender Certificate property, enabling applications to provide their own certificates and authentication management.

A message’s Privacy Level property indicates whether the message should be encrypted. The Encrypt Algorithm property specifies the type of encryption to be used on the message. If this property is not set, MSMQ uses a default value. Currently RC2 and RC4 algorithms are supported through public key security implemented by the underlying RSA provider.

# Summary

In this chapter, you have examined the advanced features of MSMQ in gory detail. You have learned how to build transactional MSMQ applications with message-based, internal, DTC, and MTS-managed transactions. You have also examined the mutually exclusive asynchronous techniques for managing MSMQ queues. The sample Ping/Pong and OrderEntry applications have provided a simple base for exploration into cursors and the various properties offered by messages and queues. If you made it this far, you’re definitely bucking for MSMQ guru.