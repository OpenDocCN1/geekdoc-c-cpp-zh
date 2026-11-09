is the timeout value of INFINITE. This is important because you do not want your pending I/O operation to timeout. That causes you to return from the `GetQueuedCompletionStatus()` call with an error. The last issue is that the Receive call modifies some of the size properties to reflect the data actually retrieved. It is very important to reset these in a loop so that MSMQ doesn’t think your buffer is shrinking. An undersize buffer will return an error, but from `GetQueuedCompletionStatus()`! This is problematic because the error code you want to see is the one delivered by `MQReceiveMessage()` not `GetQueuedCompletionStatus()`. Note that the original I/O error message can be found in the internal field of the overlapped structure.

# # Queue Security

The MSMQ ActiveX components supply support for security context information, which is available through properties and methods of the MSMQMessage and MSMQQueueInfo classes. Basic MSMQ queue security features are configured when the queue is created through MSMQQueueInfo object settings. Queues can be configured to accept only authenticated messages through the Authenticate property. Queues can be set as world readable during the MSMQQueueInfo::Create() call enabling any application to receive messages from the queue, as opposed to just the owner. The QueueInfo object also supplies a Privacy Level property that allows queues to accept messages that are encrypted, unencrypted, or both.

The examples you have looked at create queues with default security. Creating queues in this way sets the creating process user and group as the queue’s user and group. The discretionary access control list is initialized to provide full control for the creator as well as property read, security read, and send access to others. No system access control list for auditing is provided.

MSMQ queues are administrator visible enterprise objects secured with standard NT security descriptors. As I discussed in the Chapter 20, “Component Load Balancing,” security features can be managed through the MSMQ Explorer. It is also possible to manage queue security through the MSMQ API call interface. Managing queue security requires knowledge of the Windows/COM+ security services discussed in Chapter 18, “COM+ Security.” Several routines supply MSMQ security support:

+   - `MQCreateQueue()`
+   - `MQGetQueueSecurity()`
+   - `MQSetQueueSecurity()`
+   - `MQFreeSecurityContext()`
+   - `MQGetSecurityContext()`