```
**LISTING 23.1 Continued**

~~~cpp
//Set up the property struct
MQUEUEPROPS QueueProps;            //Queue properties struct
QueueProps.cProp = 1;              //Number of properties
QueueProps.aPropID = aPropID;      //Properties id array
QueueProps.aPropVar = aVariant;    //Properties value array
QueueProps.aStatus = NULL;         //No prop error reports
~~~
```

As you can see, this extensible structure allows any number of properties to be passed to MSMQ through the same MQUEUEPROPS structure. Variants are used to store property values, enabling many different programming environments to access property settings. There are similar MQMSGPROPS and MQMACHINEPROPS structures for messages and machines (also known as Queue Managers), respectively.

# # Messages

Messages are the raison d'être (reason for being) for everything else that is MSMQ; they represent the atomic units of information that move around an MSMQ enterprise. As it turns out, messages are simply a set of property values. This being the case, messages have a large set of properties to choose from. In general, applications are most interested in the Body property of a message. The Body property is the one property that has a clearly understood function. The Body property can be any size (up to 4MB). Several other message properties will frequently be set and examined by sophisticated applications.

# # Message Properties

Table 23.1 presents a list of the possible MSMQ message properties.

**TABLE 23.1  MSMQ Message Properties**

| Property | Description |
|---|---|
| PROPID_M_ACKNOWLEDGE | Types of acknowledgment messages MSMQ sends |
| PROPID_M_ADMIN_QUEUE | Queue used for acknowledgment messages |
| PROPID_M_ADMIN_QUEUE_LEN | Length of the acknowledgment queue |
| PROPID_M_APPSPECIFIC | Application-generated information such as single integer values or application-defined message classes |
| PROPID_M_ARRIVEDTIME | The maximum amount of time the message has to reach the queue |
| PROPID_M_AUTH_LEVEL | Indicates that the message needs to be authenticated when read |