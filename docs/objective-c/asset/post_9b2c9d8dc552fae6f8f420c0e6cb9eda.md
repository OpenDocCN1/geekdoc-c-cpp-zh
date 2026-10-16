
```
}
else
{
    NSDictionary *errorInfo =
        [NSDictionary dictionaryWithObject:@"Unknown error."
                         forKey:NSLocalizedDescriptionKey];

    *outError = [NSError errorWithDomain:@"FileWrapper"
                                    code:501
                                userInfo:errorInfo;
}
return NO;
}
return YES;
}
```

NSError is a formalized design pattern that is being implemented across the Cocoa and Cocoa Touch frameworks.

To use it, you extend your method signature to take an indirect reference to an NSError object. This object is provided by the caller. An indirect reference is essentially a pointer to a pointer. In other words, it’s a pointer that points to another pointer; in this case, it is a pointer to a variable allocated inside the stack of the caller. When you assign something to that variable, you dereference the indirect reference and thus are actually assigning to the variable to which it points.

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_270_0.png)

> **NOTE**
> 
> Some programmers will refer to indirect references as “pointer to a pointer”, “pass by reference”, or “a reference”. I prefer the term “indirect reference” to distinguish it from a plain reference, which you might encounter when using Objective-C++. “Pointer to a pointer” would probably be the most accurate description, but I feel the phrase “pointer to a pointer” is confusing for new programmers.

This concept of an indirect reference probably sounds very confusing. If so, then good, you’re perfectly normal. Fortunately, the underlying details are mostly unimportant as long as you understand the syntax that you have to use when creating and returning the NSError object.

When declaring the NSError indirect reference in your method’s parameter list, you will declare it using the syntax "(NSError **)". The double * signs mark this as an indirect reference.

## Creating an NSError Object

Once inside your method, if an error occurs, before you return NO from the method, you must first create your NSError objects and assign it to the dereferenced NSError indirect reference. To do this, go ahead and create your NSError object just like you would normally, but

when assigning it to the passed in variable, you dereference the variable by using the dereference operator (*). So, in other words, to create and assign a new NSError object to the passed in NSError indirect reference, you do something like Listing 10.8.

### Listing 10.8

### Assigning an NSError object to the passed in NSError indirect reference

```
*outError = [NSError errorWithDomain:@"FileWrapper"
    code:404
    userInfo:errorInfo];
```

The NSError factory method takes three parameters. The first is the error domain. This is a string value used to indicate the subsystem from which the error has originated. Cocoa provides several error domains itself, such as NSCocoaErrorDomain, NSPOSIXErrorDomain, and so on. These are declared in the NSError.h header file. You can, and probably should, specify your own error domain when creating your own instances of NSError. If you choose to do so, the error domain string should be specified in reverse DNS notation, for example, com.yourcompanyname.productname.classname.

The second parameter is the error code parameter. The error code is entirely application specific, and provides a means for you to specify a traditional error code as part of your error object. How you choose to use the error code is up to you, but it must be an unsigned integer.

## Understanding the NSError userInfo Dictionary

For the most part, the error code and the error domain are legacy parameters that are mostly unused today. The real juice in the NSError object is in the userInfo dictionary. When creating the dictionary for this parameter, you can use several keys for different error information. The keys are shown in Table 10.1.

Not all of these keys will always exist, and furthermore, users of the NSError class may add special domain-specific keys to the dictionary as well for the purposes of encoding data specific to the error that has occurred.

The ability to encode all the information required for displaying an error message to the user, the description, the error reason, a suggestion for how to recover, and even the buttons for the dialog box, make it possible to even use the NSAlert class method +alertWithError: to display an appropriate alert box with the appropriate buttons and text fields with the data from the NSError object.

### Table 10.1

| Key | Purpose |
|---|---|
| NSLocalizedDescriptionKey | A localized description of the error condition, such as "File could not be opened because it does not exist." Also accessible via the NSError object method -localizedDescription. |
| NSLocalizedFailureReasonKey | A localized reason for the error, such as "File does not exist." Also accessible via the NSError object method -localizedFailureReason. |
| NSLocalizedRecoverySuggestionErrorKey | A localized description of what the user might do to try to resolve the problem. Also accessible via the NSError method -localizedRecoverySuggestion. |
| NSLocalizedRecoveryOptionsErrorKey | An array of strings to be used for buttons in a dialog box when presenting the error to the user. The first string will be used as the right most button, and then sequentially left from there. |
| NSRecoveryAttemptErrorKey | An object which conforms to the NSErrorRecoveryAttempting protocol, which can be used to attempt to recover from the error. (Mac OS X only) |
| NSUnderlyingErrorKey | Another NSError object representing the actual underlying error. |

## Working with a recovery attempter

The recovery attempter is a little-known and rarely used component of NSError. Available only on Mac OS X, it provides an object that can be used to automatically attempt to recover from the error that has occurred.

The object provided must conform to the NSErrorRecoveryAttempting protocol, which defines two methods, -attemptRecoveryFromError:optionIndex: which is invoked exclusively in applications using a modal, non-document centric user interface, and -attemptRecoveryFromError:optionIndex:delegate:didRecoverSelector:contextInfo: which is invoked by applications with a document-centric user interface.

Recovery attempters work hand-in-hand with the OS X responder chain. To cause the recovery attempter to be used, you call either -presentError: or -presentError:modalForWindow:delegate:didPresentSelector:contextInfo: on any object in the responder chain. These two methods correspond to presenting an error for a modal application in the former case, and a document-based application in the latter case. When you call them, they will present an alert to the user, displaying the information from the NSError. When the user clicks a button, the appropriate recovery attempt method will be called on the recovery attempter, passing the index of the clicked button as the optionIndex parameter.

The -attemptRecoveryFromError:optionIndex: method returns a BOOL value if the error is able to be recovered from. The -presentError:modalForWindow:delegate:didPresentSelector:contextInfo: method is expected to call the selector provided on the delegate object. That selector should take a form similar to Listing 10.9.

### Listing 10.9

### The recovery attempter callback function

```
- (void)didPresentErrorWithRecovery:(BOOL)didRecover
    contextInfo:(void *)contextInfo;
```

Again, recovery attempters are rarely used, and probably not something you’ll typically run into in your code. Nonetheless, it’s an interesting feature of NSError.

## Working with NSError in methods

Returning to the file wrapper example, in order to take advantage of this new NSError code, you’d have to change the main block to look something like Listing 10.10.

### Listing 10.10

### Using a method with NSError

```
int main (int argc, const char * argv[])
{
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];

    FileWrapper *wrapper = [[FileWrapper alloc] init];

    NSError *error = nil;

    if([[wrapper openFileAtPath:@"..." withError:&error]])
    {
        // do stuff with the file here...
    }
    else
    {
        // tell the user the file couldn’t be opened.
        // here you have the error object filled in.
        showErrorToUser(error);
    }

    [pool drain];
    return 0;
}
```
