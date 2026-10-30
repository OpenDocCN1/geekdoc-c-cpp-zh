```
class ItemServiceListener :
    public Osp::Commerce::Store::IItemServiceListener
{
public:
    ItemServiceListener();
    ~ItemServiceListener();
    void OnItemListReceivedN(RequestId reqId,
        Osp::Base::Collection::IList* pItemInfoList,
        result r, const Osp::Base::String & errorCode,
        const Osp::Base::String &errorString);
};

void
ItemServiceListener::OnItemListReceivedN(RequestId reqId,
    Osp::Base::Collection::IList* pItemInfoList, result r,
    const Osp::Base::String & errorCode, const
    Osp::Base::String &errorString)
{
    if(IsFailed(r))
    {
        //print error message
    }
    else
    {
        //display item information
    }
    if(pItemInfoList != NULL)
    {
        pItemInfoList->RemoveAll(true);
        delete pItemInfoList;
    }
}
```

The PurchaseService class is the class that allows users to purchase items and get purchase information such as the payment history on the device. Following the same pattern as the ItemService class, you have to implement both the IPurchaseServiceListener interface class and PurchaseService class. It is very similar to IItemServiceListener mentioned above. Both classes need to have the companion listener interface class to handle the response and results from the Samsung Apps server.

```
class PurchaseServiceListener :
    public Osp::Commerce::Store::IPurchaseServiceListener
{
public:
    PurchaseServiceListener();
    ~PurchaseServiceListener();
    void OnItemPurchaseCompleted(RequestId reqId,const PaymentId& paymentId, const ItemIds itemId, const String& itemName,
        double price, String& currency, const DateTime& purchaseDate,
        result r, const String& errorCode, const String& errorMsg);
    void OnItemPurchaseInfoReceivedN(RequestId reqId,
        IList* pPurchaseInfoList,result r, const String& errorCode,
        const String& errorMsg);
};
```