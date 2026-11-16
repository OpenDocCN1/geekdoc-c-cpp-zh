When multiple connections are in use, the amount of memory required rises linearly with the number of connections. However, we can share the memory used by the queues among all the connections; except in extreme network conditions, it is unlikely that all connections will need large amounts of queue space at the same time.

In some cases, though, this will still prove to be too much memory usage. If we need to reduce the memory footprint further, we can choose to reduce the number and size of the packets stored in the queues, although the measures we need to take may seem a little draconian. We know that the arrival of packets and messages not marked as reliable are not critical to the correct execution of our application. Therefore, we can choose not to store these packets and messages in the queues.

The way this works is simple; when we store a reliable packet in the outgoing packet queue, we remove from it all the messages that are not themselves reliable. This ensures that only the most important parts of these packets are queued for possible resend, reducing the memory used. In the incoming packet queue, we can choose not to store unreliable packets that cannot be immediately processed, and we can strip the unreliable elements from reliable packets that do need to be queued.

The effects of such packet and message stripping can be undesirable, causing the times that packets are lost to be more apparent to the user. This can happen because several unreliable packets containing such things as positional updates for visible enemies will be lost each time the client has to wait for a missed packet to be resent. We can ameliorate this effect somewhat by selectively implementing it as the queues become full. When the queues are empty, all messages will be stored, but if a queue surpasses a certain length, the network library should go through and cull unreliable packets and messages from the queue. This reduces the appearance of packet loss, except in the times that it is severe.

# Conclusion

We have seen that reliable messaging is an important part of a networking library, and how the traditional method of implementing reliable messaging has several problems. We saw that by moving the responsibility for detecting a missed reliable packet to the client, we could overcome these problems and produce a robust, reliable messaging system. Finally, we examined the memory requirements for this system and looked at ways to reduce memory usage, especially during times of extreme packet loss.

# Further Reading

+   - [Donahoo01] Donahoo, Michael J. and Kenneth L. Calvert. TCP/IP Sockets in C: Practical Guide for Programmers. Morgan Kaufmann Publishers, 2001.
+   - [Napper97] Napper, Lewis. Winsock 2.0. John Wiley & Sons, Inc, 1997.