# Implementing manual notifications

All of these notifications happen automatically. All you need to do is use KVC compliant accessors for your properties and everything will work fine. Sometimes, you don’t necessarily want to take advantage of the automatic notifications. Where you want to instead manually send notifications that you’ve just changed a value or set of values. For example, if you are about to make many changes at once, you may want to group up the notification and only send one notification. In these cases, you want to use manual notifications.

To use manual notifications, you must first override the class method +automaticallyNotifiesObserversForKey: to tell Objective-C that you do not want it to automatically notify observers of changes. You do this by returning NO for any keys for which you want to implement manual notification. An example of this is shown in Listing 6.17.

# Listing 6.17

# Overriding +automaticallyNotifiesObserversForKey:

```
+(BOOL)automaticallyNotifiesObserversForKey:(NSString *)inKey;
{
    if([inKey isEqualToString:@"memberVariable"])
        return NO;
    return YES;
}
```

When you actually want to perform a manual notification for change, you must call the method -willChangeValueForKey: prior to the change and then -didChangeValueForKey: after. An example of this is shown in Listing 6.18.

# Listing 6.18

# Implementing manual notifications

```
-(void)setMemberVariable:(CGFloat)inValue;
{
    [self willChangeValueForKey:@"memberVariable"];
    memberVariable = inValue;
    [self didChangeValueForKey:@"memberVariable"];
}
```