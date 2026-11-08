The solution, LLQ, tells the scheduler to treat one or more queues as special *priority queues*. The LLQ scheduler always takes the next message from one of these special priority queues. Problem solved: very little delay for packets in that queue, resulting in very little jitter as well. Plus the queue never has time to fill up, so there are no drops due to the queue filling up. Figure 18-17 shows the addition of the LLQ logic for the voice queue.

![](bbox=[0.141, 0.176, 0.614, 0.318])

*Figure 18-17  LLQ Always Schedules Voice Packet Next*