# Listing 24.3 Continued

```
```c
void SendMessage()
{
    //Get the format name of the queue using the pathname       //Return status
    HRESULT hr;
    WCHAR wcsFormatName[FORMATNAMESIZE];                     //Queue format name
    DWORD dwFormatNameLen = FORMATNAMESIZE;                  //Size of format name
    hr = MQPathNameToFormatName(     QUEUEPATHNAME,
                                     wcsFormatName,
                                     &dwFormatNameLen );

    //Check results
    if ( FAILED(hr) )
    {
        wprintf(L"Error looking up queue format name: %x\\n\\n",hr);
        return;
    }

    //Open the queue with send access
    QUEUEHANDLE hQueue;                                      //Handle to queue
    hr = MQOpenQueue( wcsFormatName,                         //Queue format name
                      MQ_SEND_ACCESS,                       //Access requested
                      MQ_DENY_NONE,                          //Share mode
                      &hQueue);                              //Queue handle

    //Check results
    if ( FAILED(hr) )
    {
        wprintf(L"Error opening queue: %x\\n\\n",hr);
        return;
    }

    //Allocate message property objects
    MQMSGPROPS MsgProps;                                     //Message properties struct
    MSGPROPID aMsgPropId[3];                                 //Message property id array
    PROPVARIANT aMsgPropVar[3];                             //Message property value array

    //Set up message label
    static int s_cMessageNumber = 0;                         //Message label counter
    WCHAR wcsLabel[MSGLABELSIZE];                            //Message label buffer
    swprintf(wcsLabel,L"Message number %d", ++s_cMessageNumber);
    aMsgPropId[0] = PROPID_M_LABEL;
    aMsgPropVar[0].vt = VT_LPWSTR;
    aMsgPropVar[0].pwszVal = wcsLabel;

    //Set up message body
    WCHAR wcsBuf[MSGBODYSIZE];
    wprintf(L"Enter message body: ");
    _getws(wcsBuf);
```
```