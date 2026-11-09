**TABLE 23.1 Continued**

| Property | Description |
|---|---|
| `PROPID_M_RESP_QUEUE_LEN` | The length of the response queue |
| `PROPID_M_SECURITY_CONTEXT` | Security information for authenticating the message |
| `PROPID_M_SENDER_CERT` | The security certificate used to authenticate the message |
| `PROPID_M_SENDER_CERT_LEN` | The length of the sender certificate buffer |
| `PROPID_M_SENDERID` | The user who sent the message |
| `PROPID_M_SENDERID_LEN` | The length of the sender identifier |
| `PROPID_M_SENDERTYPE` | The type of sender identifier found in `PROPID_M_SENDERID`; currently, the only type of sender identifier available to MSMQ is a security identifier (SID) |
| `PROPID_M_SENTTIME` | The date and time that the message was sent by the source queue |
| `PROPID_M_SIGNATURE` | The digital signature for authenticating the message |
| `PROPID_M_SIGNATURE_LEN` | The length of the digital signature used to authenticate the message |
| `PROPID_M_SRC_MACHINE_ID` | The computer where the message originated |
| `PROPID_M_TIME_TO_BE_RECEIVED` | How long the receiving application has to remove the message from the queue |
| `PROPID_M_TIME_TO_REACH_QUEUE` | How long the message has to reach the queue |
| `PROPID_M_TRACE` | The route of the message is traced |
| `PROPID_M_VERSION` | The version of MSMQ used to send the message |
| `PROPID_M_XACT_STATUS_QUEUE` | The format name of the transaction status queue |
| `PROPID_M_XACT_STATUS_QUEUE_LEN` | The length of the transaction status queue's format name buffer |

# Queues

Message queues are the buffering mechanism that makes MSMQ an effective tool for developing loosely coupled applications. Queues store a message until an appropriate application sees fit to retrieve the message. Queues make it possible for various components to communicate, even though they execute at different times and at various locations within an enterprise.