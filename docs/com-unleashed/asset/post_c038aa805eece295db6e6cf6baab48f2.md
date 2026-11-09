
## LISTING 25.5 Continued

```cpp
IMSMQMessagePtr pMsg("MSMQ.MSMQMessage");
VARIANT vtTimeout;
vtTimeout.vt = VT_I4;
vtTimeout.lVal = 0;
pMsg = pQueue->Receive( &vtMissing,
                        &vtMissing,
                        vtMissing,
                        &vtTimeout );

wprintf(L"Retrieved message label: %s\n",
        (const wchar_t *)pMsg->Label);
if ( MQMSG_CLASS_ACK_RECEIVE == pMsg->Class )
    wprintf(L"ACK: Message received\n");
else if ( MQMSG_CLASS_NACK_RECEIVE_TIMEOUT == pMsg->Class )
    wprintf(L"NACK: Message receive timeout\n");
else if ( MQMSG_CLASS_ACK_REACH_QUEUE == pMsg->Class )
    wprintf(L"ACK: Message reached queue\n");
else if ( MQMSG_CLASS_NACK_REACH_QUEUE_TIMEOUT == pMsg->Class )
    wprintf(L"NACK: Message timed out before reaching queue\n");
else if ( MQMSG_CLASS_NACK_ACCESS_DENIED == pMsg->Class )
    wprintf(L"NACK: Access denied on target queue\n");
else if ( MQMSG_CLASS_NACK_BAD_DST_Q == pMsg->Class )
    wprintf(L"NACK: Target queue not available\n");
else if ( MQMSG_CLASS_NACK_HOP_COUNT_EXCEEDED == pMsg->Class )
    wprintf(L"NACK: Exceeded hop count\n");
}
catch (_com_error &e)
{
    wprintf(L"Error receiving message: %x\n\n", e.Error());
}
}

void DestroyQueues()
{
    try
    {
        //Set up queue information using a smart pointer
        IMSMQQueueInfoPtr pQInfo("MSMQ.MSMQQueueInfo");

        //Destroy the pong queue
        pQInfo->PutPathName(PONGPATHNAME);
        pQInfo->Delete();

        //Destroy the ping queue
        pQInfo->PutPathName(PINGACKPATHNAME);
        pQInfo->Delete();

        //Display success
        wprintf(L"Queue destroyed\n\n");
    }
    catch (_com_error &e)
    {
        wprintf(L"Error destroying queues: %x\n", e.Error());
    }
}
```

### Response Queues

Response queues can be set using the message Response Queue property. The Response Queue property is set up the same way that the Administration Queue property was configured in the previous example. Response queues are used by receiving applications that want to set up a discourse with the sender. Response queues can be private queues, which would normally be unavailable to the receiver. Unlike acknowledgment messages, the messages sent to a response queue have no predefined format and can be standardized by the application developers involved.

### Message IDs

MSMQ message ID properties have some nice features that are particularly useful when working with response and administration queues. The ID Message property is a 20-byte, read-only, unique message identifier assigned to every message by MSMQ. This can come in rather handy when sorting through messages. You can retrieve the message ID any time after sending or receiving a message. What makes the ID particularly useful is the fact that all messages also have a Correlation ID property. MSMQ automatically sets the Correlation ID of all Acks and Nacks to the ID of the original message. As a participant in a response scenario, you can do the same. The Correlation ID property is read/write.

### Journals

Journals are system queues created by MSMQ that are used to keep copies of journal messages and all messages received from journal queues. Setting the Journal property of a queue through the QueueInfo object during the Queue Creation process causes MSMQ to copy all messages received from the queue into the queue journal. A separate queue journal exists for each Journal queue. Table 25.2 shows the Queue Journal property values.

**TABLE 25.2** Queue Journal Property Values

| Property Value | Description |
|---|---|
| MQ_JOURNAL | Messages removed from the queue are stored in the queue journal. |
| MQ_JOURNAL_NONE | Messages are not stored in a journal queue. |

