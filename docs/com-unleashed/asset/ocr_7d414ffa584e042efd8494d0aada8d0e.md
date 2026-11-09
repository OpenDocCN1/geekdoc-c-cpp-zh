Visual Basic code to receive notification of this event's firing. However, that demo dealt only with persistent subscriptions. We will look at how you would perform the task of registering and unregistering transient subscriptions. One thing to also keep in mind is that whether you register either a persistent or transient subscription, the act of firing the event and handling the event works in exactly the same way. In other words, the publisher and the subscriber should be abstracted from this knowledge.

# Registering Transient Subscriptions

The first thing you'll need to see is how to register a transient subscription with the Event Service because this task cannot be done via Component Services. To do this, simply perform the following steps:

+   1. Create an instance of a COMAdminCatalog object.
+   2. Use the `ICOMAdminCatalog::GetCollection` interface in order to retrieve a collection of COM+ catalog's transient subscriptions.
+   3. Use `ICatalogCollection::Add` to add a new transient subscription.
+   4. Use `ICatalogObject::pub_Value` to assign the values discussed in the previous section regarding subscription properties.
+   5. Finally, save the subscription to the COM+ catalog using the `ICatalogCollection::SaveChanges` method.

Now, take a look at a bit of Visual C++ code (shown in Listing 26.2) to see exactly how this would work. This code (as well as a Visual Basic equivalent) can also be located on the book's CD-ROM in folders named TransientSubscriptionVC and TransientSubscriptionVB, respectively.

# **LISTING 26.2**  Registering a Transient Subscription in Visual C++

```
HRESULT hr;
ICOMAdminCatalog* pAdminCatalog;

// retrieve the COM+ catalog object
hr = ::CoCreateInstance(CLSID_COMAdminCatalog, NULL,
                        CLSCTX_SERVER,
                        IID_ICOMAdminCatalog,
                        (void**)&pAdminCatalog);

if (SUCCEEDED(hr))
{
    ICatalogCollection* pCatalogCollection;

    // allocate bstr for catalog name
    BSTR bstrCatalogName = ::SysAllocString(L"TransientSubscriptions");
```