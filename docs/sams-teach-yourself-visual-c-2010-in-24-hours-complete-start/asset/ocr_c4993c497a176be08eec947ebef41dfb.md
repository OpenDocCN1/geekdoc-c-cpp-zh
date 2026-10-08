shown in Table 2.7 are common to both Uri (where they are read-only) and UriBuilder except for the Uri property, which is only available on UriBuilder.

# TABLE 2.7  Common Uri and UriBuilder Properties

| Name | Description |
| --- | --- |
| Fragment | Gets or sets the fragment portion of the URI |
| Host | Gets or sets the hostname or IP address of a server |
| Password | Gets or sets the password associated with the user who accesses the URI |
| Path | Gets or sets the path to the resource defined by the URI |
| Port | Gets or sets the port number of the URI |
| Query | Gets or sets any query information included in the URI |
| Scheme | Gets or sets the scheme name of the URI |
| Uri | Gets the Uri instance constructed by the specified UriBuilder instance |
| UserName | Gets or sets the username associated with the user who accesses the URI |

Listing 2.1 shows how to use the UriBuilder class.

# LISTING 2.1  Working with UriBuilder

```
```
Uri immutableUri = new Uri("http://www.example.com");
Console.WriteLine(immutableUri);

UriBuilder mutableUri = new UriBuilder(immutableUri);
Console.WriteLine(mutableUri);

mutableUri.Scheme = "https";
mutableUri.Host = "www.example.com";
mutableUri.Path = "exampleFile.html";
Console.WriteLine(mutableUri);
```
```

# BigInteger

The System.Numerics.BigInteger type represents an arbitrarily large integer value that has no theoretical upper or lower bound. When a BigInteger instance has been created, you can use it just as you would any of the other integer types, enabling you to perform basic mathematical operations and comparisons.