We then create a URL that points to the Documents folder inside the container, and finally a URL that points to our file inside the Documents folder. Remember, all the files inside the iCloud container’s Documents folders are shown as individual files. The user can manage these files inside the Settings app (iCloud > Storage & Backup > Manage Storage). They can see the file’s name and the file size, and they can delete individual files if they wish.

Anything saved directly into the container (not in the Documents folder) is hidden. The user can only see the total memory usage and must delete all the data at once.

In our case, it doesn’t make a huge difference. We will only ever have a single data file. However, it’s usually best to save documents into the Documents folder.

Finally, this method will return nil if iCloud support is disabled.

> **NOTE:** We will only use the cloudURL to move documents into iCloud storage. Never use it to access iCloud files directly. After all, even if we know the file’s in the cloud, it might not have downloaded to this particular device. Furthermore, other processes may move the file, changing its URL. Therefore, when opening files from within iCloud, we must always use NSMetadataQuery to search for the document’s current location.

```
```objective-c
+ (BOOL)isCloudAvailable {
    return [self cloudURL] != nil;
}
```
```

Finally, isCloudAvailable simply calls cloudURL and checks to see if it returns nil. If it did, iCloud support is not available and this method returns NO. Otherwise, this method returns YES.

Now let’s create our accessWeightHistory: convenience method. Open WeightHistory.h and declare the method as shown:

```
```objective-c
+ (void)accessWeightHistory:(historyAccessHandler)completionHandler;
```
```

We also need to define the historyAccessHandler type. This will be a callback block that takes two arguments: a BOOL value indicating the access operation’s success or failure, and a WeightHistory object. We’re going to create a number of

![](bbox=[0.743, 0.522, 1.0, 0.661])