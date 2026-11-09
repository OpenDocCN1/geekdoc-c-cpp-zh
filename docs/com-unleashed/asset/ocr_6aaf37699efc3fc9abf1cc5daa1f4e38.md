# LISTING 25.2 Continued

```
```cpp
//Empty the output string and read buffer
WCHAR wcsBuffer[WORKINGBUFFERSIZE] = L"";
*pstrOrderLabels = NULL;

//Setup queue information using a smart pointer
IMSMQQueueInfoPtr pQInfo("MSMQ.MSMQQueueInfo");
pQInfo->put_PathName(MSMQQUEUEPATHNAME);

//Open the queue
IMSMQQueuePtr pQueue =
        pQInfo->Open( MQ_PEEK_ACCESS, MQ_DENY_NONE);

//Peek at the first message
IMSMQMessagePtr pMsg("MSMQ.MSMQMessage");
VARIANT vtTimeout;
vtTimeout.vt = VT_I4;
vtTimeout.lVal = 0;
VARIANT vtWantBody;
vtWantBody.vt = VT_BOOL;
vtWantBody.boolVal = false;
pMsg = pQueue->PeekCurrent(&vtTimeout,&vtMissing,&vtWantBody);

//Return pending if queue is empty
if (NULL == pMsg)
    return E_PENDING;

//Add label to output string
wcscpy( wcsBuffer, pMsg->GetLabel() );
wcscat( wcsBuffer, L"\n" );

//Loop through all messages
while ( pMsg =
        pQueue->PeekNext(&vtTimeout,&vtMissing,&vtWantBody) )
{
    //Add label to output string
    if ( (wcslen(wcsBuffer)+wcslen(pMsg->GetLabel()) + 2) >
                                      WORKINGBUFFERSIZE )
        return E_OUTOFMEMORY;
    wcscat( wcsBuffer, pMsg->GetLabel() );
    wcscat( wcsBuffer, L"\n" );
}

//Return label list to user
*pstrOrderLabels = SysAllocString( wcsBuffer );

}
catch (_com_error &e)
{
    return e.Error();
}

//Return success
return S_OK;
}
```
```