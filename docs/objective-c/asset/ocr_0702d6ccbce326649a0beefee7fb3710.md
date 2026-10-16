This occurrence is rare, but it’s important to know that you have this tool available to you if needed. By adding the @protocol Foo directive above the Bar protocol declaration, you are telling the compiler “Trust me, Foo is a protocol, and I’ll include it in my compilation, but I’m not importing the Foo.h here.”

# Exploring examples of protocol use

Protocols are used throughout Objective-C when working with application frameworks, such as Cocoa and Cocoa Touch. The biggest area of use is in delegation and datasource objects. Often, these are cases where the delegating object requires information at runtime that can’t be determined in a generic way, such as what columns to display in a given table view. Alternatively, they’re also used in cases where some process needs to happen in the background. You might call a method like -start, which returns immediately, and then receive a callback on a delegate protocol method telling you that the process has completed.

Just to give you an example of this in action, take a look at Listing 7.11. In this code, the application is creating an NSURLConnection, and firing it off. Later, as the data comes back from the URL request, it receives notice of that data via the protocol method -connection:didReceiveData:.

Listing 7.11

# A class using an NSURLConnection and implementing the NSURLConnection delegate protocol methods

```
@implementation NetworkConnector
-(id)init
{
    if(self = [super init])
    {
        NSURL *url = [NSURL URLWithString:@"http://www.google.com"];
        NSURLRequest *req = [NSURLRequest requestWithURL:url];

        connection = [[NSURLConnection alloc] initWithRequest:req
            delegate:self startImmediately:YES];
    }
    return self;
}
// protocol methods
(void)connection:(NSURLConnection *)connection
    didReceiveData:(NSData *)inData
{
```