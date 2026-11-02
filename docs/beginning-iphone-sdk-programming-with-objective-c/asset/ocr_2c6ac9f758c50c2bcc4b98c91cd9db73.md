# Invoking Safari

If you want to invoke the Safari Web browser on your iPhone, you can also make use of a URL string and then use the openURL: method of the application instance, like this:

```
```objc
[[UIApplication sharedApplication]
    openURL:[NSURL URLWithString:@"http://www.apple.com"]];
```
```

The preceding code snippet invokes Safari to open the www.apple.com page (see Figure 16-3).

![](bbox=[0.78, 0.12, 0.95, 0.5])

# Invoking the Phone

To make a phone call using the iPhone's dialer, use the following URL string:

```
```objc
[[UIApplication sharedApplication]
    openURL:[NSURL URLWithString:@"tel:1234567890"]];
```
```

The preceding statement invokes the dialer of the iPhone using the phone number specified.

> NOTE Note that the preceding statement works only for iPhone and not iPod Touch because the iPod Touch does not have phone capabilities. Also, you would need to a real device to test this out; the code does not have an effect on the iPhone Simulator. Appendix E discusses how to prepare your iPhone for testing.

# Invoking SMS

You can also use a URL string to send SMS messages using the SMS application:

```
```objc
[[UIApplication sharedApplication]
    openURL:[NSURL URLWithString:
        @"sms:96324065"]];
```
```

The preceding statement invokes the SMS application (see Figure 16-4).

![](bbox=[0.7, 0.7, 0.95, 0.95])