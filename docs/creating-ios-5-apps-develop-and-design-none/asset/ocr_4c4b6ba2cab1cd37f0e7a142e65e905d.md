Here, we instantiate an `NSMetadataQuery` object. We will use this to search our iCloud storage for files. We start by setting the search scope. There are two possible scopes: `NSMetadataQueryUbiquitousDocumentsScope` and `NSMetadataQueryUbiquitousDataScope`. The first searches inside our iCloud container’s Documents folder. The second searches through everything else in the container.

Next, we set the search’s predicate. In our case, we’re searching for any files named `health_beat.hbhistory`. Note that the predicate’s `LIKE` string comparison can also accept wildcards. For example, using `@"%K like '*.hbhistory'"` for our format would match any files ending in `.hbhistory`.

> > **NOTE:** When we enter a string value directly into a predicate format, we need to wrap it in quotes. Both single and double quotes are acceptable. However, when we pass in a string using substitution and the `%@` placeholder, the system automatically quotes the string for us. Importantly, strings passed into a `%K` placeholder are not quoted—which is why we use `%K` for passing in key names instead of `%@`.

![](bbox=[0.753, 0.429, 1.0, 0.548])

Additionally, we could use some of the other predicate string comparisons, including `BEGINSWITH` and `ENDSWITH` (but not `CONTAINS` or `MATCHES`). For more information, check out “String Comparisons” in the Predicates Programming Guide.

```
~~~objective-c
[[NSNotificationCenter defaultCenter]
    addObserverForName
    NSMetadataQueryDidFinishGatheringNotification
    object:query
    queue:nil
    usingBlock:^(NSNotification* notification) {
        [query disableUpdates];
        [[NSNotificationCenter defaultCenter]
            removeObserver:self
            name:NSMetadataQueryDidFinishGatheringNotification
            object:query];
        [self processQuery:query
~~~
```