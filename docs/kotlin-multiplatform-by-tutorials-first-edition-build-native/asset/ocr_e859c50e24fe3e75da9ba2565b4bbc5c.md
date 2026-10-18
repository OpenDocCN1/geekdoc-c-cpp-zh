```
```kotlin
xmL\",\"image\":\"https://assets.carolus.rawenderlich.com/assets/razeaware_460-308933a0bda63e3e327123cab8002c0383a714cd35a10ade9bae9ca20b1f438b.png\"}\")
    assertEquals(content, decoded)
}
```
```

Here, you’re validating that your JSON serialization is capable of encoding a **RWContent** object, `data`, to a string. This property corresponds to the **all** section in **learn**. If the serializer is working correctly, the result of `encodeToString` needs to be the same as `content`—otherwise the test will fail. Click the green arrow by the function on the left to run the test and select **android (testDebugUnitTest)**. You’ll see the test passes.

Now to test if the deserialization is correct, add the following method:

```
```kotlin
@Test
fun testDecodePlatformAll() {
    val data = "{\"platform\":\"all\",\"url\":\"https://www.raywenderlich.com/feed.xml\",\"image\":\"https://assets.carolus.rawenderlich.com/assets/razeware_460-308933a0bda63e3e327123cab8002c0383a714cd35a10ade9bae9ca20b1f438b.png\"}"

    val decoded = Json.decodeFromString(RWContent.serializer(), data)
    val content = RWContent(
        platform = PLATFORM.ALL,
        url = "https://www.raywenderlich.com/feed.xml",
        image = "https://assets.carolus.rawenderlich.com/assets/razeware_460-308933a0bda63e3e327123cab8002c0383a714cd35a10ade9ca20b1f438b.png"
    )

    assertEquals(content, decoded)
}
```
```

Essentially, you do the opposite. Starting with the JSON response, you’ll need to call `decodeFromString` so **kotlinx.serialization** builds your **RWContent** object, `decoded`, and then you’ll compare it with the one that you’re expecting — `content`. If the content is the same, the test successfully passes. Run the test and see that it passes.

# Testing custom serialization

To test your custom **RWSerializer**, you first need to define:

```
```kotlin
private val serializers = serializersModuleOf(PLATFORM::class,
RWSerializer)
```
```