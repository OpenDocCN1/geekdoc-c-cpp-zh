# LISTING 24.3  Continued

```
QUEUEHANDLE hQueue;                 //Handle to queue
hr = MQOpenQueue( wcsFormatName,       //Queue format name
                  MQ_RECEIVE_ACCESS,   //Access requested
                  MQ_DENY_NONE,        //Share mode
                  &hQueue);            //Queue handle

//Check results
if ( FAILED(hr) )
{
    wprintf(L"Error opening queue: %x\n\n",hr);
    return;
}

//Allocate message property objects
MQMSGPROPS MsgProps;                  //Message properties struct
MSGPROPID aMsgPropId[4];              //Message property id array
PROPVARIANT aMsgPropVar[4];           //Message property value array

//Set up message label and length
WCHAR wcsLabel[MSGLABELSIZE];          //Message label buffer
aMsgPropId[0] = PROPID_M_LABEL;
aMsgPropVar[0].vt = VT_LPWSTR;
aMsgPropVar[0].pwszVal = wcsLabel;
aMsgPropId[1] = PROPID_M_LABEL_LEN;
aMsgPropVar[1].vt = VT_UI4;
aMsgPropVar[1].ulVal = MSGLABELSIZE;

//Set up message body and length
WCHAR wcsBody[MSGBODYSIZE];            //Message body buffer
aMsgPropId[2] = PROPID_M_BODY;
aMsgPropVar[2].vt = VT_VECTOR | VT_UI1;
aMsgPropVar[2].caub.pElems = (LPBYTE)wcsBody;
aMsgPropVar[2].caub.cElems = MSGBODYSIZE * sizeof(WCHAR);
aMsgPropId[3] = PROPID_M_BODY_SIZE;
aMsgPropVar[3].vt = VT_UI4;
aMsgPropVar[3].ulVal = MSGBODYSIZE;

//Set up message property struct
MsgProps.cProp = 4;                   //Number of properties
MsgProps.aPropID = aMsgPropId;        //IDs of properties
MsgProps.aPropVar = aMsgPropVar;      //Values of properties
MsgProps.aStatus = NULL;              //No error reports

//Get first message
hr = MQReceiveMessage(    hQueue,      //Queue to receive from
                          0,           //Timeout
                          MQ_ACTION_RECEIVE, //Receive or peek
                          &MsgProps,   //Message properties
                          NULL,        //Overlapped structure
```