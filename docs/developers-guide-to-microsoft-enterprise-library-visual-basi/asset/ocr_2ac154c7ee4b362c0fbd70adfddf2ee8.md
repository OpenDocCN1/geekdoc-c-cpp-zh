![](bbox=[0.106, 0.066, 0.813, 0.532])

# FIGURE 1 Configuring caching in Enterprise Library

For each cache manager, you can specify the expiration poll frequency (the interval in seconds at which the block will check for expired items and remove them), the maximum number of items in the cache before scavenging will occur irrespective of the polling frequency, and the number of items to remove when scavenging the cache.

You can also specify, in the configuration properties of the Caching Application Block root node, which of the cache managers you configure should be the default. The Caching block will use the one you specify if you instantiate a cache manager without providing the name of that cache manager.

# PERSISTENT CACHING

The cache manager caches items in memory only. If you want to persist cached items across application and system restarts, you can add a persistent backing store to your configuration. You can specify only a single backing store for each cache manager (obviously, or it would get extremely confused), and the Caching block contains providers for caching in both a database and isolated storage. You can specify a partition name for each persistent backing store, which allows you to target multiple cache storage providers at isolated storage or at the same database.