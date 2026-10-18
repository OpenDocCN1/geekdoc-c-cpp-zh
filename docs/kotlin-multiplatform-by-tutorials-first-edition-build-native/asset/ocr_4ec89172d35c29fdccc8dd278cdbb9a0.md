```
```kotlin
if (parsed != null) {
    feed += parsed
}
```
```

Moreover, you don’t need to add brackets when it’s a single instruction.

Alternatively, you could just write:

```
```kotlin
if (parsed != null)
    feed += parsed
```
```

Or even inline:

```
```kotlin
if (parsed != null) feed += parsed
```
```

# switch

It doesn’t exist in Kotlin. Alternatively, you can use `when` which is similar.

# when

`when` is a condition expression that supports multiple and different expressions. You can see an example of how to use it on the **ImagePreview.kt** file, which is inside the **components** folder of the **androidApp**:

```
```kotlin
when (painter.state) {
    is ImagePainter.State.Loading -> {
        AddImagePreviewEmpty(modifier)
    }
    is ImagePainter.State.Error -> {
        AddImagePreviewError(modifier)
    }
    else -> {
        // Do nothing
    }
}
```
```

In this case, you’re checking the current `state` of an image that’s being downloaded from the internet, and adding different composable depending on if its value is either `Loading` or `Error`.

Since all of these expressions are single-line, you could drop the brackets.

# for

Back to the **FeedPresenter.kt** file from the **shared** module. You can find the `for` loop on `fetchAllFeeds`: