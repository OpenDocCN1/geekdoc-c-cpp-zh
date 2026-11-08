
“Accuracy of your requirements determines the benefits of your efforts.” If the quality requirements are not accurate, the QoS solutions that you implement are not likely to prove beneficial to your users. In fact, a poorly designed QoS solution can cause more trouble than it solves. Therefore, successful QoS implementation begins with quality requirements development.

Once you have a clear picture of the quality requirements in your network, you can begin to consider the different QoS tools that may assist you in meeting those requirements. These tools will be targeted at reducing latency, jitter, and delay, and they may accomplish these tasks through the use of prioritization, queuing, and dedicated connections. You can think of QoS tools as a collection of technologies that allow you to use any physical network more efficiently. QoS tools cannot make the network faster, but they can enforce or suggest better use of the network.

Several QoS types are available and will be covered in-depth in Chapters 4 and 17. For now, just know that QoS solutions can solve the problem of delay on most modern networks. You simply have to enable it and properly configure it to prioritize voice data. If your current network is a computer data-only network, it is highly unlikely that any QoS solutions have been implemented or configured.

### Jitter Solutions

Jitter buffers work at the receiving endpoint in most cases. Rather than sending the voice frames immediately up for processing, the jitter buffer holds the incoming voice frames for a very short time and then begins sending them up for processing at regular intervals, resulting in a smooth stream of audio projected through the speaker. The hold time or delay is very short, usually well under 200 milliseconds (ms). More often than not, the jitter buffer will be 100 ms or less.

Figure 1-3 illustrates the concept of a jitter buffer. Notice that the incoming packets have variable delays. The delay between the first packet coming into the buffer and the second packet is 30 ms, while the delay between the second and third packets is 15 ms. Within the jitter buffer, the packets are stored and sent out at 20-ms intervals.

![](img/ee67e6cd30f16bc39d653f87870eabb5_56_0.png)

It’s very important to understand the difference between a static jitter buffer and a dynamic jitter buffer. Static jitter buffers are of a fixed size. This fixed size means that the buffer is unable to store more than there are too few packets in the buffer to service the needed upstream rate to the telephone or software. Using a dynamic jitter buffer may resolve this issue. A dynamic jitter buffer evaluates the incoming delays and adjusts the jitter buffer size accordingly. While the dynamic buffer may utilize more processing power on the receiving device, it is usually preferred due to its ability to function best in a network with variable utilization levels.

### Packet Loss Solutions

When packet loss occurs, different techniques can be used to address it. These techniques include:

- **Ignoring packet loss** — This solution is actually what most VoIP implementations do. Rather than trying to accommodate for lost packets or retransmit them, the lost packets are simply ignored up to a specified threshold.
- **Interpolating lost packets** — Interpolation is the process of estimating unknown values based on known values and patterns. Interpolation can be very processor intensive and can increase delay. Depending on the codec used, interpolation may not be an option.
- **Retransmitting packets** — Retransmission is very common with standard data transfers; however, it is not very useful with VoIP streams, since the retransmitted data would likely arrive too far out of synchronization. The receiver would have to send a request for the sender to retransmit the data, since UDP is used. This solution means that the sender would have to buffer transmitted packets for some time, and it also means that the delay between the sender and receiver would have to be phenomenally low. For these reasons, retransmission is seldom used with lost packets in VoIP systems.
- **Transmitting redundant packets initially** — An alternative to retransmission is to transmit multiple copies of the same data all the time. The problem with

### SCENARIO & SOLUTION

| Scenario | Solution |
|---|---|
| You are experiencing dropped calls. It appears to be happening because of varying delay rates in packet delivery. What technology could help with this scenario? | A jitter buffer can help with this scenario. A jitter buffer is used to counter the impact of variable delay (jitter) in network communications. It attempts to stream the arriving packets to the audio processor at regular intervals rather than at varying rates. |

When you view the help, you will notice that you can use the -w switch to determine the amount of time to wait for a reply. Once this time is expired, the pathping command assumes no reply is coming and will consider the non-reply as a dropped packet.

### Use the pathping Command

1. Type `pathping -w 50 www.sysedco.com` and press ENTER.
2. Type `pathping www.sysedco.com` and press ENTER.

You should see results similar to those in Figure 1-4. Notice in Figure 1-4 that the first time, 19 packets were dropped, but the second time, no packets were dropped. This is because we entered a very low wait time of just 50 ms the first time. However, this shows one simple way that you can look for dropped packets, by specifying the wait time that you can accept. For example, you may want to try the same command again with a wait time of 150 ms, which is closer to what we want for VoIP communications.

![](img/ee67e6cd30f16bc39d653f87870eabb5_59_0.png)

```text
C:\Users\Tom>pathping -w 50 www.sysedco.com

Tracing route to www.sysedco.com [64.71.229.252]
over a maximum of 30 hops:
  0  BCER7 [192.168.10.222]
  1  64.71.229.252

Computing statistics for 25 seconds...
            Source to Here   This Node/Link
Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  Address
  0                                           BCER7 [192.168.10.222]
  1   82ms   19/ 100 = 19%     0/ 100 =  0%   64.71.229.252

Trace complete.

C:\Users\Tom>pathping www.sysedco.com

Tracing route to www.sysedco.com [64.71.229.252]
over a maximum of 30 hops:
  0  BCER7 [192.168.10.222]
  1  64.71.229.252

Computing statistics for 25 seconds...
            Source to Here   This Node/Link
Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  Address
  0                                           BCER7 [192.168.10.222]
  1   82ms    0/ 100 =  0%     0/ 100 =  0%   64.71.229.252

Trace complete.

C:\Users\Tom>
```

## CERTIFICATION SUMMARY

In this chapter, you began your journey to mastery of VoIP. You learned about the benefits of VoIP and the applications it provides to your users. You also reviewed the basics of TCP/IP networking as a refresher, since this information is assumed knowledge for the CCNA Voice exams. Finally, you explored the quality factor as it relates to VoIP communications. You learned why VoIP makes special demands on the quality of network communications and how to address common hindrances to this quality. In the next chapter, you will review fundamental networking technologies from the perspective of a VoIP professional.

## TWO-MINUTE DRILL

### 640-460: Identify the Factors that Impact Voice Quality

- [ ] Delay is the time it takes for data to go from one point to another on your network.
- [ ] Jitter is the variance in delay on your network.
- [ ] Jitter can cause poor voice quality and even dropped calls.

### 642-436: Describe Voice Quality Considerations

- [ ] Jitter buffers can help to counter the impact of jitter on VoIP calls.
- [ ] Packet loss must be addressed in order for your VoIP network to function properly.
- [ ] Retransmission of dropped packets is not a viable solution for packet loss in VoIP communications.
- [ ] Quality of service (QoS) solutions must be used on IP networks that also service VoIP calls.
