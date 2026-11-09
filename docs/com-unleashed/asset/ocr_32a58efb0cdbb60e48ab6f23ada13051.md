# LISTING 24.3 Continued

```
```c
case '3':
    ReceiveMessage();
    break;

case '4':
    DestroyQueue();
    break;

default:
    wprintf(L"Bad choice.\\n\\n");
    break;

} while ( iChoice != '0' );

//Return success
return 0;
}

void CreateQueue()
{
    //Set up properties (we only need the path name property)
    PROPVARIANT aVariant[1];                 //Property value array
    QUEUEPROPID aPropId[1];                  //Property id array
    aPropId[0] = PROPID_Q_PATHNAME;
    aVariant[0].vt = VT_LPWSTR;
    aVariant[0].pwszVal = QUEUEPATHNAME;

    //Set up the property struct
    MQQUEUEPROPS QueueProps;                 //Queue properties struct
    QueueProps.cProp = 1;                    //Number of properties
    QueueProps.aPropID = aPropId;            //Properties id array
    QueueProps.aPropVar = aVariant;          //Properties value array
    QueueProps.aStatus = NULL;               //No error reports

    //Create queue
    HRESULT hr;                              //Return status
    WCHAR wcsFormatName[FORMATNAMESIZE];     //Queue format name
    DWORD dwFormatNameLen = FORMATNAMESIZE;  //Size of format name
    hr = MQCreateQueue( NULL,                //Security descriptor
                        &QueueProps,         //Queue properties
                        wcsFormatName,       //Format name buffer
                        &dwFormatNameLen );  //Format name buffer size

    //Check results
    if ( FAILED(hr) )
        wprintf(L"Error creating queue: %x\\n\\n",hr);
    else
        wprintf(L"Queue created with format name: %s\\n\\n",wcsFormatName);
}
```
```