
These objects exist within an administration unit defined as an MSMQ Enterprise. Messages are objects that carry information throughout the enterprise. Messages have a flexible structure and can contain some data or nothing at all; in the latter case, the receipt of such an empty message might be all the communication required between two applications. On the other hand, messages can include up to 4MB of data. Queues act as the destination for all messages in an MSMQ enterprise. Messages are sent to queues, not to applications. The intermediary nature of queues provides a layer of independence between peers involved in a messaging scenario, thus supporting loosely coupled application development. MSMQ machines are in a process known as the Queue Manager. MSMQ machines are the computer systems designated to supply certain queuing services within the MSMQ enterprise.

All these objects are described by properties, such as labels, types, sizes, timeouts, and priorities. Variable-length property lists allow developers to work with unspecified objects in a generic way. Some applications might require objects with tons of properties, and other applications might require no property information at all. Some object properties are set by MSMQ, others can be set by MSMQ administrators, and still others can be set only procedurally. Some properties can be written to only when creating the object in question, and persist as read-only attributes thereafter.

The MSMQ Explorer enables administrators to create objects and manage object properties throughout the MSMQ enterprise. The MSMQ Explorer runs as a standalone application in early versions of MSMQ and as a Microsoft Management Console (MMC) based snap-in in more recent releases.

When assigned procedurally, properties are configured through variable-length property arrays. This allows new properties to be defined by MSMQ over time and enables a flexible programming interface. MSMQ uses this model extensively, as does OLE DB and other modern COM systems. All the basic MSMQ objects described previously support any number of properties. With the exception of a few mandatory properties that might be required in certain circumstances, the properties you set and get will be defined by the needs of your application. Listing 23.1 shows how you would procedurally configure a queue property structure with one property.

**LISTING 23.1  Procedurally Configuring a Queue Property**

```cpp
//Set up properties (we only need the path name property)
QUEUEPROPID aPropID[1];                 //Property ID array
PROPVARIANT aVariant[1];                //Property value array
aPropID[0] = PROPID_Q_PATHNAME;         //Set the ID
aVariant[0].vt = VT_LPWSTR;             //Set the value type
aVariant[0].pwszVal = L"Srv1\\Orders*"; //Set the value data

//Set up the property struct
MQUEUEPROPS QueueProps;            //Queue properties struct
QueueProps.cProp = 1;              //Number of properties
QueueProps.aPropID = aPropID;      //Property ID array
QueueProps.aPropVar = aVariant;    //Property value array
QueueProps.aStatus = NULL;         //No prop error reports
```

As you can see, this extensible structure allows any number of properties to be passed to MSMQ through the same MQUEUEPROPS structure. Variants are used to store property values, enabling many different programming environments to access property settings. There are similar MQMSGPROPS and MQMACHINEPROPS structures for messages and machines (also known as Queue Managers), respectively.

## Messages

Messages are the raison d'être (reason for being) for everything else that is MSMQ; they represent the atomic units of information that move around an MSMQ enterprise. As it turns out, messages are simply a set of property values. This being the case, messages have a large set of properties to choose from. In general, applications are most interested in the Body property of a message. The Body property is the one property that has a clearly understood function. The Body property can be any size (up to 4MB). Several other message properties will frequently be set and examined by sophisticated applications.

### Message Properties

Table 23.1 presents a list of the possible MSMQ message properties.

**TABLE 23.1  MSMQ Message Properties**

| Property | Description |
|---|---|
| `PROPID_M_ACKNOWLEDGE` | Types of acknowledgment messages MSMQ sends |
| `PROPID_M_ADMIN_QUEUE` | Queue used for acknowledgment messages |
| `PROPID_M_ADMIN_QUEUE_LEN` | Length of the acknowledgment queue |
| `PROPID_M_APPSPECIFIC` | Application-generated information such as single integer values or application-defined message classes |
| `PROPID_M_ARRIVEDTIME` | The time the message arrived at the queue |
| `PROPID_M_AUTH_LEVEL` | Indicates that the message needs to be authenticated when read |
| `PROPID_M_AUTHENTICATED` | Indicates that the message was authenticated by MSMQ |
| `PROPID_M_BODY` | The body of the message |
| `PROPID_M_BODY_SIZE` | The size of the message body |
| `PROPID_M_BODY_TYPE` | The type of message body (string, array of bytes, or object) |
| `PROPID_M_CLASS` | The type of message (for example, a message can be a normal, acknowledgment, or report message) |
| `PROPID_M_CONNECTOR_TYPE` | Indicates that some message properties were generated external to MSMQ |
| `PROPID_M_CORRELATIONID` | The correlation identifier of the original message ID |
| `PROPID_M_DELIVERY` | How the message is delivered (optimize throughput or recoverability) |
| `PROPID_M_DEST_QUEUE` | The queue where the message will reside (where the message is sent) |
| `PROPID_M_DEST_QUEUE_LEN` | The length of the destination queue |
| `PROPID_M_DEST_SYMM_KEY` | The symmetric key required when sending encrypted messages to foreign queues |
| `PROPID_M_DEST_SYMM_KEY_LEN` | The length of the symmetric key |
| `PROPID_M_ENCRYPTION_ALG` | The algorithm used to encrypt the message body |
| `PROPID_M_EXTENSION` | Additional unformatted information |
| `PROPID_M_EXTENSION_LEN` | The length of the unformatted information |
| `PROPID_M_HASH_ALG` | The hash algorithm used when authenticating messages |
| `PROPID_M_JOURNAL` | Indicates that a copy of the message is stored in the machine journal |
| `PROPID_M_LABEL` | Application-defined label for the message |
| `PROPID_M_LABEL_LEN` | The length of the message label |
| `PROPID_M_MSGID` | The MSMQ-generated identifier |
| `PROPID_M_PRIORITY` | The priority of the message |
| `PROPID_M_PRIV_LEVEL` | Indicates that the message is encrypted |
| `PROPID_M_PROV_NAME` | The name of the cryptographic provider |
| `PROPID_M_PROV_NAME_LEN` | The length of the cryptographic provider name |
| `PROPID_M_PROV_TYPE` | The type of cryptographic provider |
| `PROPID_M_RESP_QUEUE` | The queue for sending responses to the message |
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

## Queues

Message queues are the buffering mechanism that makes MSMQ an effective tool for developing loosely coupled applications. Queues store a message until an appropriate application sees fit to retrieve the message. Queues make it possible for various components to communicate, even though they execute at different times and at various locations within an enterprise.
