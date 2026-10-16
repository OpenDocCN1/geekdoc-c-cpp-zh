| Method | Purpose |
|---|---|
| +stringWithContentsOfURL:encoding:error: | Constructs a new string containing the contents of the resource specified by the URL. The resource will be downloaded using the specified protocol, and decoded using the provided encoding. This call will block while the resource is downloading. |
| +stringWithContentsOfFile:usedEncoding:error: | Constructs a new string containing the contents of the file specified. Will attempt to automatically detect the type of file encoding used and inform the caller of the type of encoding detected via the usedEncoding out parameter. |
| +stringWithContentsOfURL:usedEncoding:error: | Constructs a new string containing the contents of the resource specified by the provided URL. Will download the resource, and attempt to detect the type of file encoding used and inform the caller of the encoding type via the usedEncoding out parameter. |

Each of these also has an initializer version that can be used if you prefer to create your strings that way.

# NOTE

The term “factory method” refers to class methods that can be used to construct an object using particular arguments.

# Using format strings

One of the more commonly used factory methods is the +stringWithFormat: factory method, which utilizes a printf style format string and a list of arguments to construct the string. (I use format strings in many of the examples of this book. Every time you see a call to NSLog, you see an instance of a format string.) Listing 12.3 shows an example of a format string used with a call to NSLog.

# Listing 12.3

# The format string in NSLog

```
NSLog(@"The age of the employee named %@ is %ld", [employee name], [employee age]);
```

The use of @"" indicates the format string is an instance of NSString. When creating a format string, you use a special combination of percent signs and characters to indicate particular