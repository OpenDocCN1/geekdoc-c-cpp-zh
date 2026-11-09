MSMQ machines maintain a machine journal. Individual messages can be configured as journal messages through the Message Journal property. MSMQ machines supply a Dead Letter and a Transaction Dead Letter queue for storing messages that cannot be delivered. Transactional messages are always copied to the Transaction Dead Letter queue when delivery fails. Nontransactional messages must have the MQMSG_DEADLETTER flag set in their Journal property in order to be copied to the normal Dead Letter queue. Regardless, MSMQ ensures that there is never more than one copy of any message on a given machine at a time. Table 25.3 shows the Message Journal property values.

**Table 25.3 — Message Journal Property Values**

| Property Value | Description |
|---|---|
| `MQMSG_DEADLETTER` | If the message is not delivered to the receiving application within a timeout period (either *time-to-be-received* or *time-to-reach-queue*), the message is sent to a Dead Letter queue on the computer where the message is located. |
| `MQMSG_JOURNAL` | If the message is transmitted, keep it in the machine journal on the originating machine. |
| `MQMSG_JOURNAL_NONE` | The message is not kept in the originating computer's machine journal. |

# Transactions

OK, here’s the heavy stuff. If you’ve ever rolled your own transactional software, you know what I mean when I say, “You don’t want to develop this stuff in house.” Thanks to MSMQ you won’t have to. MSMQ presents a complete set of transaction services that can be easily integrated into any project, especially projects making heavy use of COM+. The highly complex database-style behavior and extreme reliability required to provide messaging transactions has been completely hidden behind a few simple routines. The real trick is making sure that you understand the nature of this powerful concept and how to effectively apply it to your MSMQ applications. In this section, we’ll examine several types of transactions and look at a number of programming techniques that you can use to apply them.

Transactions are atomic operations in which no one part of the operation can succeed unless all parts of the operation succeed. A successful transaction is committed, and any changes it has made to data stores become permanent. Unsuccessful transactions are