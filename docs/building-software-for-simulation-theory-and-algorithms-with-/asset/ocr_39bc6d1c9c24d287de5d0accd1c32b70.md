# # CHAPTER 6

# # APPLICATIONS

The applications in this chapter highlight the main features of the simulation framework. The first application, which examines closed-loop control through a packet-switched network, shows how the software design promotes reuse of models across simulation frameworks. The second application is also concerned with control; it looks at using load to regulate frequency in an electrical power system. This example contains complicated state events and computationally demanding continuous dynamics and leaves open at least two interesting questions that a student might pursue.

# ## 6.1 CONTROL THROUGH A PACKET-SWITCHED NETWORK

Recent work in the design of networked control systems has focused extensively on communication networks that lose information. The simplest models use a Bernoulli process for packet losses and impose a fixed delay on packets that are successfully delivered. Control processes can be surprisingly robust to this type of error, and given the relative ease with which its consequences can be analyzed, it is tempting to select a control network whose behavior closely approximates this model (Hespanha et al. [57] give an overview of recent work in this area; see also the article by Feng-Li et al. [38]).

Conversely, interest in control over packet-switched networks is spurred by relatively inexpensive communication technology that exists for data-processing applications. This networking technology is designed to favor delay and variation in delay