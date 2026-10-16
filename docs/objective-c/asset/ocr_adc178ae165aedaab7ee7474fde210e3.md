After you register as an observer, if you passed the flag NSKeyValueObservingOption Initial, you can get an initial notification of the initial value for the attribute that you’re observing. Additionally, as the value changes over time, you receive notifications of those changes.

In order to receive those notifications, you have to implement the callback method shown in the next section.

# Defining callbacks for KVO

The next step in using KVO is in writing the callback method for the Observer. Listing 6.15 shows an example implementation of the method -observeValue:forKeyPath:ofObject:change:context:.

# Listing 6.15

# An example implementation of the KVO callback method.

```
-(void)observeValueForKeyPath:(NSString *)inKeyPath
    ofObject:(id)inObject
    change:(NSDictionary *)inChange
    context:(void *)inCtx;
{
    if([inKeyPath isEqualToString:@"memberVariable"])
    {
        NSString *newValue = [inChange
            objectForKey:NSKeyValueChangeNewKey];
        // do something with the new value...
    }
    else if([inKeyPath isEqualToString:@"..."]) // etc...
    {
    }
    [super observeValueForKeyPath:inKeyPath
        ofObject:inObject
        change:inChange
        context:inCtx];
}
```