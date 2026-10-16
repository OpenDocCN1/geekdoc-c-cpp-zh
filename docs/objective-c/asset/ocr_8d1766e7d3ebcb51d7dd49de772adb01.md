To illustrate this, look at Listing 12.2.

# Listing 12.2

# Examining string constant equality

```
NSString *string1 = @"this is a string";
NSString *string2 = @"this is a string"; // same object as string1
NSString *string3 = [NSString stringWithString:string1]; // makes new

assert(string1 == string2); // true
assert([string1 isEqual:string2]); // also true
assert([string1 isEqual:string3]); // true
assert(string1 == string3); // false
```

Most often, you declare strings using the Objective-C string construct, but numerous initializers and factory methods are available on the NSString and NSMutableString classes. Some of the more common ones are shown in Table 12.1.

# Table 12.1 NSString and NSMutableString factory methods.

| Method | Purpose |
|---|---|
| +string | Constructs a new empty string. |
| +stringWithFormat: | Constructs a new string using the printf-style format specifier given and any arguments required by the format specifier. |
| +stringWithCharacters:length: | Constructs a new string containing length characters retrieved from the C. style array provided. |
| +stringWithString: | Constructs a new string with the value of the given string. |
| +stringWithCString:encoding: | Constructs a new string using a C. style string by converting it using the specified encoding. |
| +stringWithUTF8String: | Constructs a new string using a C.-style string encoded with UTF-8 string encoding. This is equivalent to calling +stringWithCString:encoding: using NSUTF8Encoding for the encoding parameter. |
| +stringWithContentsOfFile:encoding:error: | Constructs a new string containing the contents of the file specified using the encoding provided. |