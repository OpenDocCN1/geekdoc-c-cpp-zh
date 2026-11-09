```
```c
QUEUEPROPID aPropId[1];                   //Property id array
aPropId[0] = PROPID_Q_PATHNAME;
aVariant[0].vt = VT_LPWSTR;
aVariant[0].pwszVal = L".\\BasicQueue";

//Set up the property struct
MQQUEUEPROPS QueueProps;                  //Queue properties struct
QueueProps.cProp = 1;                     //Number of properties
QueueProps.aPropID = aPropId;             //Properties id array
QueueProps.aPropVar = aVariant;           //Properties value array
QueueProps.aStatus = NULL;                //No error reports
```
```

# ### Creating a Queue

The next step is to call the MQCreateQueue() library routine with the initialized MQQUEUEPROPS structure to create the queue. The MQCreateQueue() call can optionally return the format name assigned to the newly created queue. Much like other COM+ services, all characters passed through the MSMQ API are stored in Unicode format. This simple application uses Unicode characters internally, so all our library routine calls will be wide versions as well. The format name buffer should be at least 44 Unicode characters for public queues and at least 54 Unicode characters for private queues. If an undersized buffer is presented, the MQCreateQueue() call will return MQ_INFORMATION_FORMATNAME_BUFFER_TOO_SMALL (recently awarded grand prize for the world's longest symbol), placing the required buffer size in the dwFormatNameLen parameter (if you provide one).

```
```c
//Create queue
HRESULT hr;                               //Return status
WCHAR wcsFormatName[64];                  //Queue format name
DWORD dwFormatNameLen = 64;               //Format name size
hr = MQCreateQueue( NULL,                  //Security descriptor
                    &QueueProps,          //Queue properties
                    wcsFormatName,        //Receive buffer
                    &dwFormatNameLen );   //Size of buffer
```
```

# ### Destroying a Queue

Next, take a look at the destroy side. All you need to destroy a queue is the format name and the permission to do so. The trick here is how to get the format name. As discussed earlier, you can discover the queue format name by passing the queue pathname to the MSMQ MQPathNameToFormatName() library call:

```
```c
//Get the format name of the queue using the pathname
HRESULT hr;                               //Return status
WCHAR wcsFormatName[64];                  //Queue format name
DWORD dwFormatNameLen = 64;               //Format name size
hr = MQPathNameToFormatName(
        L".\\BasicQueue",
        wcsFormatName,
        &dwFormatNameLen );
```
```