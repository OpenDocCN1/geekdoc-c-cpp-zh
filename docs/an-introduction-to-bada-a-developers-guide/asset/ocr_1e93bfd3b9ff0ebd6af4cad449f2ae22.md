```
{
    IEnumarator *pEnum;
    pEnum = pNeighborPeerInfo->GetEnumeratorN();
    while (pEnum->MoveNext() == E_SUCCESS)
    {
        pAdhocPeerInfo = (AdhocPeerInfo*) pEnum->GetCurrent();
        name = pAdhocPeerInfo->GetName();
        pAddr = pAdhocPeerInfo->GetAddress();
        String ip = pAddr->ToString();
    }
    pAdhocService->SendBroadcastMessage("Hello All");
    delete pNeighborPeerInfo;
    delete pEnum;
}
```

7. Once your ad hoc service is started you can broadcast a message to all the peers by calling SendBroadcastMessage().

```
void
MyWiFiClass::SendBroadcastMessage(String msg)
{
    pAdhocService->SendBroadcastMessage(msg);
}
```

8. You can also send a dedicated message to any of your peers by calling SendUnicastMessage().

```
void
MyWiFiClass::SendMessageToPeer(String peerName, String message)
{
    pAdhocService-> SendUnicastMessage(peerName, message);
}
```

9. Once you are done with the ad hoc service call StopService().

```
void
MyWiFiClass:: void StopService()
{
    if (pAdhocService)
    {
        pAdhocService->StopAdhocService();
        delete pAdhocService;
    }
}
```