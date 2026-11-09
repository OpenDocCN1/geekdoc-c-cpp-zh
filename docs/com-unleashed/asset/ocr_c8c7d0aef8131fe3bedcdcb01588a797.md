```
**LISTING 25.3**  Continued

```cpp
SysFreeString(bstrQueueGUID);
SysFreeString(bstrPrivLevel);
SysFreeString(bstrTypeGUID);
    }
}
catch (_com_error &e)
{
    wprintf(L"Error %x, %s\n\n", e.Error(), e.ErrorMessage());
    return;
}
}
```
```

# ## Machine Properties

Just like messages and queues, machines in the MSMQ enterprise have properties. Listing 25.4 demonstrates the MSMQ ActiveX component technique for retrieving a machine’s GUID. The MSMQ API equivalent, `MQGetMachineProperties()`, enables you to retrieve the site ID, connected network list, pathname, and public key of the machine.

```
**LISTING 25.4**  Retrieving Machine Properties

```cpp
void GetMachineId(void)
{
    try
    {
        //Get machine name from user
        WCHAR wcsName[64];
        wprintf(L"Enter the name of the machine to look up: ");
        _getws(wcsName);

        //Look up independent MSMQ client or MSMQ server
        IMSMQApplicationPtr pApp("MSMQ.MSMQApplication");
        BSTR bstrName = SysAllocString(wcsName);
        BSTR bstrId = pApp->MachineIdOfMachineName(wcsName);
        wprintf(L"Machine %s has the Id: %s\n\n", bstrName, bstrId);
        SysFreeString(bstrName);
        SysFreeString(bstrId);
    }
    catch (_com_error &e)
    {
        wprintf(L"Error %x, %s\n\n", e.Error(), e.ErrorMessage());
        return;
    }
}
```
```