```
```csharp
class HeaderDemo {
    static void Main() {
        // Create a WebRequest to a URI.
        HttpWebRequest req = (HttpWebRequest)
        WebRequest.Create("http://www.McGraw-Hill.com");

        // Send that request and return the response.
        HttpWebResponse resp = (HttpWebResponse)
        req.GetResponse();

        // Obtain a list of the names.
        string[] names = resp.Headers.AllKeys;

        // Display the header name/value pairs.
        Console.WriteLine("{0,-20}\n", "Name", "Value");
        foreach (string n in names) {
            Console.Write("{0,-20}", n);
            foreach (string v in resp.Headers.GetValues(n))
                Console.WriteLine(v);
        }

        // Close the response.
        resp.Close();
    }
}
```
```

Here is the output that was produced. (Remember, all header information is subject to change, so the precise output that you see may differ.)

| Name | Value |
|---|---|
| Transfer-encoding | chunked |
| Content-Type | text/html |
| Date | Fri, 27 Jun 2008 20:32:06 GMT |
| Server | Sun-ONE-Web-Server/6.1 |

# Accessing Cookies

You can gain access to the cookies associated with an HTTP response through the Cookies property defined by HttpWebResponse. Cookies contain information that is stored by a browser. They consist of name/value pairs, and they facilitate certain types of web access.

```
```csharp
public CookieCollection Cookies { get; set; }
```
```

CookieCollection implements ICollection and IEnumerable and can be used like any other collection. (See Chapter 24.) It has an indexer that allows a cookie to be obtained by specifying its index or its name.

```
```csharp
public string Name { get; set; }
public string Value { get; set; }
```
```