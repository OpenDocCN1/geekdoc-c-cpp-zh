the appropriate type. You have to make sure that the type used is consistent for a given key. Mixing types can cause difficult-to-find bugs or crashes.

Once you have set a notification, whenever the value is changed using the Set() method, your notification is called. You can add however many notifications you want to each key value—they will all be called whenever the value changes. Notifications can be removed using the RemoveNotification() method:

```
myKVD.RemoveNotification(NotificationFunc, std::str
```

You can get the value for a key manually, if you so wish, with the following call:

```
int myValue;
myKVD.Get<int>(std::string("myInteger"), &myValue);
```

Internally, the primary storage container for the KVD is an STL map. Each map element is indexed by the key string hash, and contains the value encoded as a std::string, a lock, and a std::list of notification callbacks. Each notification callback contains a pointer to the callback function, and the user data value, as illustrated in Figure 24.3.

![](bbox=[0.17, 0.64, 0.58, 0.9])