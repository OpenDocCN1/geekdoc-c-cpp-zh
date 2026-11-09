# LISTING 25.3  Continued

```
```cpp
BSTR bstrQueueGUID;
pQInfo->get_QueueGuid(&bstrQueueGUID);
BSTR bstrTypeGUID;
pQInfo->get_ServiceTypeGuid(&bstrTypeGUID);

BSTR bstrPrivLevel = NULL;
long lPL = pQInfo->PrivLevel;
switch (lPL)
{
case MQ_PRIV_LEVEL_NONE:
    bstrPrivLevel = SysAllocString(L"Non-encrypted only");
    break;
case MQ_PRIV_LEVEL_BODY:
    bstrPrivLevel = SysAllocString(L"Encrypted only");
    break;
case MQ_PRIV_LEVEL_OPTIONAL:
    bstrPrivLevel =
        SysAllocString(L"Either Non-encrypted or Encrypted");
    break;
default:
    bstrPrivLevel = SysAllocString(L"Unknown");
    break;
}

//Display queue attributes
wprintf(L"Found queue with the following properties:\n");
wprintf(L"Authenticate:\t%\n", pQInfo->Authenticate);
wprintf(L"Base Priority:\t%\n", pQInfo->BasePriority);
wprintf(L"CreateTime:\t% s\n", pQInfo->CreateTime.bstrVal);
wprintf(L"FormatName:\t%s\n", bstrFormatName);
wprintf(L"IsTransactional:\t%\n", pQInfo->IsTransactional);
wprintf(L"IsWorldReadable:\t%\n", pQInfo->IsWorldReadable);
wprintf(L"Journal:\t%ld\n", pQInfo->Journal);
wprintf(L"JournalQuota:\t%ld KB\n", pQInfo->JournalQuota);
wprintf(L"Label:\t%s\n", bstrLabel);
wprintf(L"ModifyTime:\t%s\n", pQInfo->ModifyTime.bstrVal);
wprintf(L"PathName:\t%s\n", bstrPathName);
wprintf(L"PrivacyLevel:\t%s\n", bstrPrivLevel);
wprintf(L"QueueGUID:\t%s\n", bstrQueueGUID);
wprintf(L"Quota:\t%ld KB\n", pQInfo->Quota);
wprintf(L"TypeGUID:\t%s\n", bstrTypeGUID);
wprintf(L"\n");

//Clean up
SysFreeString(bstrFormatName);
SysFreeString(bstrLabel);
SysFreeString(bstrPathName);
```
```