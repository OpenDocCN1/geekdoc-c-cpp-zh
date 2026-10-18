
correspond to the app name:

> public const val APP_NAME: String = "learn"

Since this value should be the same for both platforms, you’re going to use it as the value for the header request.

Now, if you want to add this header to all requests done through Ktor, you need to locate `client` in the **FeedAPI.kt** file. When you’re overriding the `client`, before the call to `install` add:

> defaultRequest {
>     header(X_APP_NAME, APP_NAME)
> }

Calling `defaultRequest` directly is the equivalent of:

> install(DefaultRequest)

In other words, similar to what you did for logging, you’re setting the default configuration for every request. In this case, you’re adding an `X_APP_NAME` header.

Now, compile the app on all three applications. By opening Logcat (Android), terminal (desktop) and Xcode console (iOS), confirm in the log messages that you’re sending this new header.

![](img/2f50555a40af4ea8c85f09e577f0c5b9_272_0.png)

The shared module.

Start by creating a data class that’s going to represent an image. Go to commonMain and inside platform create a PlatformMediaFile.kt file:

```kotlin
public expect class MediaFile

public expect fun MediaFile.toByteArray(): ByteArray
```

Here, you’re defining the class and function that you’ll use to represent a file. At the platform level, the MediaFile class and the corresponding toByteArray function will be defined.

With this in mind, navigate to androidMain. Inside platform, create the corresponding actual file — PlatformMediaFile.kt:

```kotlin
public actual typealias MediaFile = MediaUri

public actual fun MediaFile.toByteArray(): ByteArray = contentResolver.openInputStream(uri)?.use {
    it.readBytes()
} ?: throw IllegalStateException("Couldn't open inputStream $uri")
```

Here, you’re defining the reference of MediaFile as MediaUri. Every time MediaFile is accessed, the properties and functions that will be called are the ones from MediaUri. This class doesn’t yet exist. You’ll need to create it, because in order to get the ByteArray from a file, Android needs to access the openInputStream from contentResolver that only exists in the activity context.

Inside data/model, create a MediaUri.kt file and add:

```kotlin
public data class MediaUri(public val uri: Uri, public val contentResolver: ContentResolver)
```

This contentResolver property is the one that’s accessed in toByteArray, from which you can openInputStream.

Once done, it’s now time to define the iOS implementation. Create the PlatformMediaFile.kt in the platform package inside the iosMain folder and add:

```kotlin
public actual typealias MediaFile = UIImage

public actual fun MediaFile.toByteArray(): ByteArray {
    return UIImageJPEGRepresentation(this, compressionQuality = 1.0)?.toByteArray()
        ?: emptyArray<Byte>().toByteArray()
}
```

In this case, `MediaFile` is represented as a `UIImage`. The `ByteArray` required for the upload is retrieved from the call to `UIImageJPEGRepresentation`.

With these implementations, you can now access the file’s content and upload it. Although it’s beyond the scope of this chapter, it’s worth showing you an example of how it can be made at Ktor level.

Imagine that you selected an image to upload. Assuming your server supports multipart requests, you could write a similar function:

```kotlin
//1
public suspend fun uploadAvatar(data: MediaFile): HttpResponse {
    //2
    return client.post(UPLOAD_AVATAR_URL) {
        //3
        body = MultiPartFormDataContent(
            formData {
                appendInput("filedata", Headers.build {
                    //4
                    append(HttpHeaders.ContentType, "application/octet-stream")
                }) {
                    //5
                    buildPacket { writeFully(data.toByteArray()) }
                }
            }
        )
    }
}
```

Here’s what’s happening:

1. You need to receive the `MediaFile` that contains a reference to your image. The important part of this object is the `toByteArray` function that’s used on 5.
2. The `client` in this example is the same that you’ve been using until now. There’s no need to install additional plugins or set any configuration.
3. In this case, the file will be sent through a multipart request, so the `body` of the request needs to contain this information.
4. Most servers require that the request contains the content type of the file — in this case, `application/octet-stream`.
5. Depending on the total size of the file, more than one part might need to be sent. Although the result is always an array of bytes, depending on the platform that your app is running, `toByteArray` will call different functions.

> Note: Depending on the file type you want to send and the server requirements, you may need to implement a different method. For more information, read the official documentation from Ktor.

To write tests for Ktor, you need to create a mock object of the HttpClient and then test the different responses that you can receive.

Before writing, you need to open the build.gradle.kts file from shared and include the following in commonTest:

```kotlin
implementation(kotlin("test-junit"))
implementation("junit:junit:4.13.2")
implementation("io.ktor:ktor-client-mock:2.0.0-beta-1")
```

Wait for the project to synchronize.

After it finishes, open commonTest and inside shared, create a NetworkTests class. All your network tests will be here.

Before creating the tests, you need to mock some objects. After the class declaration, add:

```kotlin
private val profile = GravatarProfile(
    entry = listOf(
        GravatarEntry(
            id = "1000",
            hash = "1000",
            preferredUsername = "Ray Wenderlich",
            thumbnailUrl = "https://avatars.githubusercontent.com/u/4722515?s=200&v=4"
        )
    )
)
```

This will be the GravatarProfile that you’re expecting to receive on mocked network calls.

Now, you’ll need to mock the HttpClient. Add it below the code you just pasted:

```kotlin
private val nonStrictJson = Json { isLenient = true; ignoreUnknownKeys = true }

private fun getHttpClient(): HttpClient {
    //1
    return HttpClient(MockEngine) {
```

```kotlin
public fun testFetchMyGravatar() = runTest {
    val client = getHttpClient()
    assertEquals(profile, client.request("$GRAVATAR_URL${profile.entry[0].hash}$GRAVATAR_RESPONSE_FORMAT").body())
}
```

The test passes if the response it receives is the same as the `profile` object mocked; it fails otherwise.

To run a test, right-click the class name **NetworkTests**, then click “Run ‘NetworkTests’”, or with the file open, just click on the green arrows shown next to a test and choose **android (:testDebugUnitTest)**.

## Challenge

Here is a challenge for you to practice what you’ve learned in this chapter. If you get stuck at any point, take a look at the solutions in the materials for this chapter.

### Challenge: Send your package name in a request header

You’ve learned how to define a header in a request. In that example, you were sending the app name as its value. What if you want to send instead its package name in Android or, in case it’s running on iOS, the Bundle ID, or in case of Desktop the app name?

> **Note:** You should implement this logic on the shared module.

## Key points

- Ktor is a set of networking libraries written in Kotlin. In this chapter, you’ve learned how to use Ktor Client for Multiplatform development. It can also be used independently in Android or desktop. There’s also Ktor Server; that’s used server-side.
- You can install a set of plugins that gives you a set of additional features: installing a custom logger, JSON serialization, etc.

## Where to go from here?

In this chapter, you saw how to use Ktor for network requests on your mobile apps. Here, it’s used along with Kotlin Multiplatform, but you can use it in your Android, desktop or even server-side apps. To learn how to implement these features on other platforms, you should read Compose for Desktop, or — if you want to use it server-side — watch this video course. Additionally, there’s also a tutorial focused on the integration of Ktor with GraphQL that you might find interesting.

The next chapter is focused on concurrency — in particular, how to use coroutines in your application.

See you there.
