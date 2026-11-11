With the schema registered, we need to now register our client. Here we grab a reference to the `ClientDescription.plist` that we created previously and pass it to the ISyncManager along with our unique identifier. This will register our client and return a reference to our ISyncClient object. Now that our client is registered, we need to turn on syncing with all of the other client types. This allows us to decide which syncs we want to be involved in. Again, since we are the originator of the data, we want to be involved in every sync.

```
```objective-c
[client setShouldSynchronize:YES
              withClientsOfType:ISyncClientTypeApplication];
[client setShouldSynchronize:YES
              withClientsOfType:ISyncClientTypeDevice];
[client setShouldSynchronize:YES
              withClientsOfType:ISyncClientTypeServer];
[client setShouldSynchronize:YES
              withClientsOfType:ISyncClientTypePeer];
```
```

The last step in this method is to capture and handle any exceptions that we receive. As of the writing of this book, there are still a few exceptions that this process can throw, so we want to be sure to capture those, wrap them up in an NSError, and hand them back to our caller. Assuming nothing has blown up on us, we return the ISyncClient.

```
```objective-c
} @catch (NSException *exception) {
    dict = [NSDictionary dictionaryWithObject:[exception reason]
                         forKey:NSLocalizedDescriptionKey];
    *error = [NSError errorWithDomain:@"PragProg"
                                  code:8002
                              userInfo:dict];
    return nil;
}
return client;
}
```
```

# Performing a Sync

Now that we have registered our schema and our sync client, we need to be able to handle the two ways sync can occur. We can either initiate the sync or receive a notification that a sync is about to occur. Fortunately, we handle both of these situations in the same manner.

2. Where they belong anyway.