release of our application before we do any migration. That way, when the user opens the first version of our application after “testing” the second version, they get a friendly error message, or you can take it a step further and restore/access the older version of their data.

Download GrokkingRecipes_v2/AppDelegate.m

```
if (![persistentStoreCoordinator addPersistentStoreWithType:NSXMLStoreType
                                              configuration:nil
                                                        URL:url
                                                    options:dict
                                                      error:&error]) {
    NSDictionary *ui = [error userInfo];
    if (ui) {
        NSLog(@"%@:%s %@", [self class], _cmd, [error localizedDescription]);
        for (NSError *suberror in [ui valueForKey:NSDetailedErrorsKey]) {
            NSLog(@"\t%@", [suberror localizedDescription]);
        }
    } else {
        NSLog(@"%@:%s %@", [self class], _cmd, [error localizedDescription]);
    }
    NSAlert *alert = [[NSAlert alloc] init];
    [alert setAlertStyle:NSCriticalAlertStyle];
    [alert setMessageText:@"Unable to load the recipes database."];
    NSString *msgText = nil;
    msgText = [NSString stringWithFormat:@"The recipes database %@\n\n%@\n"
               @"is either corrupt or was created by a newer "
               @"version of Grokking Recipes. Please contact "
               @"support to assist with this error.\n\nError: "
               [error localizedDescription]];
    [alert setInformativeText:msgText];
    [alert addButtonWithTitle:@"Quit"];
    [alert runModal];
    exit(1);
}
```

We have added this code to the -persistentStoreCoordinator method in the application delegate of our first version of the recipes application. In the first version of our application, if an error occurred with the adding of an NSPersistentStore to the NSPersistentStoreCoordinator, we would just present the error to the user via ([NSApplication sharedApplication]) presentError:error). With this change, we give the user a little more useful information as well as dumping quite a bit of useful information to the logs for us to review. We will also keep this code in all future versions of our application to help “future proof” it. Naturally, this is the bare minimum that we can do, and I recommend adding other options. However, the most important point is in place. We do not let the user proceed without a Core Data stack in place. The original way that we