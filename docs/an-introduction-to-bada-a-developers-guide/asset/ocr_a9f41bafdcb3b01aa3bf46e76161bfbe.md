To purchase the item, you can use following code snippet:

```
pPurchaseService = new PruchaseService();
pPurchaseService->Construct(pPurchaseServiceListener);
result r;
RequestId reqId = INVALID_REQUEST_ID;
String itemGroupId(L"1000000000a7");
String purchaseItemId(L"00000000517");
r = pPurchaseService->PurchaseItem(itemGroupId, purchaseItemId, reqId);
```

# 5.3.5 Component Setup

We explained how to set up the sale items on the Samsung Apps Seller Office when you are using the commerce service. There are other services that require you to set up the component via the bada developer site (developer.bada.com). The most common is the remote content management service. Before you actually start to write your code, you have to set up the Amazon S3 workspace for your application.

# Step 1: Set Basic Application Information

This is the first step when you generate a new application. As part of this step you need to give your application a name, a simple description, and provide version information. Figure 5.7 is a screenshot of Step 1 from the developer web site.

![](bbox=[0.28, 0.79, 0.78, 0.88])

Figure 5.7 Create application profile.

Once you have completed the required information, the Application Manager will lead you to the next step when you click the Next button.