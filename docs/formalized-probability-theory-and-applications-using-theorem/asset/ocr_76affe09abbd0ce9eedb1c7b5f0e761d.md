by a collection round named Command Period (CP), which in turn consists of a collection command period, a Listen Period (LP) and an Acknowledgment Period (AP). The interrogator then waits for the responses from the tags that are sent randomly. The tag collection is done based on a predetermined algorithm that complies with the ISO/IEC 18000 7 standard. Thus, this system has two properties:

+   1. The probability that a message can be delivered successfully within i slots is l - (n - 1 / n)

+   2. If the collection process is long enough, eventually any message can be delivered successfully.

This communication protocol can be modeled as a DTMC with 4 states: s0 (start), s1 (try), s2 (lost) and s3 (delivered), as shown in Figure 3.

In the start state, the message is generated. The next state is always the state try and thus the probability from the start state to try state is 1. The probability of losing a message is $\alpha$. Thus in the case of losing a message, the system will move to the lost state with probability $\alpha$. Whereas, it moves to the delivered state with probability $\beta = 1 - \alpha$ in case of a successful transmission. Hence, the probability that a message can be delivered successfully is $\beta$, which equals to $1 - \alpha$. Once a message is delivered successfully, the system moves to the start state for getting ready to identify the other tags in the next time slot. When the collection process ends, the system goes to sleep mode in order to minimize power consumption. The state

# Figure 3. DTMC model of the AMQM protocol

![](bbox=[0.3, 0.62, 0.7, 0.88])