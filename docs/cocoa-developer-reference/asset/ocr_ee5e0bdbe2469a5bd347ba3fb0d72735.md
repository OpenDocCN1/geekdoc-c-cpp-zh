A simple text parser is listed below. It takes the same return string as an input and extracts data from two fields: `status_txt` and `url`.

```
```objc
if (returnURLString != nil) {
    returnXML.stringValue = returnURLString;
    statusRange = [returnURLString rangeOfString: @"<status_txt>"];
    thisRange.location = statusRange.location+12;
    thisRange.length = 2;
    thisString = [returnURLString substringWithRange:thisRange];
    if ([thisString isEqualToString: @"OK"]) {
        NSLog(@"Status OK");
        urlStartRange = [returnURLString rangeOfString: @"<url>"];
        urlEndRange = [returnURLString rangeOfString: @"</url>"];
        thisRange.location = urlStartRange.location+5;
        thisRange.length = urlEndRange.location -
        urlStartRange.location - 5;
        bitlyURL.stringValue = [returnURLString
        substringWithRange:thisRange];
    }
    else
        bitlyURL.stringValue = @"Error";
}
```
```

This code uses the `rangeOfString:` method to find the range — index and length — of a target string. First, the code looks for `<status_txt>` to find the starting index of the status string. It copies exactly two characters from that index into a new string using the `substringWithRange:` method and checks whether this short new string is equal to OK.

If it is, it repeats the same sequence looking for the substring between the `<url>` and `</url>` tags. This code can extract strings of any length between any two tags. In this example, the length of the shortened URL string is fixed, so the code could be simplified slightly. But in this form, it’s a more general solution for extracting the contents of any tag from any XML return.

![](bbox=[0.103, 0.665, 0.173, 0.722])

# NOTE

The complete project is available on the Web site (www.wiley.com/go/cocoadevref), as is the more complex project discussed next.

# Creating asynchronous Web requests

The previous example used the same `stringWithContentsOfURL:` method to send an API request and read its return. The code is simple, but it stalls your application while it waits for the return to complete, or fail. This is called a *synchronous request*.

The more sophisticated alternative is called an *asynchronous request*. An asynchronous request creates a request object, with associated delegate methods. It then triggers the object to begin the request.