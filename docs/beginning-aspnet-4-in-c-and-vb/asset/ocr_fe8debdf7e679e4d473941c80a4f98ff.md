two different queue types are possible: source journaling and target journaling. Source journaling is turned on with the properties of a message; journal messages are stored with the source system. Target journaling is turned on with the properties of a queue; these messages are stored in the journal queue of the target system.

Dead-letter queues store messages if a message doesn't arrive at the target system before a specific timeout is reached. Contrary to synchronous programming where errors are immediately detected, errors must be dealt with differently using Message Queuing. The dead-letter queue can be checked for messages that didn't arrive.

Administration queues contain acknowledgments for messages sent. The sender can specify an administration queue from which it receives notification of whether the message was sent successfully.

A response queue is used if more than a simple acknowledgment is needed as an answer from the receiving side. The receiving application can send response messages back to the original sender.

A report queue is used for test messages. Report queues can be created by changing the type (or category) of a public or private queue to the predefined ID (55EEBF33-CCE9-11CF-B108-0020AFD61CE9). Report queues are useful as a testing tool to track messages on their route.

System queues are private and are used by the Message Queuing system. These queues are used for administrative messages, storing of notification messages, and to guarantee the correct order of transactional messages.

# MESSAGE QUEUING ADMINISTRATIVE TOOLS

Before looking at how to deal with Message Queuing programmatically, this section looks at the administrative tools that are part of the Windows operating system to create and manage queues and messages.

![](bbox=[0.13, 0.91, 0.85, 0.97])

# Creating Message Queues

Message queues can be created with the Computer Management MMC snap-in. On a Windows 7 system, you can start the Computer Management MMC snap-in with the Start Control Panel Administrative Tools Computer Management menu. In the tree view pane, Message Queuing is located below the Services and Applications entry. By selecting Private Queues or Public Queues, new queues can be created from the Action menu (see Figure 46-5). Public queues are available only if Message Queuing is configured in Active Directory mode.

![](bbox=[0.57, 0.78, 0.92, 0.97])

FIGURE 46-5