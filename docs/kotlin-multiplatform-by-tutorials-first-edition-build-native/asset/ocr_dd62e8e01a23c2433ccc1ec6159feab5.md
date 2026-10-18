To **build learn**, you need to make three different requests to:

+   - The RSS feed of a specific topic.
+   - An article webpage.
+   - Your Gravatar account.

The data for the first one is in the `RW_CONTENT` property inside the **FeedPresenter.kt** file located in the **shared** module. It can be one of the following:

+   - [All](#)
+   - [Android](#)
+   - [iOS](#)
+   - [Gametech](#)
+   - [Flutter](#)

Each of these requests loads the latest 20 articles published for its category.

The second request corresponds to the `link` field of the `RWEntry`. Since an RSS entry doesn’t contain a URL for the article image, you’ll need to fetch it manually from raywenderlich.com.

Finally, make the last request to [Gravatar](#), a service that allows you to define an online profile that can be used across external sites. Your picture from raywenderlich.com, for example, is retrieved from this service.

# How to make a network request

Open the **data** folder inside the **shared/src/commonMain** module and create a new file named **FeedAPI.kt**. Add the following code:

```
```kotlin
//1
public const val GRAVATAR_URL = "https://en.gravatar.com/"
public const val GRAVATAR_RESPONSE_FORMAT = ".json"

//2
@ThreadLocal
public object FeedAPI {

  //3
  private val client: HttpClient = HttpClient()

  //4
  public suspend fun fetchRWEntry(feedUrl: String): HttpResponse =
    client.get(feedUrl)

  //5
  public suspend fun fetchMyGravatar(hash: String): HttpResponse =
```
```