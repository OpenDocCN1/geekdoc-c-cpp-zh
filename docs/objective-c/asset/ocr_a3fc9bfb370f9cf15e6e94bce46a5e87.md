when assigning it to the passed in variable, you dereference the variable by using the dereference operator (*). So, in other words, to create and assign a new NSError object to the passed in NSError indirect reference, you do something like Listing 10.8.

# Listing 10.8

# Assigning an NSError object to the passed in NSError indirect reference

```
*outError = [NSError errorWithDomain:@"FileWrapper"
    code:404
    userInfo:errorInfo];
```

The NSError factory method takes three parameters. The first is the error domain. This is a string value used to indicate the subsystem from which the error has originated. Cocoa provides several error domains itself, such as NSCocoaErrorDomain, NSPOSIXErrorDomain, and so on. These are declared in the NSError.h header file. You can, and probably should, specify your own error domain when creating your own instances of NSError. If you choose to do so, the error domain string should be specified in reverse DNS notation, for example, com.yourcompanyname.productname.classname.

The second parameter is the error code parameter. The error code is entirely application specific, and provides a means for you to specify a traditional error code as part of your error object. How you choose to use the error code is up to you, but it must be an unsigned integer.

# Understanding the NSError userInfo Dictionary

For the most part, the error code and the error domain are legacy parameters that are mostly unused today. The real juice in the NSError object is in the userInfo dictionary. When creating the dictionary for this parameter, you can use several keys for different error information. The keys are shown in Table 10.1.

Not all of these keys will always exist, and furthermore, users of the NSError class may add special domain-specific keys to the dictionary as well for the purposes of encoding data specific to the error that has occurred.

The ability to encode all the information required for displaying an error message to the user, the description, the error reason, a suggestion for how to recover, and even the buttons for the dialog box, make it possible to even use the NSAlert class method +alertWithError: to display an appropriate alert box with the appropriate buttons and text fields with the data from the NSError object.