MSMQ machines maintain a machine journal. Individual messages can be configured as journal messages through the Message Journal property. MSMQ machines supply a Dead Letter and a Transaction Dead Letter queue for storing messages that cannot be delivered. Transactional messages are always copied to the Transaction Dead Letter queue when delivery fails. Nontransactional messages must have the MQMSG_DEADLETTER flag set in their Journal property in order to be copied to the normal Dead Letter queue. Regardless, MSMQ ensures that there is never more than one copy of any message on a given machine at a time. Table 25.3 shows the Message Journal property values.

**Table 25.3 — Message Journal Property Values**

| Property Value | Description |
|---|---|
| `MQMSG_DEADLETTER` | If the message is not delivered to the receiving application within a timeout period (either *time-to-be-received* or *time-to-reach-queue*), the message is sent to a Dead Letter queue on the computer where the message is located. |
| `MQMSG_JOURNAL` | If the message is transmitted, keep it in the machine journal on the originating machine. |
| `MQMSG_JOURNAL_NONE` | The message is not kept in the originating computer's machine journal. |

## Transactions

OK, here’s the heavy stuff. If you’ve ever rolled your own transactional software, you know what I mean when I say, “You don’t want to develop this stuff in house.” Thanks to MSMQ you won’t have to. MSMQ presents a complete set of transaction services that can be easily integrated into any project, especially projects making heavy use of COM+. The highly complex database-style behavior and extreme reliability required to provide messaging transactions has been completely hidden behind a few simple routines. The real trick is making sure that you understand the nature of this powerful concept and how to effectively apply it to your MSMQ applications. In this section, we’ll examine several types of transactions and look at a number of programming techniques that you can use to apply them.

Transactions are atomic operations in which no one part of the operation can succeed unless all parts of the operation succeed. A successful transaction is committed, and any changes it has made to data stores become permanent. Unsuccessful transactions are rolled back so that all data stores are returned to their state prior to the transaction’s inception. This transactional approach to data modification helps developers guarantee that data stores maintain a consistent state. This means that there are no surprises. If the account balance database can never have negative values unless the credit database has a corresponding approved record, we must make sure that only legal combinations prevail. Transactions allow multiple changes like this to be treated atomically.

Transactions are generally committed through a two-phase process. In the first phase, each of the participants votes to commit or abort the transaction. If any participant votes to abort the transaction, the transaction is rolled back and the states of all data stores involved are returned to their pretransaction form. If all participants vote to commit the transaction, the transaction is committed. This does not mean that the operations are completed, it just means that the participants are committed to completing their parts of the transaction.

### Messaging Transactions

Messages can be sent and received within a transaction. It is important to note that the messages sent will not actually become available until the transaction is committed. This means that you can never send and then receive the same message within a transaction.

Messages sent within a transaction are guaranteed to be delivered only once. Messages will also be delivered in the order that they were sent within a transaction. This order guarantee is only valid when the messages are sent to the same queue within the same transaction.

Transactional Receive operations can only take place against local queues. Furthermore, transactional Receive calls must be synchronous, thus NULLs should be supplied for the lpOverlapped and fnReceiveCallback parameters when calling MQReceiveMessage().

Both API and ActiveX component flavors of MSMQ development support complete transaction behavior. MSMQ transaction behavior is accessed through the ITransaction interface. API developers need to include the transact.h header before the mq.h header to gain proper declarations for the ITransaction interface. API developers can get an interface pointer to a local MSMQ transaction object by calling MQGetTransaction().

Developers guarantee application consistency by defining transactions within their applications. A set of MSMQ operations are grouped within a transaction by making a call to begin a transaction before any critical operations take place. When all the aspects of the transaction have returned successfully, the application calls a routine to commit the transaction. MSMQ transactions are started by calling MQBeginTransaction() or the BeginTransaction() method of either the IMSMQCoordinatedTransactionDispenser or
