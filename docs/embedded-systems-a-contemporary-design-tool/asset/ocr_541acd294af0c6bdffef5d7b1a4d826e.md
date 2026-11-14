![](bbox=[0.25, 0.08, 0.8, 0.16])

architectures. Devices may be designed with several different levels of capability: all can transmit or receive; some can transmit only, while others may receive only. Failure of the link at a single device will not compromise the entire net. A severed net, however, can prevent communication beyond the severed point.

# 8.13.3 The Ring Configuration

The basic ring structure is shown in Figure 8.14. The ring configuration also serves as the basis for token ring type networks. This configuration typically has no bus master (on some occasions, one of the nodes is designated as lord). Each device accepts all of the messages circulating within the ring. If a device receiving the message is the addressed device, the message is accepted; otherwise, the message is passed on to the next device. Such a configuration has been utilized for many years as the basis for IBM's token ring. When configured with one node designated as lord, people have gotten into the habit of referring to the architecture as a Tolkien ring. Variants on the ring architecture are common in communication networks in automotive or aircraft applications.

![](bbox=[0.25, 0.48, 0.7, 0.58])

Failure of the link in the basic ring configuration still permits full interconnection of all comprising nodes. If one of the links is lost, the architecture reduces to the multidrop bus configuration. A variant on the ring adds a second inner ring, as we see in the leftmost network in Figure 8.15.

![](bbox=[0.25, 0.7, 0.8, 0.89])