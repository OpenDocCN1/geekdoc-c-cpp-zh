The next time a request comes in for one of these pages, it won't be satisfied from the cache, and the application will handle it. In the process, it'll automatically repopulate that particular page in the cache, lightening the load for subsequent fetches of this page.

Where do you find the cache files to delete? Not surprisingly, this is configurable. Page cache files are by default stored in the public directory of your application. They'll be named after the URL they are caching, with an .html extension. For example, the page cache file for content/show/1 will be here:

```
app/public/content/show/1.html
```

This naming scheme is no coincidence; it allows the web server to find the cache files automatically. You can, however, override the defaults using this:

```
config.action_controller.page_cache_directory = "dir/name"
config.action_controller.page_cache_extension = ".html"
```

Action cache files are not by default stored in the regular filesystem directory structure and cannot be expired using this technique.

# Playing Nice with Client Caches

When we said earlier that creating cached pages is only one half of the equation, we failed to mention that there are three halves. Oops.

Clients (generally, but not always, browsers) often have caches too. Intermediaries between your server and the client may also providing caching services. You can help optimize these caches (and therefore reduce load on your server) by providing HTTP headers. Doing so is entirely optional and won't always result in a bandwidth reduction, but on the other hand, sometimes the savings can be quite significant.

# Expiration Headers

The most efficient request is the request that is never made. Many pages (particularly images, scripts, and stylesheets) change very rarely yet may be referenced fairly frequently. One way to ensure that re-retrievals are optimized out before they get to your server is to provide an Expires header.

Although an Expires header may provide a number of different options, the most common usage is to indicate how long the given response is to be considered "good for," suggesting that the client need not re-request this data in the interim. Calling the expires_in method in your controller achieves this result:

```
expires_in 20.minutes
expires_in 1.year
```

A server should not provide a dates more than one year in the future on Expires headers.