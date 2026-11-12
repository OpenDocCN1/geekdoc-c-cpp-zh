```
context:nil;

// Register to receive messages when the default units change.
[[NSNotificationCenter defaultCenter]
    addObserver:self
       selector:@selector(reloadTableData)
           name:WeightHistoryChangedDefaultUnitsNotification
         object:self.weightHistory];
}
```

The addObserver:forKeyPath:options:context: method registers our History ViewController as an observer of our weight history. Our controller will receive a notification whenever the list of weight entries changes. Notice that the KVO weightChangeKey actually points to the private weightHistory property (see “The WeightHistory Class” in Chapter 3). We could observe the public weights property, but unfortunately, because it’s a virtual property we only receive a general notification that the array has changed—we don’t get any additional information about the change. When we observe the weightHistory array directly, we get additional information about the type of change and a list of the actual indexes that changed.

In many ways, using the KVOWeightChangeKey really lets us break the WeightHistory class’s encapsulation. In my opinion, this is not necessarily ideal, but by using a public variable for the key, we are essentially blessing this backdoor access. We are promising that we won’t change the underlying implementation without also changing KVOWeightChangeKey to match.

Realistically, however, we should change the WeightHistory code to manually throw the correct KVO notifications for the weights property and just get rid of the backdoor access. However, I wanted to show how to automatically generate KVO notifications using the keyPathsForValuesAffecting<key> method. This has the fortunate side effect of also highlighting some of the limits of this approach.

The addObserver:selector:name:object: method registers our controller to receive WeightHistoryChangedDefaultUnitsNotification messages from our model (and only from our model). When a matching notification is found, the notification center will call our reloadTableData method directly.