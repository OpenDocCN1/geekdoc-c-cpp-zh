
acknowledgments _must_ arrive once they have been sent to avoid the host resending the packet in question unnecessarily. This implies that acknowledgment messages should be set to be reliable, but doing so necessitates having acknowledgments for the acknowledgments, and before you know it, every packet is set to be reliable.

## A Simpler Method

From the preceding description of a traditional reliable messaging implementation, we can see some areas that need improvement. The two most important of these are reducing the number of acknowledgments sent, and removing the need for them to be sent reliably.

Reducing the number of acknowledgments sent can be partially accomplished by adding an additional restriction to our reliable messages. If we can guarantee that reliable messages must be processed in the order that they were sent, then receiving an acknowledgment of a given packet automatically implies receipt of every prior packet. This is because, to maintain the in-order restriction, we know that all the previous packets must also have been processed. However, the need to send acknowledgment packets quickly to avoid the host resending packets it thinks have been missed reduces the usefulness of this somewhat.

If we can remove the need to send an acknowledgment quickly, we can reap several rewards. We will not have to send acknowledgments as often, and when we do send one, we can just acknowledge the most recent reliable packet processed. Additionally, there would no longer be a need to send acknowledgments reliably. Unfortunately, while the host is responsible for detecting a missed reliable packet, our hands are tied. This, then, will be our main point of attack.

The simplest way to remove the responsibility for detecting a missed reliable packet from the host is to move it to the client. For this to happen, a client must quickly detect that a reliable packet has been missed. We know that only reliable packets will ever need to be resent, and that ideally two reliable packets will be broken up with one or more unreliable packets. We also know that packets should arrive with a consistent frequency, due to the heartbeat system message.

Using this knowledge, we can formulate a method by which we can quickly detect a missing reliable packet. The easiest way to do this is to allow every incoming packet to contain enough data to infer a missing reliable packet. Since we know that packets are arriving at a consistent frequency (due to the heartbeat system message), we know that we can make such an inference quickly. For example, if 10 packets arrive in a second, we know that we can infer the existence of a missing reliable packet as soon as the next packet arrives, one tenth of a second later.

## Packet Identifiers

However, how do we allow an incoming packet to infer the existence of a missing reliable packet? Every reliable packet needs two pieces of data: a flag to say that it is reliable and an identifier, by means of which it can be acknowledged. An unreliable packet, on the other hand, only requires a flag to say that it is not reliable; it does not need an identifier. This means that, should we assign an identifier to an unreliable packet, any number of unreliable packets can have the same identifier without any side effects. By combining the reliable/unreliable flag with the packet identifier, we can create a simple packet numbering system that allows us to infer the existence of a missing reliable packet.

If we use the least-significant bit of the packet identifier to store the reliable/unreliable flag, we can see that, if we choose a bit value of 0 to represent a reliable packet, all reliable packets will have an even-numbered packet identifier and all unreliable packets an odd-numbered one. Then, taking advantage of the fact that any number of unreliable packets can share an identifier, we come up with the following two rules:

- When creating an unreliable packet, the packet identifier should have the reliable/unreliable flag set to 1.
- When creating a reliable packet, the packet identifier should be incremented by 2, and then have the reliable/unreliable flag set to 0.

These simple rules allow a client to detect that a reliable packet has been missed, simply by receiving any type of packet that was sent afterwards. To accomplish this, the client must maintain a record of the identifier of the next expected reliable packet, which we will call `nextReliableID`.

### The Incoming Packet Queue

As incoming packets are received, they are placed into a queue, sorted by packet identifier. Each time the network library is updated, it processes this queue, starting with the packet with the lowest identifier. Packets from the queue are processed in order, until the queue is empty or one is found that cannot be processed, according to the following rules:

- If the packet identifier is even (reliable) and equal to `nextReliableID`, we have received the next reliable packet. Process this packet, and then increment `nextReliableID` by 2.
- If the packet identifier is odd (unreliable) and equals `nextReliableID` minus 1, we have received an unreliable packet that should be processed.
- If the packet identifier is less than `nextReliableID`, discard the packet.
- If the packet identifier is greater than `nextReliableID`, we know that we have missed a packet and cannot yet process this new packet or any subsequent packet in the queue.

After processing the incoming packet queue, we know whether a packet has been missed, and the identifier for the missed packet (`nextReliableID`).

One notable exception to these rules is that any system messages in the incoming packets are processed immediately. This happens regardless of whether the packet is queued (care should be taken to only process each system message once). This allows us to quickly fulfill remote system requests such as resends and acknowledgments. If we do not process these system level messages, there is a danger of encountering a deadlock situation. This can happen when two machines both detect missing packets from the other, and their resend requests both get queued behind the missing packet. The resend requests never get processed, thus the machines are deadlocked.

### The Resend Timer

If a packet has indeed been missed, a countdown timer, called the resend timer, if not already active, is assigned a small value and started. This small value is called the out of order delay. The purpose of this short pause is to allow a short period for the missing packet to arrive in case it is still in transit but out of order. If at any point, the missing packet arrives, the resend timer is stopped.

When the resend timer expires, the client sends a system message to the host requesting a resend of the missing packet (`nextReliableID`). At this point, the resend timer is reset to a larger value, called the re-request delay and again started. We continue requesting the missing packet every time the resend timer expires, until the missing packet arrives.

The use of automatically repeated resend requests means that the requests themselves do not have to be sent as reliable messages. Furthermore, the initial delay before requesting a missed packet allows any out of order packets to arrive, and so reduces the chance of a resend request being sent spuriously. A typical value for the out of order delay is around one-tenth of a second, and a typical value for the re-request delay is about one-half of a second.

### Acknowledgments

Since the client is now responsible for detecting missed packets and requesting packet resends, there is no longer a requirement that acknowledgments be sent quickly. Additionally, the in-order processing of packets allows us to acknowledge the most recently processed reliable packet. From such an acknowledgment, the host can infer the acknowledgment of every reliable packet sent prior to the acknowledged packet.

The net result of this is that we can send far fewer acknowledgment packets, at a far slower rate. Additionally, acknowledgment packets no longer need to be reliable, since if one is missed, the next one to arrive will implicitly acknowledgment of all the packets acknowledged by the missed one. Acknowledgments can thus be sent out at a constant rate, regardless of how many reliable messages have arrived in between. A typical value for acknowledgment frequency in such a system is one every two seconds.

### The Reliable Packet Queue

The host must keep a record of each reliable packet sent until such a time as it is acknowledged by the client. It does this by means of a reliable packet queue. As each reliable packet is sent, it is placed in the queue. When an acknowledgment arrives
