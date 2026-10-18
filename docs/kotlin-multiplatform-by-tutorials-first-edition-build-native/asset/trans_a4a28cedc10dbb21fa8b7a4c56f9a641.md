
对应的应用名称：

> public const val APP_NAME: String = "learn"

由于该值在两个平台上都应保持一致，你将使用它作为 header request 的值。

现在，如果你想为通过 Ktor 发出的所有请求添加这个 header，需要在 **FeedAPI.kt** 文件中定位 `client`。在覆盖 `install` 之前，添加：

> defaultRequest {
>     header(X_APP_NAME, APP_NAME)
> }

直接调用 `defaultRequest` 相当于：

> install(DefaultRequest)

换句话说，就像你为日志设置一样，你正在为每个请求设置默认配置。在此情况下，你正在添加一个 `X_APP_NAME` 头。

现在，在三个应用上编译应用。通过打开 Logcat（Android）、终端（桌面）和 Xcode 控制台（iOS），确认日志信息中已发送此新 header。

![](img/2f50555a40af4ea8c85f09e577f0c5b9_272_0.png)

共享模块。

首先，在 commonMain 目录下的 platform 文件夹中创建 PlatformMediaFile.kt 文件：

```kotlin
public expect class MediaFile

public expect fun MediaFile.toByteArray(): ByteArray
```

在此，你定义了用于表示文件的类以及 `toByteArray` 函数。在平台级别，MediaFile 类和对应的 toByteArray 函数将在此处定义。

基于此，转到 androidMain 目录下的 platform 文件夹，创建对应的实际文件 — PlatformMediaFile.kt：

```kotlin
public actual typealias MediaFile = MediaUri

public actual fun MediaFile.toByteArray(): ByteArray = contentResolver.openInputStream(uri)?.use {
    it.readBytes()
} ?: throw IllegalStateException("Couldn't open inputStream $uri")
```

在此，你定义 MediaFile 为 MediaUri 的别名。每次访问 MediaFile 时，调用的属性和函数都是 MediaUri 类中的。该类目前尚未存在，需要创建，因为在 Android 上获取文件的 ByteArray 需要通过 activity 环境中的 contentResolver 调用 openInputStream。

在 data/model 目录下，创建 MediaUri.kt 文件并添加：

```kotlin
public data class MediaUri(public val uri: Uri, public val contentResolver: ContentResolver)
```

contentResolver 属性是 toByteArray 中用于调用 openInputStream 的，从而获取文件内容。

接下来，是时候定义 iOS 实现了。在 iosMain 目录下的 platform 包中创建 PlatformMediaFile.kt 文件并添加：

```kotlin
public actual typealias MediaFile = UIImage

public actual fun MediaFile.toByteArray(): ByteArray {
    return UIImageJPEGRepresentation(this, compressionQuality = 1.0)?.toByteArray()
        ?: emptyArray<Byte>().toByteArray()
}
```

在此，MediaFile 表示为 UIImage。用于上传的 ByteArray 通过调用 UIImageJPEGRepresentation 获取。

有了这些实现，你现在可以访问文件内容并进行上传。虽然超出了本章范围，但展示一个在 Ktor 级别如何使用它是有价值的。

想象你已选择一张图片进行上传。假设你的服务器支持 multipart 请求，你可以编写类似的函数：

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

以下是该过程的说明：

1. 你需要接收包含图片引用的 `MediaFile` 对象。该对象的关键部分是 `toByteArray` 函数，它在第 5 步中被使用。
2. 此示例中的 `client` 与之前使用的相同，无需安装额外插件或设置配置。
3. 由于文件将通过 multipart 请求发送，请求的 `body` 必须包含此信息。
4. 大多数服务器要求请求包含文件的内容类型 — 此处为 `application/octet-stream`。
5. 取决于文件总大小，可能需要发送多个部分。虽然结果总是字节数组，但根据应用运行的平台，`toByteArray` 会调用不同的函数。

> **注意**：根据你想要发送的文件类型和服务器要求，可能需要实现不同的方法。更多信息请参阅 Ktor 官方文档。

要为 Ktor 编写测试，需要创建 HttpClient 的 mock 对象，然后测试可以接收的不同响应。

在此之前，需要在 shared/build.gradle.kts 文件中，于 commonTest 中添加以下依赖：

```kotlin
implementation(kotlin("test-junit"))
implementation("junit:junit:4.13.2")
implementation("io.ktor:ktor-client-mock:2.0.0-beta-1")
```

等待项目同步完成。

同步后，打开 commonTest，在 shared 目录下创建 NetworkTests 类。所有网络测试都将在此处。

在类声明后，添加以下代码来 mock 一些对象：

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

这将是你在模拟网络请求时期望接收的 GravatarProfile。

接下来，需要 mock HttpClient。在上述代码下方添加：

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

如果接收到的响应与 mock 的 `profile` 对象相同，测试通过；否则失败。

运行测试时，右键点击 **NetworkTests** 类名称，选择“Run ‘NetworkTests’”，或在文件打开时，点击绿色箭头并选择 **android (:testDebugUnitTest)**。

## 挑战

以下是本章练习题，帮助你巩固所学知识：

### 挑战：在请求头中发送你的包名

你已学习如何在请求头中定义 header。在之前的示例中，你发送的是应用名称作为值。如果你想发送包名（Android）或 Bundle ID（iOS），或 Desktop 的应用名称呢？

> **注意**：此逻辑应在共享模块中实现。

