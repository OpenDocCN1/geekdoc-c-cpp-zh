```
```java
try {
    httpClient.executeMethod(method);
    String response = method.getResponseBodyAsString();
    return response;
} catch (Exception e) {
    handle(e);
} finally {
    method.releaseConnection();
}
}
}
```

The next class is the iterator that provides the contents of the pages based on an iterator of URLs:

```
```java
public class PageIterator {
    private PageReader reader;
    private URLIterator urls;

    public PageIterator(PageReader reader, URLIterator urls) {
        this.urls = urls;
        this.reader = reader;
    }

    public synchronized String getNextPageOrNull() {
        if (urls.hasNext())
            getPageFor(urls.next());
        else
            return null;
    }

    public String getPageFor(String url) {
        return reader.getPageFor(url);
    }
}
```
```

An instance of the `PageIterator` can be shared between many different threads, each one using its own instance of the `PageReader` to read and parse the pages it gets from the iterator.