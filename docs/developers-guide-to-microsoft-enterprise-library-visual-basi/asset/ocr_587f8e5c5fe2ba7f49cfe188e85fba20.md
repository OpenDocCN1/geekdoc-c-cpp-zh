Depending on the performance of your machine, you may need to change the value configured for the expiration poll frequency of the cache manager in order to see the invalidated item in the cache and the contents after the scavenging cycle completes.

# What's In My Cache?

The example you've just seen displays the contents of the cache, indicating which items are still available in the cache, and which (if any) are in the cache but not available because they are waiting to be scavenged. So how can you tell what is actually in the cache and available for use? In the time-honored way, you might like to answer “Yes” or “No” to the following questions:

+   - Can I use the Contains method to check if an item with the key I specify is available in the cache?
+   - Can I query the Count property and retrieve each item using its index?
+   - Can I iterate over the collection of cached items, reading each one in turn?

If you answered “Yes” to any of these, the bad news is that you are wrong. All of these are false. Why? Because the cache is managed by more than one process. The cache manager you are using is responsible for adding items to the cache and retrieving them through the public methods available to your code. However, a background process also manages the cache, checking for any items that have expired and removing (scavenging) those that are no longer valid. Cached items may be removed when memory is scarce, or in response to dependencies on other items, as well as when the expiry date and time you specified when you added an item to the cache has passed.

So, even if the Contains method returns True for a specified cache key, that item might have been invalidated and is only in the cache until the next scavenging operation. You can see this in the output of the previous example, where the two waits force the code to halt until the item has been flagged as expired, and then halt again until it is scavenged. The actual delay before scavenging takes place is determined by the expiration poll frequency configuration setting of the cache manager. In the previous example, this is 10 seconds.

The correct approach to extracting cached items is to simply call the GetData method and check that it did not return Nothing. However, you can use the Contains method to see if an item was previously cached and will (in most cases) still be available in the cache. This is efficient, but you must still (and always) check that the returned item is not null after you attempt to retrieve it from the cache.

The code used in the examples to read the cached items depends on the fact that we use an array of cache keys throughout the examples, and we can therefore check if any of these items are in the cache. The code we use is shown here.