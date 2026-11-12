```
```objectivec
[self.document
    saveToURL:localCoreDataURL
    forSaveOperation:UIDocumentSaveForCreating
    completionHandler:^(BOOL success) {
        [self passDocumentToSubViewControllers];
    }];
}
}
```
```

Finally, if the file exists, we open it. Otherwise, we create a new file by calling saveToURL:forSaveOperation:completionHandler:. In both cases, we call passDocumentToSubViewControllers in the completion handler to pass our document along to our other view controllers.

Note that, before creating a new document, we clear out the container. We need this code to work around a fairly serious problem.

Turns out, if the user goes into their iCloud settings and deletes this document, it will automatically revert to a local document. The devices won't sync their updates to iCloud ever again. However, we still have our transaction logs in the iCloud container. If the user removes the app from the device, then reinstalls it, it will go into an invalid state. The app will try to load the transaction data but won't be able to, and the document will fail to open. By clearing the container before we create a new document, we prevent this problem.

> > **NOTE:** Alternatively, we can use `NSMetadataQuery` to confirm the document's presence in the cloud. If the document isn't found, we clear the iCloud storage and ask the user if they want upload it again. Additionally, the `UIManagedDocument` creates a directory for our logs. `NSMetadataQuery` cannot search for directories. Instead, we search for the package's `DocumentMetadata.plist` file.

![](bbox=[0.0, 0.679, 0.242, 0.814])