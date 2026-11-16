```
.SetAbsoluteExpiration(TimeSpan.FromMinutes(5)); // Set cache
expiration
    _cache.Set(cacheKey, products, cacheEntryOptions);
}
return View(products);
}
```

In this example, we first add in-memory caching services in the ConfigureServices method. Then, in the Index action, we attempt to retrieve the product list from the cache using a cache key. If the data is not found in the cache, we retrieve it from the database, store it in the cache with an expiration time of 5 minutes, and then return it to the view.

# 2. Distributed Caching

```
C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddStackExchangeRedisCache(options =>
    {
        options.Configuration = Configuration["Redis:ConnectionString"];
        options.InstanceName = "MyFirstWebApplication";
    });
}
```

// ... (Similar usage as in-memory caching, but with IDistributedCache instead of IMemoryCache)